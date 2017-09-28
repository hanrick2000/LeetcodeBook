# [HighFive](http://www.lintcode.com/en/problem/high-five/)

## Question

There are two properties in the node student id and scores, to ensure that each student will have at least 5 points, find the average of 5 highest scores for each person.

## Examples

Given results = [[1,91],[1,92],[2,93],[2,99],[2,98],[2,97],[1,60],[1,58],[2,100],[1,61]]

Return a map from id to average of top five scores.

## Analysis

It feels like if we are asked about `top` list of xxx, then it probably can be solved by heap.

Use min heap because we want to remove the record with smallest score each time.

## Code

```java
public Map<Integer, Double> highFive(Record[] results) {
    // With lots of memory
    Map<Integer, PriorityQueue<Record>> map = new HashMap<>();
    for (Record record: results) {
        if (!map.containsKey(record.id)) {
            // top five using min heap!!! Remove smallest each time
            map.put(record.id, new PriorityQueue<>(5, new Comparator<Record>(){
                public int compare(Record r1, Record r2) {
                    return r1.score - r2.score;
                }
            }));
        }

        PriorityQueue minHeap = map.get(record.id);
        minHeap.offer(record);
        if (minHeap.size() > 5) {
            minHeap.poll();
        }
    }

    Map<Integer, Double> res = new HashMap<>();
    for (int id : map.keySet()) {
        int sum = 0;
        for (Record record : map.get(id)) {
            sum += record.score;
        }

        res.put(id, sum / 5.0);
    }

    return res;
}
```