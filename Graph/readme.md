## Graph Theory

- Very important concept, specially for visualized problems
- DFS and BFS are main traversal methods here

**DFS**
```cpp
set<int> visited;
bool dfs(map<int, vector<int>>& graph, int source, int dest) {
	if (source == dest)
		return true;
	if (visited.count(source))
		return false;
	visited.insert(source);

	for (int neighbour : graph[source]) {
		if (dfs(graph, neighbour, dest))
			return true;
	}
	return false;
}
```

**BFS**
```cpp
bool bfs(int n, vector<vector<int>>& edges, int source, int dest) {
	set<int> visited;
	queue<int> q;
	q.push(source);
	visited.insert(source);

	while (!q.empty()) {
		int cur = q.front(); q.pop();
		if (cur == dest)
			return true;
		for (int neighbour : graph[cur]) {
			if (visited.count(neighbour)) continue;
			visited.insert(neighbour);
			q.push(neighbour);
		}
	}
	return false;
}
```

**Union Find**
```cpp
vector<int> parent;
int findParent(int node) {
	if (parent[node] == node)
		return node;
	return parent[node] = findParent(parent[node]);
}

void makeGraph(int a, int b) {
	int pa = findParent(a);
	int pb = findParent(b);
	parent[pa] = pb;
}

bool validPath(int n, vector<vector<int>>& edges, int source, int dest) {
	if (source == dest) return true;

	parent.resize(n);

	//to initialize parent to itself
	for (int i = 0; i < n; i++)
		parent[i] = i;

	for (auto& edge : edges)
		makeGraph(edge[0], edge[1]);

	return findParent(source) == findParent(dest);
}
```
