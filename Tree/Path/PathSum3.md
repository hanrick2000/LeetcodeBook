#### Question
Given a binary tree, find all of its path sum. The path could start and end at any node.
#### Examples
![](https://farm5.staticflickr.com/4182/33972709320_a4ce4fd95a_o.jpg)
#### Analysis
It's so hard. First we need to consider about using parent to traverse the whole tree to find all paths. Second we need to pass parent node information to child to avoid cycle.
#### Code
```java
public List<List<Integer>> binaryTreePathSum3(ParentTreeNode root, int target) {
    List<List<Integer>> res = new ArrayList<>();
    traverse(root, res, target);
    return res;
}
    
private void traverse(ParentTreeNode root, List<List<Integer>> res, int target) {
    if (root == null) {
        return;
    }
    
    helper(root, null, res, new ArrayList<Integer>(), target);
    traverse(root.left, res, target);
    traverse(root.right, res, target);
}

private void helper(ParentTreeNode root, ParentTreeNode father, List<List<Integer>> res, List<Integer> buffer, int target) {
    if (root == null) {
        return;
    }
    
    buffer.add(root.val);
    if (target == root.val) {
        res.add(new ArrayList<>(buffer));
    }
    // 这个father的策略主要针对于整棵树的root, 因为需要跨越
    if (root.parent != father) {
        helper(root.parent, root, res, buffer, target - root.val);
    }
    if (root.left != father) {
        helper(root.left, root, res, buffer, target - root.val);
    }
    if (root.right != father) {
        helper(root.right, root, res, buffer, target - root.val);
    }
    buffer.remove(buffer.size() - 1); 
}
```

False example:
```java
public List<List<Integer>> binaryTreePathSum3(ParentTreeNode root, int target) {
        // 这个题2,4和4,2怎么出来的? 估计认为可以通过PathSum2的方法弄出来
        // 那如何解释2,1,3, 显然找出精确的path是不可能用divide and conquer了, 因为
        // 求最大值是可以聚合信息的, 而这个是需要找出每一个合理的path.
        // 考虑过把parent也作为递归的condition, 但是没有理清楚. 我想到了可能会产生死循环, 但是没想到这个问题是可以解决的.
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> buffer = new ArrayList<>();
        helper(root, res, buffer, target, true);
        return res;
    }
    
    private void helper(ParentTreeNode root, List<List<Integer>> res, List<Integer> buffer, int target, boolean isLeft) {
        if (root == null) {
            return;
        }
        
        // Paths that start from current node toward root
        int temp = target;
        buffer.add(root.val);
        int level = buffer.size() - 1;
        for (int i = level; i >= 0; i--) {
            temp -= buffer.get(i);
            if (temp == 0) {
                List<Integer> list = new ArrayList<>();
                for (int j = level; j >= i; j--) {
                    list.add(buffer.get(j));
                }
                res.add(list);
            }
        }
        // Paths that start from current node to other side
        if (temp > 0) {
            List<Integer> reverseBuffer = new ArrayList<>();
            for (int i = buffer.size() - 1; i >= 0; i--) {
                reverseBuffer.add(buffer.get(i));
            }
            ParentTreeNode first = root;
            while (first.parent != null) {
                first = first.parent;
            }
            List<List<Integer>> res1 = new ArrayList<>();
            List<Integer> buffer1 = new ArrayList<>();
            if (isLeft) {
                findPath(first.right, res1, buffer1, temp, true);
            } else {
                findPath(first.left, res1, buffer1, temp, true);
            }
            for (List<Integer> list : res1) {
                List<Integer> list1 = new ArrayList<>(reverseBuffer);
                list1.addAll(list);
                res.add(list1);
            }
        }
        
        // Paths that start from current node toward leaf node
        findPath(root, res, new ArrayList<Integer>(), target, false);
        
        // Traverse
        helper(root.left, res, buffer, target, true);
        helper(root.right, res, buffer, target, false);
        buffer.remove(buffer.size() - 1);
    }
    
    // find all paths whose start is current root node
    private void findPath(ParentTreeNode root, List<List<Integer>> res, List<Integer> buffer, int target, boolean isCross) {
        if (root == null) {
            return;
        }
        
        buffer.add(root.val);
        if (target == root.val) {
            if (buffer.size() > 1 && !isCross) {
                res.add(new ArrayList<>(buffer));
            }
            if (isCross) {
                res.add(new ArrayList<>(buffer));
            }
        }
        findPath(root.left, res, buffer, target - root.val, isCross);
        findPath(root.right, res, buffer, target - root.val, isCross);
        buffer.remove(buffer.size() - 1);
    }
```