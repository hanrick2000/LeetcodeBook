# [BubbleSort](http://www.geeksforgeeks.org/bubble-sort/)

## Question

Self-implemented bubble sort.

## Examples

Given 3,1,2,4,5 return 1,2,3,4,5

## Analysis

This is the simplest sorting algorithm that I can come up with. Also it's the most intuitive one.

But the true principle of bubble sort is to bubble bigger number towards last position. Not to only bubble biggest number to the last position. The magic here is that each time the bubble will eventually be a biggest number at the last position.

Worst case is O(n^2), the array is reverse sorted. (n-1 + n-2 + ... + 1). Best case is O(n), the array is already sorted.

## Code

```java
// My bubble sort!!!
public void sortIntegers2(int[] A) {
    // bubble sort, each time bubble the biggest number to last pos
    for (int i = 0; i < A.length; i++) {
        int max = Integer.MIN_VALUE;
        int maxIndex = 0;
        int lastIndex = A.length - i - 1;
        int j;
        for (j = 0; j <= lastIndex; j++) {
            if (A[j] > max) {
                max = A[j];
                maxIndex = j;
            }
        }
        swap(maxIndex, lastIndex, A);
    }
}

private void swap(int i, int j, int[] A) {
    int temp = A[j];
    A[j] = A[i];
    A[i] = temp;
}

// A better way is to swap each time. So that for example, 3,1,2,5,4
// actually can be sorted in first operation. Because 3 will still be
// moved to last.
// 记住是 towards last position, 简直太形象了, 就是一堆气泡在往上冒, 所以其实有可能在过程中就已经 sort 结束了.
// 但是如果一上来就遇见最大的, 那就 sort 不了其他点了. 可能就会慢一些.
public void sortIntegers2(int[] A) {
    // a better bubble sort
    // i represents the ith bubble time. So there will be length - 1 bubbles.
    for (int i = 0; i < A.length - 1; i++) {
        // j represents the position that our bubble could be, the last position is length - 2
        // optimize by adding flag to check if it's already sorted
        boolean sorted = true;
        for (int j = 0; j < A.length - 1 - i; j++) {
            if (A[j] > A[j + 1]) {
                swap(j, j + 1, A);
                sorted = false;
            }
        }
        if (sorted) {
            break;
        }
    }
}

private void swap(int i, int j, int[] A) {
    int temp = A[j];
    A[j] = A[i];
    A[i] = temp;
}
```