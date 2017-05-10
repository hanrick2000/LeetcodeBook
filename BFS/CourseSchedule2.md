# [CourseSchedule2](https://leetcode.com/problems/course-schedule-ii/#/description)

## Question

See below.

## Examples

![](https://farm3.staticflickr.com/2862/33537060624_7bf2c0f025_o.jpg)

## Analysis

It's almost identical to [CourseSchedule](CourseSchedule.md). This one has a result array to hold any one of valid topological order.

## Code

```java
public int[] findOrder(int numCourses, int[][] prerequisites) {
    // Build graph
    List<Integer>[] graph = buildGraph(numCourses, prerequisites);
    // Count in-degree
    int[] indegree = getIndegree(numCourses, prerequisites);
    // BFS
    Queue<Integer> queue = new LinkedList<>();
    int n = numCourses;
    int[] res = new int[numCourses];
    int index = 0;
    for (int i = 0; i < n; i++) {
        if (indegree[i] == 0) {
            queue.offer(i);
            res[index++] = i;
            numCourses--;
        }
    }
    while (!queue.isEmpty()) {
        int curr = queue.poll();
        for (int i : graph[curr]) {
            indegree[i]--;
            if (indegree[i] == 0) {
                queue.offer(i);
                res[index++] = i;
                numCourses--;
            }
        }
    }
    if (numCourses == 0) {
        return res;
    }
    return new int[0];
}

private List<Integer>[] buildGraph(int n, int[][] prerequisites) {
    List<Integer>[] graph = new List[n];
    for (int i = 0; i < n; i++) {
        graph[i] = new ArrayList<>();
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
