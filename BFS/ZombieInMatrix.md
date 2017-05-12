# [ZombieInMatrix](http://lintcode.com/en/problem/zombie-in-matrix/)

## Question

Wall is 2, zombie is 1, and people is 0. Zombies can turn nearest people (four directions) into zombies every day. How long it would take to turn all people into zombies? Zombies cannot go through wall.

Return -1 if zombies cannot get all people.

## Examples

![](https://farm5.staticflickr.com/4155/33763984194_f6163751d2_o.jpg)

## Analysis

Actually this question can be interpreted as: __Do a BFS level order on every zombie in every day__. So we need to traverse the whole graph starting from each zombie, and return the time to get all people.

So __each zombie is similar to each root node in topological sorting__.

Use m, n to simplify `grid.length and grid[0].length`.

## Code

```java
private class Point {
    public int x;
    public int y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
private int WALL = 2;
private int ZOMBIE = 1;
private int PEOPLE = 0;
private int[] dx = {0,0,1,-1};
private int[] dy = {1,-1,0,0};
private int m = 0;
private int n = 0;
public int zombie(int[][] grid) {
    Queue<Point> queue = new LinkedList<>();
    // 从每个zombie出发都用bfs level order
    // find all zombies
    m = grid.length;
    n = grid[0].length;
    int wallCount = 0;
    int zombieCount = 0;
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (grid[i][j] == ZOMBIE) {
                queue.offer(new Point(i, j));
                zombieCount++;
            } else if (grid[i][j] == WALL) {
                wallCount++;
            }
        }
    }
    // bfs
    int time = 0;
    int totalCount = m * n;
    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            Point curr = queue.poll();
            for (int j = 0; j < 4; j++) {
                int x = curr.x + dx[j];
                int y = curr.y + dy[j];
                if (inBound(x, y, grid) && grid[x][y] == PEOPLE) {
                    grid[x][y] = ZOMBIE;
                    queue.offer(new Point(x, y));
                    zombieCount++;
                }
            }
        }
        // process after level order
        time++;
        // it would be better that to use peopleCount-- until 0
        if (zombieCount + wallCount == totalCount) {
            return time;
        }
    }
    return -1;
}
// quite clear! I like it!
private boolean inBound(int x, int y, int[][] grid) {
    return x >= 0 && y >= 0 && x < m && y < n;
}
```
