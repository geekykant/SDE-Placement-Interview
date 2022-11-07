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

**Level Order Traversal (BFS)**
```
     1
  2    3
4  5  6 7

Ouput: [[1],[2,3],[4,5,6,7]]
```

```cpp
vector<int> getLevelOrder(BinaryTreeNode<int> *root) {
    vector<int> ans;
    if (root == NULL) return ans;
    
    queue<BinaryTreeNode<int>*> q;
    q.push(root);
    
    while (!q.empty()) {
        BinaryTreeNode<int>* temp = q.front();
        q.pop();
        ans.push_back(temp->val);
        if (temp->left) q.push(temp->left);
        if (temp->right) q.push(temp->right);
    }
    return ans;
}
```

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
vector<int> iterativePreorder(TreeNode* root) {
    vector<int> res;
    if(!root) return res;
    stack<TreeNode*> st;
    st.push(root);
    while(!st.empty()){
        root = st.top(); st.pop();
        res.push_back(root->val);

        if(root->right) st.push(root->right);
        if(root->left) st.push(root->left);
    }
    return res;
}
```

**Iterative Postorder**
```cpp
//Using 2 stacks
vector<int> postorderTraversal(TreeNode* root) {
    vector<int> ans;
    if (root == NULL) return ans;
    stack<TreeNode*> st1, st2;
    st1.push(root);

    while (!st1.empty()) {
        TreeNode* temp = st1.top();
        st1.pop();
        st2.push(temp);
        if (temp->left) st1.push(temp->left);
        if (temp->right) st1.push(temp->right);
    }

    while (!st2.empty()) {
        ans.push_back(st2.top() -> val);
        st2.pop();
    }
    return ans;
}

OR

// Using 1 stack
vector<int> postorderTraversal(TreeNode* root) {
    vector<int>ans;
    if (root == NULL) return ans;

    stack<TreeNode*> st;
    TreeNode* cur = root;

    while (cur != NULL || !st.empty()) {
        if (cur != NULL) {
            st.push(cur);
            cur = cur->left;
        } else {
            TreeNode* temp = st.top()->right;
            if (temp == NULL) {
                temp = st.top();
                st.pop();
                ans.push_back(temp->val);
                while (!st.empty() && temp == st.top() -> right) {
                    temp = st.top(); st.pop();
                    ans.push_back(temp->val);
                }
            } else {
                cur = temp;
            }
        }
    }
    return ans;
}
```

**All in One Traversal**
```cpp
vector<int> allInOneTraversal(TreeNode* root) {
    stack<pair<TreeNode*, int>> st;
    st.push({root, 1});
    vector<int> pre, in, post;
    
    while(!st.empty()){
        auto it = st.top();
        st.pop();

        // pre order
        // increment++ (1 -> 2)
        // check left and push
        if(it.second == 1){
            pre.push_back(it.first->val);
            it.second++;
            st.push(it);
            if(it.first->left)
                st.push({it.first->left, 1});
        }
        // in order
        // increment++ (2 -> 3)
        // check left and push
        else if(it.second == 2){
            in.push_back(it.first->val);
            it.second++;
            st.push(it);
            if(it.first->right)
                st.push({it.first->right, 1});
        }
        // post order
        else {
            post.push_back(it.first->val);
        }
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
