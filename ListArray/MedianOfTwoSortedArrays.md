# [MedianOfTwoSortedArrays](link)

## Question

Find median number of two sorted arrays.

## Examples

![](https://i.imgur.com/gjwNdEL.jpg)

## Analysis

It's quite similar to merging two sorted lists.

## Code

```java
// My own stupid solutions.
public double findMedianSortedArrays(int[] A, int[] B) {
    // O(m+n), O(m+n)
    // What if we have two big arrays? We need constant space solution. Actually we don't need to use quick select. Because two arrays are sorted, so we can just get median number by indexes.
    // Consider about merging two linked lists, we are using an extra pointer to store new list, so we should use the same here.
    if ((A.length + B.length) == 1) {
        return A.length == 0 ? (double) B[0] : (double) A[0];
    }

    int lengthA = A.length;
    int lengthB = B.length;
    int[] newArray = new int[lengthA + lengthB];
    int pA = 0, pB = 0;
    while (pA < lengthA && pB < lengthB) {
        if (A[pA] < B[pB]) {
            newArray[pA + pB] = A[pA];
            pA++;
        } else {
            newArray[pA + pB] = B[pB];
            pB++;
        }
    }

    // We use pA + pB, however, (pA + pB) max value is total length - 2, but if pA == lengthA, then we can get to total length - 1. So this non-optimal solution is quite similar to merging two sorted lists.
    while (pA < lengthA) {
        newArray[pA + pB] = A[pA];
        pA++;
    }

    while (pB < lengthB) {
        newArray[pA + pB] = B[pB];
        pB++;
    }

    int m1 = newArray[newArray.length / 2 - 1];
    int m2 = newArray[newArray.length / 2];
    return newArray.length % 2 == 0 ? (m1 + m2) / 2.0 : (double) m2;
}
```