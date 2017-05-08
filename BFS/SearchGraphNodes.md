# [SearchGraphNodes](http://lintcode.com/en/problem/search-graph-nodes/)

## Question

Find a node that is nearest to given node and its value is target.

## Examples

![](https://farm5.staticflickr.com/4192/34374718705_c9ee929143_o.jpg)

## Analysis

Visited set is necessary. When to check target is a question. Other parts are just normal bfs on an undirected graph.

## Code

```java
public UndirectedGraphNode searchNode(Map<UndirectedGraphNode, Integer> values,UndirectedGraphNode node, int target) {
    // find nearest node, which means shortest path
    Queue<UndirectedGraphNode> queue = new LinkedList<>();
    // We must add visited set to keep track of visited nodes, otherwise
    // there will be many duplicate visits to a same node
    Set<UndirectedGraphNode> visited = new HashSet<>();
    // Queue and Map can store null value or key. But if the root node is not null, then there will be no null in neighbors.
    if (node != null) {
        if (values.get(node) == target) {
            return node;
        }
        queue.offer(node);
        visited.add(node);
    }
    //int count = 0;
    while (!queue.isEmpty()) {
        //count++;
        UndirectedGraphNode curr = queue.poll();
        // visit
        for (UndirectedGraphNode neighbor : curr.neighbors) {
            //System.out.println("current neighbor : " + neighbor.label);
            if (!visited.contains(neighbor)) {
                // 我感觉把这个移到前面去也可以, 其实就两种呗, 一种是我只要遍历到了就check是否满足退出条件, 还有种是只在弹出的时候去check退出条件.
                if (values.get(neighbor) == target) {
                    //System.out.println("number of nodes visited : " + count);
                    return neighbor;
                } else {
                    queue.offer(neighbor);
                    visited.add(neighbor);
                }
            }
        }
    }
    return null;
}
```
