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
