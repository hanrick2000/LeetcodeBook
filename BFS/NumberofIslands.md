#### Question
0 represents sea, and 1 represents island. Find number of islands in a 2d matrix.
#### Examples
![](https://farm5.staticflickr.com/4155/33976473290_44250b7840_o.jpg)
#### Analysis
Most typical BFS question. Key points are, first, make sure to remove state after visiting one node, to avoid cycle. Second, the next element in queue is a valid element which contains all information we need.
#### Code
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