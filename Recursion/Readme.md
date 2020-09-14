# Recursion - Basic Notes

Recursion is a function which calls itself. It's added up in memory as stacks and is generally used to write codes that has loops.
DP & Backtracking makes use of recusion as the fundamentals to proceed with solutions.

**Tail-Recursive** - is said when the recursive call is the last in the function. This means the parent function control need not be handled back after recursion from child.
- **Tail call elimation** is used where the recusion is replaced with **goto** and **start* keywords as modified loop.

#1. Count from N to 1 (Tail Recursive)

```cpp
void fun(int n) {
	if (n == 0) return;

	cout << n;
	fun(n - 1);
}
```

**After Tail Elimination**
```cpp
void dec(int n) {
start:
	if (n == 0) return;

	cout << n;
	n = n - 1;
	goto start;
}
```

#2. Count from 1 to N

```cpp
void fun(int n) {
	if (n == 0) return;

	fun(n - 1);
	cout << n;
}
```
**Better code (with T-Elimination)**
```cpp
void fun(int n, int k = 1) {
	if (n == 0) return;

	cout << k;
	fun(n - 1, k + 1);
}
```
