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
  - Level order
  - [Serialization](BinaryTreeSerialization.md)
- Graph
- 2D matrix

## Notes

- For BFS, "visited" happens before adding the node into queue.
- Always remember to check if this node is valid before offering it to the queue.
- Maintain a HashSet to keep track of __visited nodes__.