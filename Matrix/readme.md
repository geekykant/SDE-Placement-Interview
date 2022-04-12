#### Matrix

- Move Across 8-pointer direction
```cpp
void moveAcrossMatrix(vector<vector<int>>& board) {
    int d[][2] = {{ -1, -1}, { -1, 0}, { -1, 1}, {0, -1}, {0, 1}, {1, -1}, {1, 0}, {1, 1}};
    
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            // 8 directions
            for (int k = 0; k < 8; k++) {
                int x = i + d[k][0], y = j + d[k][1];
                if (x < 0 || x >= m || y < 0 || y >= n)
                    continue;
                ...
            }
        }
    }
}
```
