## Breadth First Search

Разделя възлите на посетени и непосетени. !!!

Започва да обхожда от начален връх.

Добавя всички съседи, които не са посетени.

->Намира най-къс път от даден възел до всички останали в непретеглен граф 
```c
void bfs(int starting_vertex, unordered_map<int, unordered_set<int>>& graph) {
    queue<int> q; // !!!
    unordered_set<int> visited; // !!!
    q.push(starting_vertex); // start
    visited.insert(starting_vertex); //start

    int distance = 0;

    while (!q.empty()) {
        int level_size = q.size();

        for (int i = 0; i < level_size; ++i) // visit only v of this lvl
        {
            int current = q.front();
            q.pop();

            for (int neighbor : graph[current]) // add all not visited neighbors
            { 
                if (!visited.count(neighbor)) {
                    visited.insert(neighbor);
                    q.push(neighbor);
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
