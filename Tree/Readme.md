### General solution methods
- Recursion
	> Both of following methods are __DFS__. So they both have such sentences like helper(root.left, …), helper(root.right, …).

- Divide and conquer

	Put results as __return values__.
	> I would prefer this method than traverse, since this method is easier to organize a solution. We would already have all those information we need when we are backtracking. But traverse is like a blind search. The key point is to deal with __leaf nodes or nodes with one null child and how to simplify their logic (four conditions)__. __Three values__ in ResultType is most. __Definition__ in ResultType is important.

- Traverse

	Put results as __parameters__. 
	> Sometimes we may add __global variables__. We need global variables if we need to break when we find some node or value, which means we don’t need to check every value in the traverse.

- Non recursion

	Use stack or queue.
### Concepts
- Height and depth
### Category
* [Traversal][1]
### Hard for myself
- Tricky question for path sum! [PathSum2][3]
### Experience
- Don’t use else if when using traverse method! [LowestCommonAncestor2][2]
- Start analysis from examples first!!! Don't start to write code unless you are confident.
- We can pass parent node information to child node!

[1]:	Traversal/traversal.md
[2]:	http://lintcode.com/en/problem/lowest-common-ancestor-ii/
[3]:	http://lintcode.com/en/problem/binary-tree-path-sum-ii/