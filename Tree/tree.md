### Traversal 
* Preorder, inorder and postorder are all using DFS. And BFS is just level order traversal, which will print nodes level by level. And it can only be implemented by iterative approach using Queue. 

#### Recursion
#### Preorder

root  
helper(root.left)  
helper(root.right)

* Inorder 

helper(root.left)  
root  
helper(root.right)  
[Question](Tree/Traversal/inorder.md)

* Postorder

helper(root.left)  
helper(root.right)  
root

#### Iterative
* Stack

Exchange the order of left and right subtree will only change the order of output. Change the order of root, left, and right will change the order category of output.

The position of `stack.push()` for children and the position of `stack.pop()` for root determine the category of traversal. 

#### Example
levelorder: 1,2,3,4,5,6,7    
inorder: 4,2,5,1,6,2,7  
preorder: 1,2,4,5,3,6,7   
postorder: 4,5,2,6,7,3,1
