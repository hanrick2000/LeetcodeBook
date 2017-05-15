# [Permutations](http://www.lintcode.com/en/problem/permutations/)

## Question

Given a list of numbers, return all possible permutations. There is no duplicate number in the list.

## Examples

![](https://farm5.staticflickr.com/4177/34610834466_9878af1188_o.jpg)

## Analysis

This is easier than combination sum. Very straightforward.

Time complexity: n^2 * n!, since `buffer.contains(nums[i])` is O(n).

## Code

```java
public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    // factorial of n
    if (nums == null || nums.length == 0) {
        res.add(new ArrayList<Integer>());
        return res;
    }
    List<Integer> buffer = new ArrayList<>();
    dfs(res, buffer, nums);
    return res;
}

private void dfs(List<List<Integer>> res, List<Integer> buffer, int[] nums) {
    // end
    if (buffer.size() == nums.length) {
        res.add(new ArrayList<>(buffer));
        return;
    }
    // recursion
    for (int i = 0; i < nums.length; i++) {
        // O(n), any optimization?
        if (buffer.contains(nums[i])) {
            continue;
        }
        buffer.add(nums[i]);
        dfs(res, buffer, nums);
        buffer.remove(buffer.size() - 1);
    }
}
```