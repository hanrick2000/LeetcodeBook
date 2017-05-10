# [CourseSchedule](https://leetcode.com/problems/course-schedule/#/description)

## Question

To take course 0 you have to take course 1, which is [0, 1].

## Examples

![](https://farm5.staticflickr.com/4155/34439308361_922655fcb1_o.jpg)

## Analysis

Typical topological sorting, since every element has relationship with each other. Normally I would use `Map<Integer, Set<Integer>>` to represent this graph. But for this question, since all nodes are presented from 0 to n-1, so we can use the nature of array to hash index of nodes.

The index 0 to n-1 can simplify the representation of graph! So we can use List[] to represent the graph and ArrayList to represent degrees. What if there are duplicates in the given 2D array? (ex, there are two pairs of [1,9]) Not a problem! The List[] will add it again, and array will reduce degree again. So the idea is, no mattter there is duplicate or not, the graph representation and in-degree representation should stick together and keep the same pace.

## Code

```java
public boolean canFinish(int numCourses, int[][] prerequisites) {
    // Build graph
    List<Integer>[] graph = buildGraph(numCourses, prerequisites);
    // Count in-degree
    int[] indegree = getIndegree(numCourses, prerequisites);
    // BFS
    int n = numCourses;
    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < n; i++) {
        if (indegree[i] == 0) {
            queue.offer(i);
            //System.out.println("node : " + i);
            numCourses -= 1;
        }
    }
    while(!queue.isEmpty()) {
        int curr = queue.poll();
        for (int i : graph[curr]) {
            indegree[i]--;
            if (indegree[i] == 0) {
                queue.offer(i);
                numCourses -= 1;
            }
        }
    }
    return numCourses == 0;
}

private List[] buildGraph(int n, int[][] prerequisites) {
    List<Integer>[] graph = new List[n];
    for (int i = 0; i < n; i++) {
        graph[i] = new ArrayList<Integer>();
    }
    for (int i = 0; i < prerequisites.length; i++) {
        graph[prerequisites[i][1]].add(prerequisites[i][0]);
    }
    return graph;
}

private int[] getIndegree(int n, int[][] prerequisites) {
    int[] indegree = new int[n];
    for (int i = 0; i < prerequisites.length; i++) {
        indegree[prerequisites[i][0]]++;
    }
    return indegree;
}
```