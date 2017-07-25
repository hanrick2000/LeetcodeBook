# [KnightShortestPath](http://lintcode.com/en/problem/knight-shortest-path/)

## Question

See the below.

## Examples

![](https://farm5.staticflickr.com/4158/33796344743_afacfcaaaf_o.jpg)
![](https://farm5.staticflickr.com/4188/33796349373_611c843a9f_o.jpg)

## Analysis

This is a so typical BFS on matrix!

- Define global variables.
- __Increment path__ after level order.
- __Be clear about__ when to process variables.
  - Process root node.
  - Process node along with `queue.offer()`.

## Code

```java
private boolean EMPTY = false;
private boolean BARRIER = true;
private int[] dx = {1, 1, -1, -1, 2, 2, -2, -2};
private int[] dy = {2, -2, 2, -2, 1, -1, 1, -1};
public int shortestPath(boolean[][] grid, Point source, Point destination) {
    // 象棋里的马
    Queue<Point> queue = new LinkedList<>();
    queue.offer(source);
    // grid其实就是visited数组
    grid[source.x][source.y] = BARRIER;
    int path = 0;
    while (!queue.isEmpty()) {
        // 求最短路径, 肯定就是level order了
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            Point curr = queue.poll();
            for (int j = 0; j < 8; j++) {
                int x = curr.x + dx[j];
                int y = curr.y + dy[j];
                if (destination.x == x && destination.y == y) {
                    path++;
                    return path;
                }
                if (inBound(x, y, grid) && grid[x][y] == EMPTY) {
                    grid[x][y] = BARRIER; //设置visited
                    queue.offer(new Point(x, y));
                }
            }
        }
        path++; // important! Only increment this after level order!
    }
    return -1;
}

private boolean inBound(int x, int y, boolean[][] grid) {
    return x >= 0 && y >= 0 && x < grid.length && y < grid[0].length;
}
```