# [TwoSumClosest](http://lintcode.com/en/problem/two-sum-closest-to-target/#)

## Question

Given an array nums of n integers, find two integers in nums such that the sum is closest to a given number, target.

Return the difference between the sum of the two integers and the target.

## Examples

Given array nums = [-1, 2, 1, -4], and target = 4.

The minimum difference is 1. (4 - (2 + 1) = 1).

## Analysis

Still two pointers. A small point is that if current == target, then directly return 0.

## Code

```java
public int twoSumClosest(int[] nums, int target) {
    // 原理是通过排序去掉了很多不必要的筛选
    Arrays.sort(nums);
    int left = 0, right = nums.length - 1;
    int minDiff = Math.abs((nums[right] + nums[left]) - target);
    while (left < right) {
        int current = nums[left] + nums[right];
        if (current < target) {
            left++;
        } else if (current > target) {
            right--;
        } else {
            return 0;
        }

        minDiff = Math.min(minDiff, Math.abs(current - target));
    }

    return minDiff;
}
```