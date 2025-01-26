```c
void bfs(int starting_vertex, unordered_map<int, unordered_set<int>>& graph) {
    queue<int> q;
    unordered_set<int> visited;
    q.push(starting_vertex);
    visited.insert(starting_vertex);

    int distance = 0;

    while (!q.empty()) {
        int level_size = q.size();
        cout << "At distance " << distance << ":\n";

        for (int i = 0; i < level_size; ++i) {
            int current = q.front();
            q.pop();
            cout << current << "\n";

            for (int neighbor : graph[current]) {
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
