# [CombinationSum2](http://www.lintcode.com/en/problem/combination-sum-ii/#)

## Question

Non descending order, no duplicate combinations, and each number can only be used for once.

## Examples

![](https://farm5.staticflickr.com/4182/34590611616_a9a30ab5d0_o.jpg)

## Analysis

So similar to CombinationSum, there is only one difference that each number can only be used **for once**.

## Code

```java
public List<List<Integer>> combinationSum2(int[] num, int target) {
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> buffer = new ArrayList<>();
    Arrays.sort(num);
    dfs(res, buffer, num, target, 0);
    return res;
}

private void dfs(List<List<Integer>> res, List<Integer> buffer, int[] num, int target, int index) {
    // end
    if (target < 0) {
        return;
    }
    if (target == 0) {
        res.add(new ArrayList<>(buffer));
        return;
    }
    // divide
    // 不会像bfs那样说从当前的一个点展开到周围的点, 而是直接查看当前所有可能的状态
    // 定义里需要什么参数, 其实到这里才会知道, 因为当前所有可能的状态数是由上层传递
    // 的信息得到的
    for (int i = index; i < num.length; i++) {
        if (i > index && num[i] == num[i - 1]) {
            continue;
        }
        buffer.add(num[i]);
        dfs(res, buffer, num, target - num[i], i + 1);
        // backtracking
        buffer.remove(buffer.size() - 1);
    }
}
```