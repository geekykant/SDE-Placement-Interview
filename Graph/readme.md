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
 - Linear ordering of vertices
 - Topological sort makes sures u -> v (u comes before v) order is followed in traversal.
 - Applicable only to DAG (Directed Acyclic Graph)
 - Multiple answers possible
 - Can be used for "cycle detection" using Kahn's Algo BFS (altho not recommended)

<img width="435" alt="Screenshot 2022-04-20 at 10 44 12 AM" src="https://user-images.githubusercontent.com/27401142/164155262-04bb8405-4f0c-45e5-9890-9c3104919f10.png">

Output: 5 4 2 3 1 0 

**DFS - Topological Sort**
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

**BFS - Topological Sort** (Kahn's Algorithm)
> You can use this technique for cycle detection (cnt == N) (not recommended)
```cpp
void topoSort(vector<vector<int>>& graph, int n) {
    vector<int> indegree(n);
    queue<int> q;

    //count indegrees
    for (int i = 0; i < n; i++)
        for (auto it : graph[i])
            indegree[it]++;

    //add non-dependent (0 indegree) to queue
    for (int i = 0; i < n; i++)
        if (indegree[i] == 0)
            q.push(i);

    vector<int> res;
    while (!q.empty()) {
        int node = q.front(); q.pop();
        res.push_back(node);

        for (int neighbour : graph[node]) {
            indegree[neighbour]--;
            if (indegree[neighbour] == 0)
                q.push(neighbour);
        }
    }
    
    // printVectors(res); -> 4 5 0 2 3 1 
}
```

#### Disjoint Set - Union By Rank, Path Compression
- Can check if belongs to same component
- Two operations - findParent(), Union()
- Less rank child tree nodes are attached to higher rank node
- Time Complexity: O(4α) - close to constant time

``cpp
vector<int> parent;
vector<int> myrank;

int findParent(int node) {
    if (node == parent[node])
        return node;

    //path compression using -> parent[node]
    return parent[node] = findParent(parent[node]);
}

void setUnion(int u, int v) {
    //find parent
    u = findParent(u);
    v = findParent(v);

    //lesser rank attached to higher ones
    if (myrank[u] < myrank[v])
        parent[u] = v;
    else if (myrank[v] < myrank[u])
        parent[v] = u;
    else {
        parent[v] = u;
        myrank[u]++;
    }
}

void disjointSet(vector<vector<int>> edgeList, int n) {
    parent.resize(n + 1);
    myrank.resize(n + 1);

    for (int i = 1; i <= n; i++)
        parent[i] = i;

    for (auto edge : edgeList) {
        int u = edge[0], v = edge[1];
        setUnion(u, v);
    }

    if (findParent(2) != findParent(3))
        cout << "Different component" << endl;
    else
        cout << "Same component" << endl;

    //printVectors(parent);
    //printVectors(myrank);
}
```
