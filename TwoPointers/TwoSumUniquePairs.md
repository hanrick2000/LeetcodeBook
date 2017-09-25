# [TwoSumUniquePairs](http://lintcode.com/en/problem/two-sum-unique-pairs/)

## Question

Given an array of integers, find how many unique pairs in the array such that their sum is equal to a specific target number. Please return the number of pairs.

## Examples

Given nums = [1,1,2,45,46,46], target = 47, return 2

1 + 46 = 47

2 + 45 = 47

## Analysis

Use similar idea from combination sum by just choosing a representative for the duplicate numbers. Once we choose a number, other numbers with same values are of no use and we can skip them.

Only when we have both pointers pointing to duplicates, we need to move them to a non duplicate location. For other two conditions, if current < target, then just move left one step further, even it's duplicate, it's still smaller than target, so we will move it again.

Also one edge case could be that 11 + 11 = 22.

## Code

```java
public int twoSum6(int[] nums, int target) {
    Arrays.sort(nums);
    int left = 0, right = nums.length - 1;
    int count = 0;
    while (left < right) {
        int current = nums[left] + nums[right];
        if (current < target) {
            left++;
        } else if (current > target) {
            right--;
        } else {
            count++;
            left++;
            right--;
            while (left < right && nums[left] == nums[left - 1]) {
                left++;
            }

            while (left < right && nums[right] == nums[right + 1]) {
                right--;
            }
        }
    }

    return count;
}
```