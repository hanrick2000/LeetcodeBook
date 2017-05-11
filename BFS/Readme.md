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
  - Process node after poll or after offer (__it depends ?__).
  - Question list
    - [Level order](LevelOrderTraversal.md)
    - [BinaryTreeSerialization](BinaryTreeSerialization.md)
- Graph
  - Use "visited" set to avoid loops, no matter the graph is directed or undirected.
  - Build [all graph nodes first](CloneGraph.md) and store them into a list, and then it's easier to process.
  - Use `Map<Integer, Set<Integer>>` or graph node (__can we use graphnode ?__) to store a graph.
  - Question list
    - [SearchGraphNodes](SearchGraphNodes.md) ![star3][star3]
    - [GraphValidTree](GraphValidTree.md) ![recommended][recommended]
    - [CloneGraph](CloneGraph.md) ![must-have][must-have]
    - [TopologicalSorting](TopologicalSorting.md) ![must-have][must-have]
    - [CourseSchedule](CourseSchedule.md) ![star5][star5]
    - [CourseSchedule2](CourseSchedule2.md) ![star2][star2]
    - [SequenceReconstruction][SequenceReconstruction.md] ![must-have][must-have]![star5][star5]
- 2D matrix

## Notes

- Maintain a set to keep track of __visited nodes__.
- For BFS, the "visited" set must ensure that every node will only be offered into the queue for once!!!
- [Divide a complicated question into several parts](CloneGraph.md), and write them as separate methods. Because during interview, we might not have enought time to implement every detail, so we need to implement most significant methods first.
- Remember to check if this node is valid before offering it to the queue.
- Remember to initializa root node.

[must-have]: https://jaywcjlove.github.io/sb/ico/min-bibei.svg
[recommended]: https://jaywcjlove.github.io/sb/ico/min-tuijian.svg
[star]: https://jaywcjlove.github.io/sb/star/red.svg
[star0]: https://jaywcjlove.github.io/sb/star/red0.svg
[star1]: https://jaywcjlove.github.io/sb/star/red1.svg
[star2]: https://jaywcjlove.github.io/sb/star/red2.svg
[star3]: https://jaywcjlove.github.io/sb/star/red3.svg
[star4]: https://jaywcjlove.github.io/sb/star/red4.svg
[star5]: https://jaywcjlove.github.io/sb/star/red5.svg