# [WordLadder2](http://www.lintcode.com/en/problem/word-ladder-ii/#)

## Question

Return all possible shortest sequences.

## Examples

![](https://farm5.staticflickr.com/4171/34555053702_5380ff45f6_o.jpg)

## Analysis

Use BFS to get distances to target, and use DFS to get all shortest sequences. Still it looks like a little difficult. There is still something that can be improved, like generalizing bfs function. But anyway, for the first time, it passed.

## Code

```java
public List<List<String>> findLadders(String start, String end, Set<String> dict) {
    // dfs求不了最短路径, 而bfs可以求
    // 所以先用bfs求最短路径, 存起来, 然后用dfs来解, 相当于用bfs给dfs提供了
    // 搜索的额外信息, 按照离end的距离来搞
    // Start bfs from end string to get distances from each intermediate
    // string to end string
    dict.add(start);
    Map<String, Integer> distances = new HashMap<>();
    Queue<String> queue = new LinkedList<>();
    Set<String> visited = new HashSet<>();
    queue.offer(end);
    visited.add(end);
    int distance = 0;
    boolean stopFlag = false; // 不能return, 得把倒数第二层都遍历完
    while (!queue.isEmpty() && !stopFlag) {
        distance++;
        // 如果我想在for neighbors里进行操作, 那我的length肯定就得
        // 在这里加加
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            String curr = queue.poll();
            for (String neighbor : getNeighbors(dict, curr)) {
                if (visited.contains(neighbor)) {
                    continue;
                }
                distances.put(neighbor, distance);
                if (neighbor.equals(start)) {
                    stopFlag = true;
                    break;
                }
                queue.offer(neighbor);
                visited.add(neighbor);
            }
            if (stopFlag) {
                break;
            }
        }
    }
    //System.out.println(distances.size());
    // Start dfs from start string to get all shortest paths
    List<List<String>> res = new ArrayList<>();
    List<String> buffer = new ArrayList<>();
    dict.remove(start);
    dict.add(end);
    distances.put(end, 0); // 别忘了初始化
    buffer.add(start);
    dfs(distances, start, end, dict, res, buffer, distance);
    //System.out.println(getNeighbors(dict, start));
    return res;
}

private void dfs(Map<String, Integer> distances,
                    String start, String end,
                    Set<String> dict,
                    List<List<String>> res,
                    List<String> buffer,
                    int distance) {
    // exit
    if (distance == 0) {
        res.add(new ArrayList<>(buffer));
        return;
    }
    // next
    for (String neighbor : getNeighbors(dict, start)) {
        //System.out.println(neighbor);
        if (distances.get(neighbor) == null) {
            continue;
        }
        if (distances.get(neighbor) != distance - 1) {
            continue;
        }
        //System.out.println(neighbor);
        buffer.add(neighbor);
        dfs(distances, neighbor, end, dict, res, buffer, distance - 1);
        buffer.remove(buffer.size() - 1);
    }
}

private List<String> getNeighbors(Set<String> dict, String curr) {
    List<String> neighbors = new ArrayList<>();
    for (char c = 'a'; c <= 'z'; c++) {
        for (int i = 0; i < curr.length(); i++) {
            if (curr.charAt(i) == c) {
                continue;
            }
            char[] temp = curr.toCharArray();
            temp[i] = c;
            String tempString = new String(temp);
            if (dict.contains(tempString)) {
                neighbors.add(tempString);
            }
        }
    }
    return neighbors;
}
```