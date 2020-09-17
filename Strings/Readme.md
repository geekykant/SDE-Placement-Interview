## Strings

Strings are an array of chars. 'string' datatype is used in C++. ASCII has **max value - 256 characters**, such that:

A - 65 \
a - 97 (+32) \
. \
. \
and so on.

### Pre-processing algorithms
1. Robin Karp - O((n-m+1)xm) (**Compares hash of each window**)
2. KMP - O(n) (**Reduces redundancy and searches only extra ends**)

**KMP**
- Computes longest Proper Prefix/Suffics 
- It creates lps[] = if longest prefix = longest suffix

```
A B A B
0 0 1 2

A A A A
0 1 2 3
```

Suffix Tree - A [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) of all suffixes in basic form. 
- O(m) in worst case.
- Better for fixed text (eg. Bhagavad geetha, Shakespeare's novel)


#1. Check whether two strings are anagram.

```
string a = "aabacc";
string b = "ccabaa";

Output: True
```

**Code**
```cpp
bool isAnagram(string a, string b) {
	int count[256] = {0};

	if (a.length() != b.length())
		return false;

	for (int i = 0; i < a.length(); i++)
		count[a[i]]++;

	for (int i = 0; i < b.length(); i++)
		count[b[i]]--;

	for (int i = 0; i < 256; i++)
		if (count[i] != 0)
			return false;

	return true;
}
```


