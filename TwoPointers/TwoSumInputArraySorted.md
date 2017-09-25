# [TwoSumInputArraySorted](http://lintcode.com/en/problem/two-sum-input-array-is-sorted/#)

## Question

Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

## Examples

Given nums = [2, 7, 11, 15], target = 9
return [1, 2]

## Analysis

Simply use two pointers.

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