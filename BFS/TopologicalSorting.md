# [TopologicalSorting](http://lintcode.com/en/problem/topological-sorting/)

## Question

Return any one of topological sorting based on the given graph.

## Examples

![](https://farm5.staticflickr.com/4170/34419708281_c181abc867_o.jpg)

## Analysis

How to keep persistent information about a node, is the key problem. Directed graph also could have loops. You have to know in degree and out degree concepts. In degree means number of edges going into a node. Out degree means number of edges going out of a node. This question only uses in degree.

Use the thought of dividing big questions into several small parts (methods).

## Code

```java
// 其实就是按照入度从小到大排列, 因为入度小的排在前面, 这样肯定不会被反过来.
public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
    if (graph == null) {
        return new ArrayList<DirectedGraphNode>();
    }
    // Get degrees
    Map<DirectedGraphNode, Integer> map = getDegrees(graph);
    // Add root nodes
    Queue<DirectedGraphNode> queue = new LinkedList<>();
    ArrayList<DirectedGraphNode> res = new ArrayList<>();
    for (DirectedGraphNode node : graph) {
        if (!map.containsKey(node)) {
            queue.offer(node);
            res.add(node);
        }
    }
    // bfs
    while (!queue.isEmpty()) {
        DirectedGraphNode curr = queue.poll();
        for (DirectedGraphNode neighbor : curr.neighbors) {
            map.put(neighbor, map.get(neighbor) - 1);
            if (map.get(neighbor) == 0) {
                queue.offer(neighbor);
                res.add(neighbor);
            }
        }
    }
    return res;
}

private Map<DirectedGraphNode, Integer> getDegrees(ArrayList<DirectedGraphNode> graph) {
    Map<DirectedGraphNode, Integer> map = new HashMap<>();
    for (DirectedGraphNode node : graph) {
        for (DirectedGraphNode neighbor : node.neighbors) {
            if (map.containsKey(neighbor)) {
                map.put(neighbor, map.get(neighbor) + 1);
            } else {
                map.put(neighbor, 1);
            }
        }
    }
    return map;
}
```