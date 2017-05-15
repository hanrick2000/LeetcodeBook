# [Permutations2](http://www.lintcode.com/en/problem/permutations-ii/)

## Question

Given a set of numbers with duplicates. Find all unique permutations.

## Examples

![](https://farm5.staticflickr.com/4160/34489958792_dd7b9dcfc9_o.jpg)

## Analysis

**Use visited array to store binary values 0 or 1.**

Time complexity: n * n!.

Draw some concrete simple examples on paper and it would be easier to understand.

For [1,2,2], we can regard it as [1, 2(1), 2(2)], so duplicates are 2(1) and 2(2), normally we just choose 2(1).

Don't think too much, just list every possibility that there might be duplicates, and adding some rule to remove them.

## Code

```java
public List<List<Integer>> permuteUnique(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    if (nums == null || nums.length == 0) {
        res.add(new ArrayList<Integer>());
        return res;
    }
    Arrays.sort(nums);
    //int[] numsWithoutDuplicate = removeDuplicates(nums);
    ArrayList<Integer> buffer = new ArrayList<>();
    int[] visited = new int[nums.length];
    dfs(res, buffer, nums, visited);
    return res;
}

// res -> result list, buffer -> solution path to last level, nums -> target array, indexes -> index list of current elements in the buffer
// 用hash来存visited就行了!!! list.contains()这个方法也太傻逼了把
private void dfs(List<List<Integer>> res, List<Integer> buffer, int[] nums, int[] visited) {
    // exit
    if (buffer.size() == nums.length) {
        // if (res.contains(buffer)) {
        //     return;
        // }
        res.add(new ArrayList<>(buffer));
        return;
    }
    for (int i = 0; i < nums.length; i++) {
        // Two kinds of duplicates:
        // 1. duplicate numbers in the solution path, like 1,2,2, and these
        // two 2s are differnt
        // 2. duplicate paths
        // 1
        if (visited[i] == 1) {
            continue;
        }
        // 2, we can't just igore duplicates in every level.
        // We need visited array. 就是说:
        // 比如，给出一个排好序的数组，[1,2,2]，那么第一个2和第二2如果在结果中互换位置，
        // 我们也认为是同一种方案，所以我们强制要求相同的数字，原来排在前面的，在结果
        // 当中也应该排在前面，这样就保证了唯一性。所以当前面的2还没有使用的时候，就
        // 不应该让后面的2使用。
        if (i > 0 && nums[i] == nums[i - 1] && visited[i - 1] == 0) {
            continue;
        }
        visited[i] = 1;
        buffer.add(nums[i]);
        dfs(res, buffer, nums, visited);
        buffer.remove(buffer.size() - 1);
        visited[i] = 0;
    }
}

// We don't need to preprocess here
private int[] removeDuplicates(int[] nums) {
    // pointer to current unique num
    int index = 0;
    for (int i = 0; i < nums.length; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) {
            continue;
        }
        // move index forward
        nums[++index] = nums[i];
    }
    int numsWithoutDuplicates[] = new int[index + 1];
    for (int i = 0; i < index + 1; i++) {
        numsWithoutDuplicates[i] = nums[i];
    }
    return numsWithoutDuplicates;
}
```