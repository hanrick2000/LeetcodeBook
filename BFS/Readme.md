# Overview

## When to use BFS

- Traversal
  - Level order traversal
  - Connected components
  - Topological sorting
- Shortest path
  - Simple graph (no direction, weight is 1)

## Category

- Binary tree
  - Process node after poll or after offer ?.
  - Question list
    - [Level order](LevelOrderTraversal.md)
    - [BinaryTreeSerialization](BinaryTreeSerialization.md)
- Graph
  - Use "visited" set to avoid loops.
  - Use `Map<Integer, Set<Integer>>` or graph node (?) to store a graph.
  - Question list
    - [SearchGraphNodes](SearchGraphNodes.md)
- 2D matrix

## Notes

- For BFS, "visited" happens before adding the node into queue.
- Always remember to check if this node is valid before offering it to the queue.
- Maintain a HashSet to keep track of __visited nodes__.