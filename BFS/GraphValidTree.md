# [GraphValidTree](http://lintcode.com/en/problem/graph-valid-tree/)

## Question

Check if the given 2D array (a graph) is a valid tree.

## Examples

![](https://farm3.staticflickr.com/2838/33723540933_f0056cb6e3_o.jpg)

## Analysis

Edge case of 2D array is the same with one dimentional array, which is `array.length == 0`. Do not forget to initialize queue if I decide to process node after offer.

## Code

```java
public boolean validTree(int n, int[][] edges) {
    // 如果node值有重复, 那估计就只有用GraphNode封装了
    Queue<Integer> queue = new LinkedList<>();
    Set<Integer> visited = new HashSet<>();
    // Check number of edges
    if (edges.length != n - 1) {
        return false;
    }
    // Initialize
    Map<Integer, Set<Integer>> graph = initializeGraph(n, edges);
    queue.offer(0);
    visited.add(0);
    while (!queue.isEmpty()) {
        int curr = queue.poll();
        for (int i : graph.get(curr)) {
            // Or use continue
            // if (visited.contains(i)) {
               // continue;
            // }
            if (!visited.contains(i)) {
                queue.offer(i);
                visited.add(i);
            }
        }
    }
    return visited.size() == n;
}
// This initialization function is such typical style!!!
private Map<Integer, Set<Integer>> initializeGraph(int n, int[][] edges) {
    // So concise and clear!
    Map<Integer, Set<Integer>> graph = new HashMap<>();
    for (int i = 0; i < n; i++) {
        graph.put(i, new HashSet<Integer>());
    }
    for (int i = 0; i < edges.length; i++) {
        int u = edges[i][0];
        int v = edges[i][1];
        graph.get(u).add(v);
        graph.get(v).add(u);
    }
    return graph;
}
```
