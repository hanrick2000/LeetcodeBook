# [TwoSumInputArraySorted](http://lintcode.com/en/problem/two-sum-input-array-is-sorted/#)

## Question

Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

## Examples

Given nums = [2, 7, 11, 15], target = 9
return [1, 2]

## Analysis

Simply use two pointers. But the idea behind this is that, every time we add up the smallest and biggest numbers in the array. If the current sum is greater than target, then we know that even add the smallest number we are too big, so we should reduce the biggest number, and move right pointer. Left pointer is similar.

## Code

```java
public int[] twoSum(int[] nums, int target) {
    // Simply use two pointers
    int left = 0, right = nums.length - 1;
    while (left + 1 < right) {
        int current = nums[left] + nums[right];
        if (current < target) {
            left++;
        } else if (current > target) {
            right--;
        } else {
            return new int[]{left + 1, right + 1};
        }
    }

    return new int[]{left + 1, right + 1};
}
```