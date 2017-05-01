# NumberofIslands

## Question

0 represents sea, and 1 represents island. Find number of islands in a 2d matrix.

## Examples

![](https://farm5.staticflickr.com/4155/33976473290_44250b7840_o.jpg)

## Analysis

Most typical BFS question. Key points are, first, make sure to remove state after visiting one node, to avoid cycle. Second, the next element in queue is a valid element which contains all information we need. In this question, the BFS algorithm is used to traverse and mark all valid nodes.

## Code

```java
private class Point {
    int x;
    int y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
public int numIslands(boolean[][] grid) {
    int count = 0;
    for (int i = 0; i < grid.length; i++) {
        for (int j = 0; j < grid[0].length; j++) {
            // Traverse every node
            if (grid[i][j]) {
                bfs(grid, i, j);
                count++;
            }
        }
    }
    return count;
}

// Separate bfs method from main method
private void bfs(boolean[][] grid, int i, int j) {
    Queue<Point> queue = new LinkedList<>();
    int[] dx = {1,0,-1,0};
    int[] dy = {0,1,0,-1};
    // Mark starting node
    queue.offer(new Point(i, j));
    grid[i][j] = false;

    // bfs
    while (!queue.isEmpty()) {
        Point curr = queue.poll();
        //grid[x][y] = false; // 这个速度快, 不过应该跟测试集有关系, 这个理论上应该更慢
        for (int k = 0; k < 4; k++) {
            int x = curr.x + dx[k];
            int y = curr.y + dy[k];
            if (!inBound(grid, x, y)) {
                continue;
            }
            // Only add valid point!!!
            if (grid[x][y]) {
                queue.offer(new Point(x, y));
                grid[x][y] = false; // 应该是visit之后就抹除比较合理, 不然会产生重复
            }
        }
    }
}
// 好吧, 其实这个思路更好, 因为更加清晰, 拆分方法, 而其实速度是差不多的
private boolean inBound(boolean[][] grid, int x, int y) {
    if (x >= grid.length || x < 0) {
        return false;
    }
    if (y >= grid[0].length || y < 0) {
        return false;
    }
    return true;
}
```

My own solution:

```java
private class Point {
    int x;
    int y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
public int numIslands(boolean[][] grid) {
    Queue<Point> queue = new LinkedList<>();
    int count = 0;
    for (int i = 0; i < grid.length; i++) {
        for (int j = 0; j < grid[0].length; j++) {
            if (grid[i][j]) {
                queue.offer(new Point(i, j));
                grid[i][j] = false;
                count++;
            }
            while (!queue.isEmpty()) {
                Point curr = queue.poll();
                int x = curr.x;
                int y = curr.y;
                //grid[x][y] = false; // 这个速度快, 不过应该跟测试集有关系, 这个理论上应该更慢
                if (x + 1 < grid.length && grid[x + 1][y]) {
                    queue.offer(new Point(x + 1, y));
                    grid[x + 1][y] = false; // 应该是这个比较合理, 不然会产生重复
                }
                if (y + 1 < grid[0].length && grid[x][y + 1]) {
                    queue.offer(new Point(x, y + 1));
                    grid[x][y + 1] = false;
                }
                if (x - 1 >= 0 && grid[x - 1][y]) {
                    queue.offer(new Point(x - 1, y));
                    grid[x - 1][y] = false;
                }
                if (y - 1 >= 0 && grid[x][y - 1]) {
                    queue.offer(new Point(x, y - 1));
                    grid[x][y - 1] = false;
                }
            }
        }
    }
    return count;
}
```