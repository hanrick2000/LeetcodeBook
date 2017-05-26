# [NextPermutation](http://www.lintcode.com/en/problem/next-permutation/)

## Question

Find next permutation in ascending order.

## Examples

![](https://farm5.staticflickr.com/4199/34732892952_d41bdc78ef_o.jpg)

## Analysis

- My idea
  - Use DFS to get next valid permutation.
- Solution
  - The above idea is wrong!!! Since this question is about getting one valid next permutation. So we can't use DFS. DFS is used when we need to find all possible permutations. If we only need to find one next permutation, there must be some solution **without using DFS**.
  - We can use Intellij to debug, which is quite convenient.
  - Start from the nature of the array itself, don't be stuck in DFS mindset.
  - But actually this question is a good question, which is involved with some basic array operations.

## Code

```java
public int[] nextPermutation(int[] nums) {
   int len = nums.length;
   for (int i = len - 1; i >= 0; i--) {
       if (i > 0 && nums[i] > nums[i - 1]) {
           int minIndex = getMinIndex(nums, i, len - 1);
           swap(nums, i - 1, minIndex);
           reverse(nums, i, minIndex);
           return nums;
       }
   }
   reverse(nums, 0, len - 1);
   return nums;
}

private int getMinIndex(int[] nums, int begin, int end) {
   int min = nums[begin];
   int minIndex = begin;
   for (int i = begin; i < nums.length; i++) {
       if (nums[i] < min) {
           min = nums[i];
           minIndex = i;
       }
   }
   return minIndex;
}

private void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}

private void reverse(int[] nums, int begin, int end) {
    int len = end - begin + 1;
    int offset = begin;
    for (int i = 0; i < len / 2; i++) {
      swap(nums, i + offset, len - 1 - i + offset);
    }
}
```