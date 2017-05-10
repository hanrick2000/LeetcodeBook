# [SequenceReconstruction](https://leetcode.com/problems/sequence-reconstruction/#/description)

## Question

See below.

## Examples

![](https://farm5.staticflickr.com/4172/34441577981_de28ee432e_o.jpg)

## Analysis

Several edge cases:

- 1 and [[1,1]]
- [4,1,5,2,6,3] and [[5,2,6,3],[4,1,5,2]]
- 1 and [[], []]

## Code

```java
public boolean sequenceReconstruction(int[] org, int[][] seqs) {
    // Edge case
    // if (org.length > seqs.length) {
    //     return false;
    // }
    // Preprocess
    reduceOne(org, seqs);
    // Build graph (with hashmap, since this qustion requires unique node to connect possible connections)
    // [4,1,5,2,6,3], [[5,2,6,3],[4,1,5,2]] -> return true
    // 同时, 因为org和seqs相对独立, 所以肯定是用Map来做哈希
    Map<Integer, List<Integer>> graph = buildGraph(seqs);
    // Get indegree
    Map<Integer, Integer> indegree = getIndegree(seqs);
    // BFS
    int n = org.length;
    int num = 0;
    int[] res = new int[n];
    // Check number of nodes
    // 1 and [[], []] -> return false
    if (n != graph.size()) {
        //System.out.println("1");
        return false;
    }
    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < n; i++) {
        if (indegree.get(i) == 0) {
            queue.offer(i);
            res[num++] = i;
        }
        if (num > 1) {
            //System.out.println("2");
            return false;
        }
    }
    while (!queue.isEmpty()) {
        int size = queue.size();
        // level order
        for (int j = 0; j < size; j++) {
            int curr = queue.poll();
            int count = 0;
            for (int i : graph.get(curr)) {
                indegree.put(i, indegree.get(i) - 1);
                if (indegree.get(i) == 0) {
                    queue.offer(i);
                    res[num++] = i;
                    count++;
                    // [5,2,1,3,4] and [5,2,1], [5,3,4] -> return false
                    if (count > 1) {
                        //System.out.println("3");
                        return false;
                    }
                }
            }
        }
    }
    // Check number of elements
    // 1 and [[1,1]] -> return false
    if (num != graph.size()) {
        return false;
    }
    // Check if elements are equal
    // 1 and [[2]] -> return false
    for (int i = 0; i < n; i++) {
        if (res[i] != org[i]) {
            //System.out.println("4");
            return false;
        }
    }
    return true;
}

private Map<Integer, List<Integer>> buildGraph(int[][] seqs) {
    Map<Integer, List<Integer>> graph = new HashMap<>();
    // for (int i = 0; i < org.length; i++) {
    //     graph.put(i, new ArrayList<Integer>());
    // }
    // org和seqs相互独立, 所以不应该用以上的org.length来初始化
    for (int i = 0; i < seqs.length; i++) {
        for (int j = 0; j < seqs[i].length; j++) {
            graph.put(seqs[i][j], new ArrayList<Integer>());
        }
    }
    for (int i = 0; i < seqs.length; i++) {
        for (int j = 0; j < seqs[i].length - 1; j++) {
            graph.get(seqs[i][j]).add(seqs[i][j + 1]);
        }
    }
    return graph;
}

private Map<Integer, Integer> getIndegree(int[][] seqs) {
    Map<Integer, Integer> indegree = new HashMap<>();
    for (int i = 0; i < seqs.length; i++) {
        for (int j = 0; j < seqs[i].length; j++) {
            indegree.put(seqs[i][j], 0);
        }
    }
    for (int i = 0; i < seqs.length; i++) {
        for (int j = 1; j < seqs[i].length; j++) {
            indegree.put(seqs[i][j], indegree.get(seqs[i][j]) + 1);
        }
    }
    return indegree;
}

private void reduceOne(int[] org, int[][] seqs) {
    for (int i = 0; i < org.length; i++) {
        org[i]--;
    }
    for (int i = 0; i < seqs.length; i++) {
        for (int j = 0; j < seqs[i].length; j++) {
            seqs[i][j]--; // 这个可以自加减, 因为可以看做变量, 如果seqs是双重list就不行了l
        }
    }
}
```
