# [Subsets2](http://www.lintcode.com/en/problem/subsets-ii/)

## Question

Given a list of numbers that may have duplicates, return all possible subsets. (non-descending and non-duplicate)

## Examples

![](https://farm5.staticflickr.com/4169/33875983053_07dc7cef2e_o.jpg)

## Analysis

This is different from Permutations2. We don't need visited array here. We just ignore duplicate values. But if we add visited array, it can still be solved.

## Code

```java
public ArrayList<ArrayList<Integer>> subsetsWithDup(int[] nums) {
    ArrayList<ArrayList<Integer>> res = new ArrayList<>();
    if (nums == null || nums.length == 0) {
        res.add(new ArrayList<Integer>());
        return res;
    }
    Arrays.sort(nums);
    ArrayList<Integer> buffer = new ArrayList<>();
    //int[] visited = new int[nums.length];
    dfs(res, buffer, nums, 0);
    return res;
}
// index -> valid index for current level
private void dfs(ArrayList<ArrayList<Integer>> res, ArrayList<Integer> buffer, int[] nums, int index) {
    // exit
    res.add(new ArrayList<Integer>(buffer));
    // next
    for (int i = index; i < nums.length; i++) {
        // if (i > 0 && nums[i] == nums[i - 1] && visited[i - 1] == 0) {
        //     continue;
        // }
        // 这里是大于index, 不是大于0
        if (i > index && nums[i] == nums[i - 1]) {
            continue;
        }
        buffer.add(nums[i]);
        //visited[i] = 1; 跟permutations不一样, 不需要加visited, 直接跳过就行了, 因为Permutations是要求全排列, 所以长度都只能是nums.length, 会难一点
        // 这个地方被坑死了啊, 应该是i + 1, 不是index + 1
        // 不过呢, 加上visited, 也是可以做出来的!!! 是不是通用方法哦??
        dfs(res, buffer, nums, i + 1);
        buffer.remove(buffer.size() - 1);
        //visited[i] = 0;
    }
}
```