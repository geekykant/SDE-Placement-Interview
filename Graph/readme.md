## Graph Theory

- Very important concept, specially for visualized problems
- **DFS and BFS** are main traversal methods.

(Playlist link: https://www.youtube.com/playlist?list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw)

#### Graph Representation
- (Adjacency) Matrix
- Edge List (u,v)
- Adjacency List (mostly used)

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

#### Topological Sort
 - Topological sort makes sures u -> v (u comes before v) order is followed in traversal.
 - Applicable only to DAG (Directed Acyclic Graph)
 - Multiple answers possible

<img width="435" alt="Screenshot 2022-04-20 at 10 44 12 AM" src="https://user-images.githubusercontent.com/27401142/164155262-04bb8405-4f0c-45e5-9890-9c3104919f10.png">

Output: 5 4 2 3 1 0 

```cpp
stack<int> st; //stack makes sure LIFO order (u,v)

void topoSort(vector<vector<int>>& graph, vector<int>& visited, int start) {
    visited[start] = 1;

    for (int& neighbour : graph[start])
        if (visited[neighbour] == 0)
            topoSort(graph, visited, neighbour);

    st.push(start);
}
int driver(vector<vector<int>>& graph, vector<int>& visited, int n) {
    ...
    for (int i = 0; i < n; i++)
        if (visited[i] == 0)
            topoSort(graph, visited, i);

    vector<int> res;
    while (!st.empty()) {
        res.push_back(st.top());
        st.pop();
    }
    // printVectors(res); -> 5 4 2 3 1 0 
}

```
