#### Question
Given a tree node, return a list of int values which represent the preorder traversal. 

#### Examples
Given 1,2,3,4,5,6,7 return 1,2,4,5,3,6,7

#### Solution
Using recursion is the simplest solution, but may need more `stack space`. 

#### Analysis
Time: O(n)  
Space: O(1)

#### Code

* Recursion

```java
public static List<Integer> preorder(TreeNode root){
    List<Integer> res = new ArrayList<>();
    helper(res, root);
    return res;
}

public static void helper(List<Integer> res, TreeNode root) {
    if (root == null) {
        return;
    }
    res.add(root.val);
    helper(res, root.left);
    helper(res, root.right);
}
```

* Iterative

```java
public static List<Integer> preorder(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    Stack<TreeNode> stack = new Stack<>();
    if (root != null) {
        stack.push(root);
    }
    while (!stack.isEmpty()) {
        root = stack.pop();
        res.add(root.val);
        // 因为向下找的时候就需要记录了, 所以直接pop就行了, 这比中序和后序都简单. 
        // 先加右边的, 因为先进后出, 所以左边的先出
        if (root.right != null) {
            stack.push(root.right);
        }
        if (root.left != null) {
            stack.push(root.left);
        }
    }
    return res;
}
```
