# Hashing - Used for search, insert and delete only

Sorting Data & Near Value data - AVL Trees & Red Black Trees (No hashing)
Prefix searching - Trie (Efficient information reTrieval data structure)

### Applications of Hashing
1. Dictionaries
2. Database indexing (Primary & Secondary indexing - implemented using B+ Trees or Hashing)
3. Cryptography
4. Caches
5. Symbol tables in compiler/interpreter
6. Router (Mac, IP address)
7. Data from database (associative array)

Direct Index/Adress Table - Normal scenario
eg: 0-5 [1,0,0,0,1,0]

*Hashing function - takes large value and does the magic to get small value to store in Hash Table.*

Best hashing function
-> should always match BIG key -> small
-> should generate from 0 to m-1
-> O(1) for integers and O(str_len) for large keys (strings)
-> should uniformly distribute large keys

**Collisions are bound to happend in hashing**. To prevent collision,
1. **Chaining** (We make a chain of colliding items)
2. **Open Addressing** (Linear probing, Quadratic probing, Double hashing) (We use the same arrary and check if position is occupied)

```
Load factor (alpha) = (no of keys to be inserted) / (no of slots in hash table) = n/m
(should be <= 1)
```

Data structure for storing chains
-> Linked list (O(l) for search, insert, delete) (NOT cache friendly)
-> Dynamic sized arrays (vectors) (cache friendly)
-> Self balancing BST (AVL Tree, Red Black Tree) - O(logl) for search, insert, delete - (NOT cache friendly)

```cpp
//Creating a custom hashmap
struct MyHash{
	int BUCKET; //size of hashmap
	list<int> *table;

	MyHash(int b){
		BUCKET = b;
		table = new list<int>[BUCKET];
	}

	//get hash of key
	int hash(int key)
		return key % BUCKET;

	void insert(int key){
		int i = hash(key);
		table[i].push_back(key);
	}

	void search(int key){
		int i = hash(key);
		for(auto x: table[i])
			if(x == hash)
				return true;
		return false;
	}

	void remove(int key){
		int i = hash(key);
		table[i].remove(key);
	}
}
```

## Open Addressing

-> No. of slots in hash table >= no. of keys to be inserted
-> Cache friendly

Linear Probing - linearly search and insert hash to the next free slot.
Clustering (cluttering in linear probing having same hash)

### Quadrating probing 
- secondary clustering formed (better than linear)
- double size of table required
- BUT disadvantages misses free slots
- Free slot missing fix  - (Alpha < 0.5 & hash table size (m) is prime number)

### Double hashing
- hash is calculated, at same time next collision shift index
- no clusters are formed
- (h1(key) + i*h2(key))%m
- h2(key) and m best if relatively prime

Expected no. of probes required = 1/(1 - alpha)

Deleted slots (-2) -> point to dummy node
Empty slots (-1) -> point to NULL
