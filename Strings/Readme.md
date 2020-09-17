## Strings

Strings are an array of chars. 'string' datatype is used in C++. ASCII has **max value - 256 characters**, such that:

A - 65
a - 97 (+32)
.
.
and so on

#1. Check whether two strings are anagram.

Eg.
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
