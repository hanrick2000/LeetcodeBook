# [StringPermutation](http://www.lintcode.com/en/problem/string-permutation/)

## Question

Decide if string A is a permutation of string B.

## Examples

![](https://farm5.staticflickr.com/4202/34504940880_44a7165e32_o.jpg)

## Analysis

It's quite easy. It's just used to clarify the meaning of permutation. A more elegant way is to use hash to count the number of each character. `cnt[(int) source.charAt(i)] += 1`.

## Code

```java
public boolean stringPermutation(String A, String B) {
    if (A.length() != B.length()) {
        return false;
    }
    if (A.length() == B.length()) {
        char[] arrayA = A.toCharArray();
        char[] arrayB = B.toCharArray();
        Arrays.sort(arrayA);
        Arrays.sort(arrayB);
        for (int i = 0; i < arrayA.length; i++) {
            if (arrayA[i] != arrayB[i]) {
                return false;
            }
        }
    }
    return true;
}
```