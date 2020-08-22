# Dynamic Programming 

Dynamic programming is used where we have problems, which can be divided into similar sub-problems, so that their results can be re-used.

It includes recussions + memorization which can also be top-down approach. Its constructive in nature and provides optimum result in problems where **greedy algorithm** fails to provide the right solution.

## Knapsack Problem

A bag is to be filled with many items with restriction upon the max-holding capacity 'W'. Find the total profitable value that can be taken

```cpp
int wt[] = {1, 3, 4, 5};
int val[] = {1, 4, 5, 7};
int W = 7;
```

**Using Recursion**
```cpp
int knapsack(int  wt[], int val[], int W, int n) {
	if (n == 0 || W == 0)
		return 0;

	if (wt[n - 1] <= W) {
		return max(val[n - 1] + knapsack(wt, val, W - wt[n - 1], n - 1),
		           knapsack(wt, val, W, n - 1));
	}

	return knapsack(wt, val, W, n - 1);
}
```

**Recursion -> Memorization (DP)**
```cpp
int t[102][1002];

int knapsack(int  wt[], int val[], int W, int n) {
	if (n == 0 || W == 0)
		return 0;

	if (t[n][W] != -1)
		return t[n][W];

	if (wt[n - 1] <= W) {
		return t[n][W] = max(val[n - 1] + knapsack(wt, val, W - wt[n - 1], n - 1),
		                     knapsack(wt, val, W, n - 1));
	}

	return t[n][W] = knapsack(wt, val, W, n - 1);
}

int main() {
	int wt[] = {1, 3, 4, 5};
	int val[] = {1, 4, 5, 7};
	int W = 9;
	int n = sizeof(wt) / sizeof(wt[0]);

	memset(t, -1, sizeof(t));
	cout << knapsack(wt, val, W, n);

	return 0;
}
```
