## Linked List in C++

### Single Linked List
- **`head` is the key**
- Insertion at start - O(1)
- Searching & Inserting at end - O(N)

### Circular Linked List
- **`tail` is the key**
- Insertion a beginning, end - O(1)
- Searching - O(N)
- Advantages for **[Round Robin Algorithm](https://www.geeksforgeeks.org/program-round-robin-scheduling-set-1/)**

**Basic Code**
```cpp
struct Node {
	int data;
	Node *next;
	
  Node(int x) {
		data = x;
		next = NULL;
	}
};

void printAll(Node *head) {
	while (head != NULL) {
		cout << head->data << " ";
		head = head->next;
	}
}

int main() {
	Node *head = new Node(2);
	Node *b = new Node(5);
	Node *c = new Node(3);

	head->next = b;
	b->next = c;
  
  printAll(head);
	return 0;
}
```

#1. Search for node

```cpp
int searchNode(Node *head, int x) {
	int pos = -1;
	while (head != NULL) {
		pos++;
		if (head->data == x)
			return pos;

		head = head->next;
	}

	return false;
}
```

#2. Insert node before head

```cpp
Node* insertHead(Node *head, int x) {
	Node *new_head = new Node(x);
	new_head->next = head;

	return new_head;
}
```

#3. Delete the head

```cpp
Node* deleteFirst(Node *head) {
	if (head == NULL)
		return NULL;

	Node *temp = head->next;
	delete temp;
	return temp;
}
```

#4. Insert at a given position in Linked List

#5. Insert in a sorted array

#6. Remove nth element from end

```cpp
int elementFromEnd(Node *head, int pos) {
	Node *cur = head;
	int n;

	while (cur != NULL) {
		n++;
		cur = cur->next;
	}

	if (pos > n) return -1;

	for (int i = 0; i < n - pos - 1; i++) 
		head = head->next;

	return head->data;
}
```

## Circular Linked List

```cpp
void printAll(Node *head) {
	if (head == NULL) return;

	cout << head->data << " ";
	Node *cur = head->next;

	while (cur != head) {
		cout << cur->data << " ";
		cur = cur->next;
	}
	cout << endl;
}
```


#1. Insert at Head
```cpp
Node* insertAtHead(Node *head, int x) {
	Node *temp = new Node(x);

	if (head == NULL) {
		temp->next = temp;
		return temp;
	} else {
		swap(head->data, temp->data);

		temp->next = head->next;
		head->next = temp;
		return head;
	}
}
```
