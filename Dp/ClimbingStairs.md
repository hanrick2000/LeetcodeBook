# [ClimbingStairs](http://lintcode.com/en/problem/climbing-stairs/)

## Question

There are two ways to get to a stair, by one step or by two steps. Find number of ways to get a given stair.

## Examples

Given step n = 3, return 3.

## Analysis

It's easy to understand.

## Code

```java
public int climbStairs(int n) {
    if (n == 0) {
        return 1;
    }
    int[] res = new int[n + 1];
    res[0] = 1;
    res[1] = 1;
    // simple dp
    for (int i = 2; i < n + 1; i++) {
        res[i] = res[i - 1] + res[i - 2];
    }
    return res[n];
}
```