# [DecodeWays](http://lintcode.com/en/problem/decode-ways/#)

## Question

Find number of ways to decode a given string.

## Examples

Given "12", return 2. (There are two ways, one is "AB", and another one is "L")

## Analysis

So many edge cases!

Try to build a reasonable state transition equation.

## Code

```java
public int numDecodings(String s) {
    // for example, 1837918273, to reach this string, you make either one 
    // two steps forward
    if (s == null || s.length() == 0 || s.charAt(0) == '0') {
        return 0;
    }
    int n = s.length();
    int[] res = new int[n + 1];
    // init
    res[0] = 1;
    res[1] = 1;
    for (int i = 2; i < n + 1; i++) {
        int prev = s.charAt(i - 2) - '0';
        int curr = s.charAt(i - 1) - '0';
        int num = prev * 10 + curr;
        if (num == 10 || num == 20) {
            res[i] = res[i - 2];
        } else if (num > 10 && num <= 26) {
            res[i] = res[i - 1] + res[i - 2]; 
        } else if (curr == 0) {
            return 0;
        } else {
            res[i] = res[i - 1];
        }
    }
    return res[n];
}
```