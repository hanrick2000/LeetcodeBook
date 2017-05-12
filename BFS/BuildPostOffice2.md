# [BuildPostOffice2](http://lintcode.com/en/problem/build-post-office-ii/)

## Question

Wall is 2, house is 1, and empty is 0. Find a place to build a post office so that the sum of the distance from the post office to all houses is smallest. Return that smallest distance.

## Examples

![](https://farm5.staticflickr.com/4167/34477106181_f2fb3b296e_o.jpg)

## Analysis

There are two opitons:

- Do BFS from __each house__ (It's better! Since there are usually less houses than empty there in the matrix, so the total time complexity is likely less).
- Do BFS from each empty. (normal way)
- Actually this question can be solved in a quite simple way. Just traverse the whole matrix to get a list of houses. And for each empty spot, calculate sum of distance from these houses, and pick the smallest sum. No need for BFS. But this can be slow. It's `Number of houses * Number of empty spots`. So we can just do BFS from each house and calculate the total distance to each empty spot. So we only need to do __Number of houses__ BFS.
- I was trapped in this question. I was thinking about starting from each house, and doing BFS from each house at the same time, whenever there is a node that is reached __Number of houses__ times, then we can return. But if we can do this in just one BFS, that would be a huge performance improvement.
- And what if there are some spots that cannot be reached by all houses?
- Always remember that this question asks us to calcuate the distance!!! This is the core.
- Do not mix `i, j` and `x, y`!!!
- Do not consider memory limitation in such question! Or you will be fucked up.
- __Do not forget that you can jsut define a new array to represent visited hash__. Normally we can just use the original grid because it's convenient. But for this question, we have to define a new visited hash!!! There is no need to save memory!

## Code

```java
// 有时候用电笨办法反而思路更清晰, 比如这个, 我起初想的是把Point里加上visited信息, 发现行不通, 那咋办? 直接每次重置一遍grid就行了.
// 诶, 其实空间节省没太所谓的, 尽量简化code把, 牺牲一下空间. 我本来想让所有house都共享一个points二维数组, 这样就不用每次都新建Point.
// 在Point里把信息都封装起来, 也还是不太好, 还是要restore empty的位置.

private class Point {
    public int x;
    public int y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
private int WALL = 2;
private int HOUSE = 1;
private int EMPTY = 0;
private int VISITED = 3;
private int m = 0;
private int n = 0;
private int[] dx = {0,0,-1,1};
private int[] dy = {1,-1,0,0};
private int[][] distances;
private int[][] times;
public int shortestDistance(int[][] grid) {
    // 还是做多次BFS比较靠谱
    m = grid.length;
    n = grid[0].length;
    distances = new int[m][n];
    times = new int[m][n];
    int houseCount = 0;
    // 其实还有优化空间, 可以把HOUSE和EMPTY单独拿出来作为list, 这样就不用每次都遍历全部, 不过这个问题不大
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (grid[i][j] == HOUSE) {
                updateDistanceByBFS(i, j, grid);
                houseCount++;
            }
        }
    }
    // Sort
    int min = Integer.MAX_VALUE;
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (times[i][j] == houseCount && isEmpty(i, j, grid)) {
                min = Math.min(distances[i][j], min);
            }
        }
    }
    return min == Integer.MAX_VALUE ? -1 : min;
}

private void updateDistanceByBFS(int x, int y, int[][] grid) {
    Queue<Point> queue  = new LinkedList<>();
    boolean[][] visited = new boolean[m][n];
    queue.offer(new Point(x, y));
    visited[x][y] = true;
    // bfs
    int distance = 0;
    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            Point curr = queue.poll();
            for (int j = 0; j < 4; j++) {
                x = curr.x + dx[j];
                y = curr.y + dy[j];
                if (!inBound(x, y)) {
                    continue;
                }
                if (visited[x][y]) {
                    continue;
                }
                if (isEmpty(x, y, grid)) {
                    queue.offer(new Point(x, y));
                    visited[x][y] = true;
                    times[x][y]++;
                    distances[x][y] += distance + 1;
                }
            }
        }
        distance++;
    }
    // restoreEmpty(grid); 不需要这个了, 因为bfs里可以自己建visited啊!!! 不要节约空间!
}

private boolean isEmpty(int x, int y, int[][] grid) {
    return grid[x][y] == EMPTY;
}

private boolean inBound(int x, int y) {
    return x >= 0 && y >= 0 && x < m && y < n;
}

// private void restoreEmpty(int[][] grid) {
//     for (int i = 0; i < m; i++) {
//         for (int j = 0; j < n; j++) {
//             if (grid[i][j] == VISITED) {
//                 grid[i][j] = EMPTY;
//             }
//         }
//     }
// }
```
