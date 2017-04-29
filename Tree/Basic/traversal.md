### Traversal 
Preorder, inorder and postorder are all using DFS. And BFS is just level order traversal, which will print nodes level by level. And it can only be implemented by iterative approach using Queue. 

#### Recursion
Three types of traversal:  

* [__Preorder__](BinaryTreePreorderTraversal.md): root, root.left, root.right

* [__Inorder__](BinaryTreeInorderTraversal.md): root.left, root, root.right

* [__Postorder__](BinaryTreePostorderTraversal.md): root.left, root.right, root

#### Iterative
* Stack: 
Exchange the order of left and right subtree will only change the order of output. Change the order of root, left, and right will change the order category of output.  
The position of `stack.push()` for children and the position of `stack.pop()` for root determine the category of traversal.  
Preorder: push root, pop root, push right, push left.  
Inorder: push root and left, pop root and left, push right, pop right.  
Postorder: push right and left, pop right and left, push root, pop root.  
Remeber all the nodes in stack are not empty, so we need to check if the node is empty whenever we want to push a new node into stack.

* [__Queue__](BinaryTreeBFSorderTraversal.md):
BFS order traversal that will return a single flatten list.
[__Level__](BinaryTreeLevelorderTraversal.md) order traversal that will return each level as a list. 

#### Example
levelorder: 1,2,3,4,5,6,7    
inorder: 4,2,5,1,6,2,7  
preorder: 1,2,4,5,3,6,7   
postorder: 4,5,2,6,7,3,1