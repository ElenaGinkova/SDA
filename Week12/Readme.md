## Prim
МПД

Имплементацията наподобява тази на алгоритъма на Дийкстра с разликата, че приоритетната опашка държи ребра, а не двойка връх и изминат път от началото до него.

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
## Kruskal

```c

struct Edge
{
  int from, to,w;
  bool operator<(const Edge& rhs)const
  {
    return w < rhs.w;
  }  
};
int find(int x, vector<int>& parents)
{
    return parents[x] == x ? x : parents[x] = find(parents[x], parents); 
}
void yu(int x, int y, vector<int>& parents)
{
    parents[find(x,parents)] = find(y, parents);
}
int kruskals(int n,   vector<Edge>& edges){
    sort(edges.begin(), edges.end());
    vector<int> parents(n + 1);
    for(int i = 1; i <= n; i++)
    {
        parents[i] = i;
    }
    int W = 0;
    for(int i = 0; i < edges.size(); i++)
    {
        if(find(edges[i].from, parents) == find(edges[i].to, parents)) continue;
        yu(edges[i].from, edges[i].to, parents);
        W += edges[i].w;
    }
    return W;
}

int main()
{
    int V, E;
    cin >> V >> E;
    vector<Edge> edges;
    for(int i = 0; i < E; i++)
    {
        int from, to,w;
        cin >> from >> to >> w;
        edges.push_back({from, to ,w});
        edges.push_back({to,from,w});
    }
    cout << kruskals(V, edges);
}
```
## points
```c
class Solution {
public:
    
    struct Node
    {
        int x, y;
    };
    struct Edge
    {
        int from, to;
        int len;
        bool operator<(const Edge& rhs)const
        {
            return len < rhs.len;
        }
    };
    void fill(vector<Edge>& edges, vector<Node> nodes)
    {
        for(int i = 0; i < nodes.size(); i++)
        {
            for(int j = i + 1; j < nodes.size(); j++)
            {
                int x1 = nodes[i].x, y1 = nodes[i].y;
                int x2 = nodes[j].x, y2 = nodes[j].y;
                int len = abs(x1 - x2) + abs(y1 - y2);
                edges.push_back({i, j, len});
            }
        }
    }
    int find(int x, map<int, int>& parents)
    {
        return parents[x] == x ? x : parents[x] = find(parents[x], parents);
    }
    void yu(int x, int y, map<int, int>& parents)
    {
        parents[find(x, parents)] = find(y, parents);
    }
    int minCostConnectPoints(vector<vector<int>>& points) {
        vector<Node> nodes;
        vector<Edge> edges;
        for(int i = 0; i < points.size(); i++)
        {
            int x = points[i][0]; int y = points[i][1]; 
            nodes.push_back({x, y});
        }
        fill(edges, nodes);
        sort(edges.begin(), edges.end());
        map<int,int> parents;
        for(int i = 0; i < points.size(); i++)
        {
            parents[i] = i;
        }
        int cost = 0;
        for(int i = 0; i < edges.size(); i++)
        {
            if(find(edges[i].from, parents) == find(edges[i].to, parents)) continue;
            yu(edges[i].from, edges[i].to, parents);
            cost += edges[i].len;
        }
        return cost;
    }
};
```
