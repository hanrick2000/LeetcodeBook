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
  - Process node after poll or after offer (it depends ?).
  - Question list
    - [Level order](LevelOrderTraversal.md)
    - [BinaryTreeSerialization](BinaryTreeSerialization.md)
- Graph
  - Use "visited" set to avoid loops.
  - Build [all graph nodes first](CloneGraph.md) and store them into a list, and then it's easier to process.
  - Use `Map<Integer, Set<Integer>>` or graph node (can we use graphnode ?) to store a graph.
  - Question list
    - [SearchGraphNodes](SearchGraphNodes.md)
    - [GraphValidTree](GraphValidTree.md)
    - [CloneGraph](CloneGraph.md)
- 2D matrix

## Notes

- For BFS, the "visited" set must ensure that every node will only be offered into the queue for once!!!
- Always remember to check if this node is valid before offering it to the queue.
- Maintain a HashSet to keep track of __visited nodes__.