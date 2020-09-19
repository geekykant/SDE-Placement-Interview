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
