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

**Search Iterator**
```cpp
class BSTIterator {
private:
    void partialInorder(TreeNode* node) {
        while (node) {
            st.push(node);
            node = node->left;
        }
    }

public:
    stack<TreeNode*> st;
    BSTIterator(TreeNode* root) {
        st.push(root);
        partialInorder(root->left);
    }

    int next() {
        TreeNode* temp = st.top(); st.pop();
        partialInorder(temp->right);
        return temp->val;
    }

    bool hasNext() {
        return !st.empty();
    }
};
```
