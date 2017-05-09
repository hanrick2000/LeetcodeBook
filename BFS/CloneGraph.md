# [CloneGraph](http://lintcode.com/en/problem/clone-graph/)

## Question

Deep copy a graph.

## Examples

![](https://farm3.staticflickr.com/2859/33701776454_35c4d0c8ea_o.jpg)

## Analysis

Maintain a hashmap to keep relationship between original graph and copied graph. Just think about copying elements from one array to anothr new array. We need to traverse original array, and copy elements according to their indexes. So it's quite similar here. We just need to traverse the original graph and copy it to another graph based on a hashmap.

The true reason that why we need __"visited"__ set is we must ensure every node is offered into the queue for only once! This is true for all kinds of nodes, including those who has itself as neighbor. (self cycle)

## Code

```java
public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
    // edge
    if (node == null) {
        return null;
    }
    //System.out.println("size: " + (node.neighbors.get(0) == node.neighbors.get(1)));
    UndirectedGraphNode root = new UndirectedGraphNode(node.label);
    Map<UndirectedGraphNode, UndirectedGraphNode> map = new HashMap<>();
    Queue<UndirectedGraphNode> queue = new LinkedList<>();
    Set<UndirectedGraphNode> visited = new HashSet<>();
    // Initializa graph nodes
    // 可以单独做个遍历建立graph, 但是太麻烦了, 不值得
    // 然而其实没有那么复杂, 反而更清晰, 只是多了一个arraylist而已
    // 这样写不好!!! 还是应该用下面的better solution, 能分开做的任务一定不要合在一起, 这在工业界工作也是这样, 尽量拆分大任务.
    // 尽管这个题会多生成一个arraylist, 但是其实没太所谓的???
    // bfs
    queue.offer(node);
    visited.add(node);
    map.put(node, root);
    while (!queue.isEmpty()) {
        UndirectedGraphNode curr = queue.poll();
        UndirectedGraphNode currCopy = map.get(curr);
        for (UndirectedGraphNode neighbor : curr.neighbors) {
            if (!visited.contains(neighbor)) {
                queue.offer(neighbor);
            }
            if (map.get(neighbor) == null) {
                map.put(neighbor, new UndirectedGraphNode(neighbor.label));
            }
            currCopy.neighbors.add(map.get(neighbor));
            visited.add(neighbor);
        }
        // visited.add(neighbor), this is wrong! some nodes will be offered into the queue
        // for more than once!
    }
    return root;
}
```

Better solution:

```java
TODO
```