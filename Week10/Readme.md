## Breadth First Search

Разделя възлите на посетени и непосетени. !!!

Започва да обхожда от начален връх.

Добавя всички съседи, които не са посетени.

-> Намира **най-къс път** от даден възел до всички останали в непретеглен граф 
```c

void bfs(int s, map<int, set<int>>& graph, vector<int>& res) {

    queue<int> q; // !!!
    set<int> visited; // !!!

    q.push(s); // start
    visited.insert(s); //start
    int distance = 1;
    res[s] = 0;

    while (!q.empty()) {
        int level_size = q.size();

        for (int i = 0; i < level_size; ++i) // visit only v of this lvl
        {
            int curr = q.front(); q.pop();

            for (int nb : graph[curr]) // add all not visited neighbors
            { 
                if (!visited.count(nb)) {
                    res[nb] = distance;
                    visited.insert(nb);
                    q.push(nb);
                }
            }
        }
        distance++;
    }
}
```
## Depth First Search
Разделя възлите на посетени и непосетени. // !!!

Започва да обхожда от начален връх.

Добавя всички съседи, които не са посетени, към края на стек* // !!!

-> Удобен за намиране на **компоненти на свързаност**, проверка за **цикъл в граф** и **топологична сортировка**. (*Забележка: Възможно е и използването на BFS за решаване на горните проблеми.)
```c
void dfs(int current, unordered_set<int> &visited, unordered_map<int, unordered_set<int>> &graph) {
    visited.insert(current);

    for (int neighbor : graph[current]) {
        if (!visited.count(neighbor)) {
            dfs(neighbor, visited, graph);
        }
    }
}
```
```c
void dfsIterative(int start, unordered_map<int, unordered_set<int>>& graph) {
    unordered_set<int> visited;
    stack<int> s;
    s.push(start);

    while (!s.empty()) {
        int current = s.top();
        s.pop();

        if (!visited.count(current)) {
            visited.insert(current);

            for (int neighbor : graph[current]) {
                if (!visited.count(neighbor)) {
                    s.push(neighbor);
                }
            }
        }
    }
}
```
## Топологична сортировка

Подрежда върховете, така че всеки възел се намира преди наследниците си, към които има ребра.

Задачата може да се реши чрез DFS или BFS.
```c
void topological_dfs(int current, unordered_set<int> &visited, vector<int> &stack, unordered_map<int, unordered_set<int>> &graph) {
    visited.insert(current);

    for (int neighbor : graph[current]) { // посети вс съседи
        if (!visited.count(neighbor)) {
            topological_dfs(neighbor, visited, stack, graph);
        }
    }
    stack.push_back(current); // добави накрая в резултата
}

vector<int> topological_sort(unordered_map<int, unordered_set<int>> &graph) {
    vector<int> stack;
    unordered_set<int> visited;

    for (auto iter = graph.begin(); iter != graph.end(); ++iter) { // посети всеки връх
        int vertex = iter->first;
        if (!visited.count(vertex)) {
            topological_dfs(vertex, visited, stack, graph);
        }
    }

    std::reverse(stack.begin(), stack.end());

    return stack; // 1 4 2 3 5 6
}
```
```c

vector<int> bfs(int n, int s, map<int, set<int>> gr) {
    vector<int> res(n + 1);
    set<int> visited;
    queue<int> q;
    q.push(s);
    visited.insert(s);
    int len = 0;
    while(!q.empty())
    {
        int size = q.size();
        for(int i = 0; i < size; i++)
        {
            int curr = q.front(); q.pop();
            visited.insert(curr);
            res[curr] = len;
            for(auto& nb: gr[curr])
            {
                if(!visited.count(nb))   
                {q.push(nb);visited.insert(nb);}
            }
        }
        len++;
    }
    return res;
}

int main()
{
     int Q;
    std::cin >> Q;

    while (Q--)
    {
        std::map<int, std::set<int>> graph;
        int V, E, start, v, w;
        std::cin >> V >> E;
        for (int i = 0; i < E; i++)
        {
            std::cin >> v >> w;
            graph[v].insert(w);
            graph[w].insert(v);
        }
        std::cin >> start;
        std::vector<int> results = bfs(V, start, graph);
    }
```
```c
void dfs(int s, map<int, set<int>>& gr, set<int>& vis)
{
    vis.insert(s);
    for(int nb:gr[s])
    {
        if(!vis.count(nb))
            dfs(nb, gr,vis);
    }
} // but more time complexity
void bfs(int s, map<int, set<int>>& gr, set<int>& vis)
{
    queue<int> q;
    q.push(s);
    vis.insert(s);
    
    while(!q.empty())
    {
        int curr = q.front(); q.pop();
        for(auto nb:gr[curr])
        {
            if(!vis.count(nb))
            {
                q.push(nb);
                vis.insert(nb);
            }
        }
    }
}
int countBFS(int v, map<int, set<int>>& gr)
{
    set<int> vis;
    int c = 0; 
    for(int i = 0; i < v; i++)
    {
        if(!vis.count(i))
        {
            bfs(i, gr, vis);
            c++;
        }
    }
    return c;
}
```
```c
bool dfs(int i, map<int, set<int>>& gr, vector<int>& vis)
{
    vis[i] = 1;
    for(auto nb:gr[i])
    {
        if(vis[nb] == 2) continue;
        if(vis[nb] == 1)
        {
            return true;
        }   
        if(dfs(nb, gr,vis)) return true;
    }
    vis[i] = 2;
    return false;
}
bool cycle(int V, map<int, set<int>>& gr)
{
    vector<int>visited(V + 1, 0);
    for(int i = 1; i <= V; i++)
    {
        if(visited[i] == 0)
        if(dfs(i, gr, visited))return true;
    }
    return false;
}
```
```c
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> neighbors;
};
*/

class Solution {
public:
    map<Node*, Node*> m;
    Node* cloneGraph(Node* node) {
        if(!node) return node;
        auto it = m.find(node);
        if(it != m.end())
        {
            return it->second;
        }
        Node* newNode = new Node(node->val);
        m[node] = newNode;
        for(auto nb: node->neighbors)
        {
            newNode->neighbors.push_back(cloneGraph(nb));
        }
        return newNode;
    }
};
```
```c
vector<vector<int>> res;

    void dfs(int i, vector<vector<int>>& m, vector<int>& temp)
    {
        temp.push_back(i);
        if(i == m.size() - 1)
        {
            res.push_back(temp);
            temp.pop_back();
            return;
        }
        for(auto& nb: m[i])
        {
            dfs(nb, m, temp);
        }
        temp.pop_back();
    }
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
        vector<int> temp;
        dfs(0, graph, temp);  
        return res;
    }
```
```c
int res = 0;
int dfs(vector<set<int>>& gr, set<int>& vis, int i)
{
    
    int ch = 1;
    vis.insert(i);
    
    for(auto& nb: gr[i])
    {
        if(!vis.count(nb))
        ch += dfs(gr, vis, nb);
    }
    
    if(ch % 2 == 0)
    {
        res++;
        return 0;
    }
    
    return ch;
}

int main() {
    int V, E, e1, e2;
    cin >> V >> E;
    vector<set<int>>gr(V + 1);
    for(int i = 0; i < E; i++)
    {
        cin >> e1 >> e2;
        gr[e1].insert(e2);
        gr[e2].insert(e1);
    }
    set<int> vis;
    dfs(gr, vis, 1);
    cout << res - 1;
}
```
