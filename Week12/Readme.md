```c
struct Edge
{
  int from, to, w;  
  bool operator<(const Edge& rhs)const
  {
    return w > rhs.w;
  }
};

int prims(int n, vector<vector<int>> edges, int start) {
    map<int, vector<Edge>> gr;
    for(int i = 0; i < edges.size(); i++)
    {
        gr[edges[i][0]].push_back({edges[i][0],edges[i][1], edges[i][2]});
        gr[edges[i][1]].push_back({edges[i][1],edges[i][0], edges[i][2]});
    }
    
    vector<Edge> res;
    priority_queue<Edge> pq;
    pq.push({start, start, 0});
    set<int> vis; // !!
    
    while(!pq.empty())
    {
        auto curr = pq.top(); pq.pop();
        if(vis.count(curr.to)) continue; //!!!
        
        res.push_back(curr);
        vis.insert(curr.to);
        for(auto& nb: gr[curr.to])
        {
            if(!vis.count(nb.to))
            {
                pq.push(nb);
            }
        }
    }
    
    if(res.size() < n)
    return -1;
    int result = 0;
    for(int i = 0; i < res.size(); i++)
    result += res[i].w;
    return result;
}

```
