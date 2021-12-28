## Tree

#### Applications
- Organising structures
- HTML/JSON/XML, Folder organisation, in OOP (inheritance)
- **Binary Search Trees** - represents priority queues
- Binary Heap
- B and B+ Trees in DBMS
- Spanning and shortest path trees (used in bridges - forward packets, routers - shortest path to nodes)
- Parse trees in compilers

Application of Trees
- Trie - used to represent dicitonaries
- Suffix tree - pattern & text fast finding O(m)
- Binary index tree & Segment trees (fast) - both used for query searches in range

**Representation - CPP**
```cpp
struct Node {
	int key;
	Node *left, *right;
	Node(int k){
		key = k;
		left = right = NULL:
	}
};

int main() {
	Node *root = NULL;
	return 0;
}
```

### Tree Traversal
1. Bredth First (or level order)
2. Depth First

#### Depth First (3! = 6 Methods - 3 Popular)
- Inorder (Left -> Root -> Right) 
- Preorder (Root -> Left -> Right)
- Postorder (Left -> Right -> Root)

**Recursion*
```cpp
void inorder(Node *root) {
	if (root != NULL) {
		inorder(root->left);
		cout << (root->key) << " ";
		inorder(root->right);
	}
}

void preorder(Node *root) {
	if (root != NULL) {
		cout << (root->key) << " ";
		preorder(root->left);
		preorder(root->right);
	}
}

void postorder(Node *root) {
	if (root != NULL) {
		preorder(root->left);
		preorder(root->right);
		cout << (root->key) << " ";
	}
}
```

**Iterative Inorder**
```cpp
void iterativeInorder(Node *root) {
	stack<Node*> s;
	Node *cur = root;

	while (cur != NULL || !s.empty()) {
		while (cur != NULL) {
			s.push(cur);
			cur = cur->left;
		}

		cur = s.top(); s.pop();
		cout << cur->key << " ";
		cur = cur->right;
	}
}

OR

vector<int> inorderTraversal(TreeNode* root) {
    stack<TreeNode*> st;
    TreeNode* temp = root;
    vector<int> ans;
    while (true) {
        if (temp != NULL) {
            st.push(temp);
            temp = temp->left;
        } else {
            if (st.empty()) break;
            temp = st.top();
            st.pop();
            ans.push_back(temp->val);
            temp = temp->right;
        }
    }
    return ans;
}
```

**Iterative Preorder**
```cpp
void interativePreorder(Node *root) {
	stack<Node*> s;
	s.push(root);

	while (!s.empty()) {
		Node *cur = s.top();
		cout << cur->key << " ";
		s.pop();

		if (cur->right != NULL) s.push(cur->right);
		if (cur->left != NULL) s.push(cur->left);
	}
}
```

**Size of Binary Tree**
```cpp
int btreesize(Node *root) {
	if (root == NULL) return 0;

	return 1 + btreesize(root->left)
	       + btreesize(root->right);
}

//Better Preorder iteration
void betterPreorder(Node *root) {
	if (root == NULL) return;

	stack<Node*> s;
	Node *cur = root;

	while (cur != NULL || !s.empty()) {
		while (cur != NULL) {
			cout << cur->key << " ";
			if (cur->right != NULL)
				s.push(cur->right);
			cur = cur->left;
		}

		if (!s.empty()) {
			cur = s.top();
			s.pop();
		}
	}
}
```

#1. Maximum in binary tree
```cpp
int maxBsize(Node *root) {
	if (root == NULL) 
      return INT_MIN;

	return max(max(maxBsize(root->left), maxBsize(root->right)),
				 root->key);
}
```

#2. Height of Binary tree

```cpp
int height(Node *root) {
	if (root == NULL) 
		return 0;
	
	return 1 + max(height(root->left), height(root->right));
}
```

#3. Max Element in a tree

```cpp
int maxElement(Node *root) {
	if (root == NULL) return INT_MIN;

	return max(max(maxElement(root->left), maxElement(root->right)),
	           root->key);
}
```

## Binary Search Tree - O(H)
- smaller keys on left, larger keys on right
- all keys are distinct
- **NOT Cache Friendly**
- C++ - Map, Set, Multiset, Multimap
- Java - TreeSet, TreeMap
- Insert, Delete, Search - O(H)

**BST - Searching**
```cpp
//Recursive
bool search(Node *root, int x) {
	if (root == NULL)
		return false;

	if (root->key == x)
		return true;
	else if (x < root->key)
		return search(root->left, x);
	else
		return search(root->right, x);
}

//Iterative
bool search(Node *root, int x) {
	while (root != NULL) {
		if (root->key == x)
			return true;
		else if (x < root->key)
			root = root->left;
		else
			root = root->right;
	}

	return false;
}
```

**Inserting**
```cpp
Node* insert(Node *root, int x) {
	if (root == NULL)
		return new Node(x);
	if (root->key == x)
		return root;
	else if (x < root->key)
		root->left = insert(root->left, x);
	else if (x > root->key)
		root->right = insert(root->right, x);

	return root;
}
```

Inorder Successor - closes greater value in inorder traversal

**Deletion**
```cpp
Node* deleteNode(Node *root, int x) {
	if (root == NULL) return root;

	if (x < root->key)
		root->left = deleteNode(root->left, x);
	else if (x > root->key)
		root->right = deleteNode(root->right, x);
	else {
		if (root->left == NULL) {
			Node *temp = root->right;
			delete root;
			return temp;
		} else if (root->right == NULL) {
			Node *temp = root->left;
			delete root;
			return temp;
		}
	}
	return root;
}
```
