# N-Queens Problem

N-Queens uses **backtracking**, a general form of DFS algorithm.

The N Queen is the problem of placing N chess queens on an N×N chessboard so that no two queens attack each other.<br><br>
<img src="https://assets.leetcode.com/uploads/2018/10/12/8-queens.png">

```cpp
#define N 5

void printSolution(int board[N][N]) {
	for (int i = 0; i < N; ++i) {
		for (int j = 0; j < N; ++j)
			cout << board[i][j];
		cout << endl;
	}
}

bool isSafe(int board[N][N], int row, int col) {
	int i, j;

	//check left of one col
	for (int i = 0; i < col; i++)
		if (board[row][i])
			return false;

	//check 135 back i--,j--
	for (i = row, j = col; i >= 0 && j >= 0; i--, j--)
		if (board[i][j])
			return false;

	//bottom left diagonals i++,j--
	for (i = row, j = col; j >= 0 && i < N; i++, j--)
		if (board[i][j])
			return false;

	return true;
}

bool solveNQUtil(int board[N][N], int col) {
	if (col >= N)
		return true;

	for (int row = 0; row < N; row++) {
		if (isSafe(board, row, col)) {
			board[row][col] = 1;

			if (solveNQUtil(board, col + 1))
				return true;

			board[row][col] = 0;
		}
	}

	return false;
}

void solveNQ() {
	int board[N][N];
	memset(board, 0, sizeof(board));

	if (!solveNQUtil(board, 0)) {
		printf("Solition doesnt exist!");
		return;
	}

	printSolution(board);
}


int main() {
	solveNQ();
	return 0;
}
```

**Output**
```
10000
00010
01000
00001
00100
```
