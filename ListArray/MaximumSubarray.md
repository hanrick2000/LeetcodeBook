# [MaximumSubarray](http://www.lintcode.com/en/problem/maximum-subarray/#)

## Question

Given an array of integers, find a contiguous subarray which has the largest sum.

## Examples

![](https://farm5.staticflickr.com/4082/35605866466_ab426b1716_o.jpg)

## Analysis

 Classic problem!!!

 Like this kind of O(n) problem, do not think it as DP problem. Just think intuitively.

## Code

```java
// 第一感觉是这种 n^2的解法, 但是代码极其丑陋, 三种情况思路倒是清晰
public int maxSubArray(int[] nums) {
    if (nums.length == 0) {
        return 0;
    }
    // get sums
    // 我想当于是把 prefix sum 弄成了 O(n) 来存储, 而标准答案是 O(1), prefix sum 只是一个中间结果
    int[] sums = new int[nums.length];
    sums[0] = nums[0];
    for (int i = 1; i < nums.length; i++) {
        sums[i] += sums[i - 1] + nums[i];
    }
    // get max
    // three conditions
    // 1
    int max = Integer.MIN_VALUE;
    for (int i = 0; i < sums.length; i++) {
        max = Math.max(max, sums[i]);
    }
    // 2
    for (int i = 0; i < nums.length; i++) {
        max = Math.max(max, nums[i]);
    }
    // 3
    for (int i = 1; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            int sum = sums[j] - sums[i - 1];
            max = Math.max(sum, max);
        }
    }
    return max;
}

// Best solution!
public int maxSubArray(int[] nums) {
    if (nums.length == 0) {
        return 0;
    }
    // prefix sum in O(1) space, not sums
    // normally such kind of question can be solved in O(n)
    // three conditions
    // 1 -> max is current nums[i], then previous minSum is from 0 to i-1
    // 2 -> max is from 0 to i, then minSum = 0
    // 3 -> max is from i to j, then minSum is from 0 to i - 1
    // So it's important to provide an initial value as minSum = 0
    int max = Integer.MIN_VALUE, minSum = 0, sum = 0;
    for (int i = 0; i < nums.length; i++) {
        sum += nums[i];
        max = Math.max(max, sum - minSum);
        minSum = Math.min(minSum, sum);
    }
    return max;
}
```