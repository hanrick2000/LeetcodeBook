#### Question
Given a tree node, return a list of int values which represent the inorder traversal. 

#### Examples
Given 1,2,3,4,5,6,7 return 4,2,5,1,6,3,7

#### Solution
Using recursion is the simplest solution, but may need more `stack space`. 

#### Analysis
Time: O(n)  
Space: O(1)

#### Code

* Recursion

```python
def greet(name):
    print 'Hello', name
greet('Jack')
greet('Jill')
greet('Bob')
```

* Iterative

```java
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    Stack<TreeNode> stack = new Stack<>();
    // 这一小段代码可以和下面的合在一起
    if (root != null) {
        stack.push(root);
        root = root.left;
    }
    // 必须要加root != null条件, 因为最后回溯到root pop掉, stack就为空了
    // 如果不加, 那么这里遍历到1就停止了, 因为stack为空了
    while (root != null || !stack.isEmpty()) {
        // 先去找到最左边的点, 同时往栈里存储top-down的节点顺序
        // 始终坚守一个准则, stack里只存not null的节点
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
        root = stack.pop();
        // 依旧是Inorder
        res.add(root.val);
        // 最后右边
        root = root.right;
    }
    return res;
}
```
