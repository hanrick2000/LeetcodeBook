#### Question
Given a binary tree, find all of its path sum. The path doesn’t need to start from root and end at leaf.
#### Examples
Given 1,2,3,#,4,2,#,3, return [2,4], [1,3,2]
#### Analysis
Actually this is a question using backtracking. It’s kind of similar to traverse method.
#### Code
	private void findPath(List<List<Integer>> res, List<Integer> list, TreeNode root, int target) {
	System.out.println(root.val);
	if (root == null) {
	return;
	}
	if (target < root.val) {
	return;
	}
	if (target == root.val) {
	list.add(root.val);
	res.add(new ArrayList<>(list));
	list.remove(list.size() - 1);
	return;
	}
	// Traverse
	list.add(root.val);
	System.out.println(root.val);
	findPath(res, list, root.left, target - root.val);
	findPath(res, list, root.right, target - root.val);
	list.remove(list.size() - 1);
	}