## Linked List

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



