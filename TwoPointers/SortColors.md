# [SortColors](http://lintcode.com/en/problem/sort-colors/#)

## Question

Sort as [0,0,0,...,1,1,1,...,2,2,2]

## Examples

Given [1, 0, 1, 2], sort it in-place to [0, 1, 1, 2].

## Analysis

Two pointers + partition.

1. Because right is pointing to some value that is not equal to 2, so we use i <= right to check the value of i when i == right.
1. Don't move i when swap right pointer, because the swapped value could be 0, we need i to stay to check if it's 0, then we can move i if the value is really 0 because we will swap it with left.

## Code

```java
public void sortColors(int[] nums) {
    int left = 0, right = nums.length - 1, i = 0;
    // Use i <= right
    while (i <= right) {
        if (nums[i] == 0) {
            swap(nums, i, left);
            left++;
            i++;
        } else if (nums[i] == 1) {
            i++;
        } else {
            // Don't move i
            swap(nums, i, right);
            right--;
        }
    }
}

private void swap(int[] nums, int a, int b) {
    int temp = nums[a];
    nums[a] = nums[b];
    nums[b] = temp;
}
```