# [WordLadder](http://www.lintcode.com/en/problem/word-ladder/#)

## Question

![](https://farm5.staticflickr.com/4168/34666582486_7683eef5ae_o.jpg)

## Examples

![](https://farm5.staticflickr.com/4189/33896386943_9ba7bc03b4_o.jpg)

## Analysis

The solution on Jiuzhang is a better one and it's quite elegant! But questions on Lintcode and Leetcode are slightly different.

Time complexity: O(n^4) ?? n is the length of word. If HashSet contains method for a String is O(lenght of String).

Just draw out the graph, and you will see the most natural thing is to use 26 characters as neighbors.

**Increment length before size**!

一样的, 类似PostOffice, 双向思维, 我可以从dict中遍历去找所有的neighbors, 其实也可以从start单词出发去找所有符合条件并且在dict里的单词.

## Code

```java
public int ladderLength(String start, String end, Set<String> dict) {
    // 最短路径问题呗
    // 两种, 第一种以dict展开, 第二种以26个字母展开, 怕是dict还是要少点哦
    // 失误了, 这个方法有点失败, 因为说白了dict的长度始终是未知的, 有可能很大, 而字母也就26个, 26 * start.length, 其实也就是一个常数而已
    Queue<String> queue = new LinkedList<>();
    queue.offer(start);
    int length = 1;
    // 边检查边删dict
    while(!queue.isEmpty()) {
        // length++ 写在这儿更好, 这样就可以在for循环求neighbors的过程中就退出
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            String curr = queue.poll();
            // System.out.println(curr);
            if (curr.equals(end)) {
                return length;
            }
            if (inOneDistance(curr, end)) {
                return length + 1;
            }
            ArrayList<String> temp = new ArrayList<>();
            for (String word : dict) {
                if (inOneDistance(curr, word)) {
                    queue.offer(word);
                    temp.add(word);
                }
            }
            for (String t : temp) {
                dict.remove(t);
            }
        }
        length++;
    }
    return 0;
}

private boolean inOneDistance(String s1, String s2) {
    int d = 0;
    int length = s1.length();
    for (int i = 0; i < length; i++) {
        if (s1.charAt(i) != s2.charAt(i)) {
            d++;
        }
    }
    return d == 1;
}
```