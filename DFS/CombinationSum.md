# [CombinationSum](https://leetcode.com/problems/combination-sum/)

## Question

Given a set C of unique positive integers, and a target number T. Find all unique combinations in C that sum up to T. Integers in each combination are in non-descending order.

## Examples

![](https://farm5.staticflickr.com/4188/33813423233_a8525212c2_o.jpg)

## Analysis

This question is not hard. Just follow the three steps of recursion. And don't forget to meet all the requirements from the question.

## Code

```java
public List<List<Integer>> combinationSum(int[] candidates, int target) {
    List<List<Integer>> res = new ArrayList<>();
    // 就是一个搜索树, 搞清楚进行到哪个搜索状态了, 在脑袋中构建一个搜索树的样子
    // 需要一个list从顶端到叶子节点构建path, 所以定义中需要有一个list
    List<Integer> buffer = new ArrayList<>();
    // non-descending
    Arrays.sort(candidates);
    // target和candidates肯定也不可或缺
    dfs(res, buffer, target, candidates, 0);
    return res;
}

private void dfs(List<List<Integer>> res, List<Integer> buffer, int target, int[] candidates, int index) {
    // 递归出口, 可能不止一个condition
    if (target < 0) {
        return;
    }
    if (target == 0) {
        res.add(new ArrayList<>(buffer));
        return;
    }
    // 递归第二步, 先拆解, 到了每个状态应该做什么事情
    // 每个状态分两个方面, 一个是向下递归, 第二个是回溯, 这两个方面包含了需要拆解的事情
    for (int i = index; i < candidates.length; i++) {
        // 这块儿就是核心部分, 去满足所有的要求的! 比如unique combinations
        // 去重两部分分析:
        // 1. 本身candidate数组里有重复 (但是这道题没有, 好吧, 其实有, 而leetcode上那道没有)
        // 2. 选择neighbor时造成了重复. 所以其实, dfs combination就是通过决定如何选取neighbor的规则来解题
        // 解答:
        // 1. 因为sort过, 所以跳过重复的就行了
        // 2. 所以引入index, 让每个点知道当前的index是什么
        if (i > index && candidates[i] == candidates[i - 1]) {
            continue;
        }
        int curr = candidates[i];
        buffer.add(curr);
        dfs(res, buffer, target - curr, candidates, i);
        // 剩下的这一步其实可以在第三步递归出口写完之后来写, 算了, 还是拆解的时候写把, 免得忘了
        // 从当前状态的视角观察, 其实就是在remove自己
        buffer.remove(buffer.size() - 1);
    }
}
```