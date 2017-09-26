# [TwoSumLessThanOrEqualTo](http://lintcode.com/en/problem/two-sum-less-than-or-equal-to-target/)

## Question

Given an array of integers, find how many pairs in the array such that their sum is less than or equal to a specific target number. Please return the number of pairs.

## Examples

Given nums = [2, 7, 11, 15], target = 24. Return 5.
2 + 7 < 24

2 + 11 < 24

2 + 15 < 24

7 + 11 < 24

7 + 15 < 25

## Analysis

首先参照 two sum 进行 sort, 然后双指针用变量控制法. 到这里有点明白了, 为什么我看很多题都像是在用 greedy 在做, 那是因为我对题目的类型分类不够清晰, 总觉得每道题都是在蒙, 没有自己的理论知识体系, 是不成章法的.

这里的变量控制法的关键是指针不回头.

## Code

```java
public int twoSum5(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    Arrays.sort(nums);
    int count = 0;
    while (left < right) {
        int current = nums[left] + nums[right];
        if (current <= target) {
            count += right - left;
            left++;
        } else if (current > target) {
            right--;
        }
    }

    return count;
}
```