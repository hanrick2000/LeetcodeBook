# [PalindromePartitioning](http://www.lintcode.com/en/problem/palindrome-partitioning/)

## Question

Partition given string s that every substring of s is a palindrome.

## Examples

![](https://farm5.staticflickr.com/4178/34484690282_7875aa2138_o.jpg)

## Analysis

It's quite similar to combination sum. The key point is that how to calculate the possible **valid** states in current level.

**Use index** rather than storing substring directly in buffer list.

## Code

```java
public List<List<String>> partition(String s) {
    List<List<String>> res = new ArrayList<>();
    if (s == null || s.length() == 0) {
        return res;
    }
    // This is still some kind of 2^n searching problem, since there are about n - 1 positions to choose partition, and each position can be partitioned or not.
    // And the question requires use to return all possible partitioning, so it's time to use DFS
    List<String> buffer = new ArrayList<>();
    dfs(res, buffer, s, 0);
    return res;
}
private void dfs(List<List<String>> res, List<String> buffer, String s, int index) {
    // end
    if (index == s.length()) {
        res.add(new ArrayList<>(buffer));
        return;
    }
    // next states
    for (int i = index; i < s.length(); i++) {
        String sub = s.substring(index, i + 1);
        // there is many duplicate calculation
        // Although memorizing all the possible palindrome results is a method to optimize, the main complexity is still in 2^n
        if (!isPalindrome(sub)) {
            continue;
        }
        buffer.add(sub);
        dfs(res, buffer, s, i + 1);
        buffer.remove(buffer.size() - 1);
    }
}

private boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}
```