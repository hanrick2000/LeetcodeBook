#### Question
Return binary tree level order traversal.
#### Examples
![](https://farm3.staticflickr.com/2885/33562034873_9b7d5b5e03_o.jpg)
#### Analysis
For each level, we need to know how many nodes we need.
#### Code
```java
public ArrayList<ArrayList<Integer>> levelOrder(TreeNode root) {
    ArrayList<ArrayList<Integer>> res = new ArrayList<>();
    Queue<TreeNode> queue = new LinkedList<>();
    if (root != null) {
        queue.offer(root);
    }
    while(!queue.isEmpty()) {
        int size = queue.size();
        ArrayList<Integer> temp = new ArrayList<>();
        for (int i = 0; i < size; i++) {
            TreeNode curr = queue.poll();
            temp.add(curr.val);
            if (curr.left != null) {
                queue.offer(curr.left);
            }    
            if (curr.right != null) {
                queue.offer(curr.right);
            }    
        }
        res.add(temp);
    }
    return res;
}
```