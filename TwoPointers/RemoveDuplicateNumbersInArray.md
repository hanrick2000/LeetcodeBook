# [RemoveDuplicateNumbersInArray]()

## Question

Given an array of integers, remove the duplicate numbers in it.

You should:

1. Do it in place in the array.
1. Move the unique numbers to the front of the array.
1. Return the total number of the unique numbers.

## Examples

Given nums = [1,3,1,4,4,2], you should:

Move duplicate integers to the tail of nums => nums = [1,3,4,2,?,?].

Return the number of unique integers in nums => 4.

Actually we don't care about what you place in ?, we only care about the part which has no duplicate integers.

## Analysis

We can also use HashMap to get O(n) solution.

## Code

```java
// nlogn with two pointers
public int deduplication(int[] nums) {
    if (nums.length == 0) {
        return 0;
    }

    Arrays.sort(nums);
    int left = 0, right = 0;
    while (right < nums.length) {
        if (nums[right] == nums[left]) {
            right++;
        } else {
            left++;
            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = nums[left];
            right++;
        }
    }

    return left + 1;
}
```