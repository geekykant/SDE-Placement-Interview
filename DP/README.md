# Dynamic Programming 

Dynamic programming is used where we have problems, which can be divided into similar sub-problems, so that their results can be re-used.

It includes recussions + memorization which can also be top-down approach. Its constructive in nature and provides optimum result in problems where **greedy algorithm** fails to provide the right solution.

YT Playlist: https://www.youtube.com/playlist?list=PL_z_8CaSLPWekqhdCPmFohncHwz8TY2Go

## Knapsack Problem

A bag is to be filled with many items with restriction upon the max-holding capacity 'W'. Find the total profitable value that can be taken

```cpp
int wt[] = {1, 3, 4, 5};
int val[] = {1, 4, 5, 7};
int W = 7;
```

**Using Recursion - Top Down Approach**
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

**Tabulation - Bottom Up (Final Code)**
```cpp
int knapsack(int  wt[], int val[], int W, int n) {
	int t[n + 1][W + 1];
	memset(t, -1, sizeof(t));

	for (int i = 0; i < n; ++i)
		for (int j = 0; j < W; ++j)
			if (i == 0 || j == 0) {
				t[i][j] = 0;
			}

	for (int i = 1; i < n + 1; ++i) {
		for (int j = 1; j < W + 1; ++j) {
			if (t[i][j] <= j)
				t[i][j] = val[i - 1] + t[i - 1][j - wt[i - 1]];
			else
				t[i][j] = t[i - 1][j];
		}
	}

	return t[n][W];
}
```
