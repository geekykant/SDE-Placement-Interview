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

**CPP**
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

