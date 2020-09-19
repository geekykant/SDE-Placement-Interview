## Self Balancing Trees
- Balancing property - keys on the left are always smaller than keys on right
- Uses left & right rotation to make it balanced
- **AVL Tree and Red Black Tree** are 2 main SBT's.
- Red Black trees used more commonly. eg. Works on RBT. (Java - TreeSet & TreeMap , C++ - Map & Set)

### AVL Trees
- Maintains strict tree height
- |lh-rh| = balance factor
- balance factor <= 1

```cpp
//Bredth First Search

void levelOrderTraversal(Node *root) {
	if (root == NULL) return;

	queue<Node*> q;
	q.push(root);
	q.push(NULL);

	while (q.size() > 1) {
		Node* cur = q.front();
		q.pop();
		if (cur == NULL) {
			cout << endl;
			q.push(NULL);
			continue;
		}
		cout << (cur->key) << " ";

		if (cur->left != NULL) q.push(cur->left);
		if (cur->right != NULL) q.push(cur->right);
	}
}
```

### Red-Black Tree
- Loose & Less frequent restructuring
- Good for less insertion & deletion
- Every node is either RED or BLACK
- root is always **BLACK**
- No two consecutive REDS
- Black heigh should be same through all descended trees

#### Applications
- Maintain sorted stream of data
- implement double ended priority queue (Sets, Maps - C++)

```cpp
map<int, int> m;

m.insert({3, 50});
//wont bechanged
m.insert({3, 40});

m.insert({1, 10});
for (auto x : m)
	cout << x.first << " " << x.second << endl;
	
cout<<m[20]; //will be inserted instantly to [0]

//Ouput
//1 10
//3 50
//0

// m[3] = 99; can be used to update
// m.at(3) = 300 gets reference only when present
```	

