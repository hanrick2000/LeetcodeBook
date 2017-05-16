# [NQueens2](http://www.lintcode.com/en/problem/n-queens-ii/)

## Question

Return number of distinct solutions of N-Queens problem.

## Examples

For n = 4, return 2.

## Analysis

Easier than NQueens. But visited array can be optimized as one dimensional array.

## Code

```java
public int totalNQueens(int n) {
    int[][] visited = new int[n][n];
    int total = dfs(n, visited, 0);
    return total;
}

private int dfs(int n, int[][] visited, int row) {
    // exit
    // 必须是n, 说明n - 1最后一行是通过了的
    // row就是指number of queens placed up to last level
    if (row == n) {
        return 1;
    }
    // next
    int total = 0;
    for (int i = 0; i < n; i++) {
        if(isValid(i, row, visited)) {
            visited[row][i] = 1;
            total += dfs(n, visited, row + 1);
            visited[row][i] = 0;
        }
    }
    return total;
}

private boolean isValid(int col, int row, int[][] visited) {
    // same col
    int leftCol = col - 1, rightCol = col + 1;
    for (int i = row - 1; i >= 0; i--) {
        if (visited[i][col] == 1) {
            return false;
        }
        if (leftCol >= 0 && visited[i][leftCol--] == 1) {
            return false;
        }
        if (rightCol < visited.length && visited[i][rightCol++] == 1) {
            return false;
        }
    }
    return true;
}
```