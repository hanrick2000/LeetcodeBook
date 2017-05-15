# [NQueens](http://www.lintcode.com/en/problem/n-queens/#)

## Question



## Examples

![](https://farm5.staticflickr.com/4174/34542673661_4ba2621096_o.jpg)

## Analysis

There must be some queens at the edge. This question is actually not hard. And it's quite straightforward!

**Learn the standard answer**. There is a lot to learn.

## Code

```java
// 还是代码功力不够深啊, 很多地方可以合并简化的, 尤其是二维数组表示, 这个有点失败, 我一直想着把所有信息都存下来, 其实没太有必要.
// 而且我这代码太难懂了.
private char QUEEN = 'Q';
private char EMPTY = '.';
ArrayList<ArrayList<String>> solveNQueens(int n) {
    ArrayList<ArrayList<String>> res = new ArrayList<>();
    // init
    char[][] buffer = new char[n][n];
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            buffer[i][j] = EMPTY;
        }
    }
    // dfs
    int[] visited = new int[n];
    dfs(res, buffer, n, visited, 0);
    return res;
}
// n -> number of queens to be placed
private void dfs(ArrayList<ArrayList<String>> res, char[][] buffer, int n, int[] visited, int level) {
    // exit
    if (n == 0) {
        res.add(convertToList(buffer));
        return;
    }
    // next
    for (int i = 0; i < buffer.length; i++) {
        if (visited[i] == 1) {
            continue;
        }
        if (!isValid(buffer, i, level)) {
            continue;
        }
        buffer[level][i] = QUEEN;
        visited[i] = 1;
        dfs(res, buffer, n - 1, visited, level + 1);
        buffer[level][i] = EMPTY;
        visited[i] = 0;
    }
}

private ArrayList<String> convertToList(char[][] buffer) {
    ArrayList<String> res = new ArrayList<>();
    for (int i = 0; i < buffer.length; i++) {
        StringBuilder sb = new StringBuilder();
        for (int j = 0; j < buffer[0].length; j++) {
            sb.append(buffer[i][j]);
        }
        res.add(sb.toString());
    }
    return res;
}

private boolean isValid(char[][] buffer, int column, int level) {
    int leftIndex = column;
    int rightIndex = column;
    for (int i = level - 1; i >= 0; i--) {
        leftIndex--;
        if (leftIndex >= 0 && buffer[i][leftIndex] == QUEEN) {
            return false;
        }
        rightIndex++;
        if (rightIndex < buffer.length && buffer[i][rightIndex] == QUEEN) {
            return false;
        }
    }
    return true;
}
```