### Longest Common String
- Questions are basically to compute the longest "Substring" and "Subsequence".
- Make sure to take max of `res` when calculating for longestSubstring.

#### Common Subsequence

Recursion
```cpp
int longestSubsequence(string a, string b, int m, int n) {
	if (m == 0 || n == 0)
		return 0;

	if (a[m - 1] == b[n - 1])
		return 1 + longestSubsequence(a, b, m - 1, n - 1);

	return max(longestSubsequence(a, b, m - 1, n), longestSubsequence(a, b, m, n - 1));
}
```

Tabulation
```cpp
int longestSubsequence(string& s1, string& s2, int m, int n) {
    vector<vector<int>> dp(m + 1, vector<int>(n + 1));

    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (s1[i - 1] == s2[j - 1])
                dp[i][j] = 1 + dp[i - 1][j - 1];
            else
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
        }
    }

    return dp[m][n];
}
```

#### Common Substring

Recursion
```cpp
int res = 0;
void longestSubsequence(string& s1, string& s2, int m, int n, int count = 0) {
    if (m == 0 || n == 0) return;

    if (s1[m - 1] == s2[n - 1]) {
        res = max(res, count + 1);
        longestSubsequence(s1, s2, m - 1, n - 1, count + 1);
        return;
    }

    longestSubsequence(s1, s2, m - 1, n, 0);
    longestSubsequence(s1, s2, m, n - 1, 0);
}
```

Tabulation
```cpp
int longestSubstring(string& s1, string& s2, int m, int n) {
    vector<vector<int>> dp(m + 1, vector<int>(n + 1));
    int res = 0;

    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (s1[i - 1] == s2[j - 1]) {
                dp[i][j] = 1 + dp[i - 1][j - 1];
                res = max(res, dp[i][j]);
            }
            else
                dp[i][j] = 0;
        }
    }

    return res;
}
```
