
Най-кратък път в **непретеглен** граф се намира чрез Breadth-first search (BFS).

## Dijkstra's algorithm (Алгоритъм на Дейкстра)

Greedy алгоритъм, който пресмята най-кратък път от начален връх до всички останали в **претеглен** граф.

При използването на Binary Heap сложността е **O(E*logV)**.

Алгоритъмът **не работи** правилно при наличие на ребро с **отрицателна** тежест.

```c
struct Node
{
  int indx,dist;   
    bool operator<(const Node& rhs)const
    {
        return dist > rhs.dist;
    }
};
struct Edge
{
    int to,w;

};
vector<int> shortestReach(int n, vector<vector<int>> edges, int s) {
    vector<int> res(n, INT_MAX); //unreachable
    
    map<int, vector<Edge>>gr;                //na vs vruh rubovete // graph of EDGES
    for(size_t i = 0; i < edges.size(); i++) //undirected
    {
        gr[edges[i][0]].push_back({edges[i][1], edges[i][2]});
        gr[edges[i][1]].push_back({edges[i][0], edges[i][2]});
    }
    
    priority_queue<Node> pq; // !!!! pq of NODES
    pq.push({s,0});
    res[s - 1] = 0;
    
    while(!pq.empty())
    {
        auto curr = pq.top(); pq.pop();
        if(curr.dist > res[curr.indx - 1]) continue; // we have seen diff and better
        
        for(auto edge: gr[curr.indx])
        {
            int newW = curr.dist + edge.w;
            if(res[edge.to - 1] > newW) // is it better
            {
                res[edge.to - 1] = newW;
                pq.push({edge.to, newW});
            }
        }
        
    }
    //res.erase(res.begin() + s - 1);
    /*for(size_t i = 0; i < res.size(); i++) {
        if(res[i] == INT_MAX) {
            res[i] = -1;
        }
    }*/
    return res;
}
```
