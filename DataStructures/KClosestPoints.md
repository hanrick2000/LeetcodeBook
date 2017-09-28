# [KClosestPoints](http://www.lintcode.com/en/problem/k-closest-points/#)

## Question

Given some points and a point origin in two dimensional space, find k points out of the some points which are nearest to origin. Return these points sorted by distance, if they are same with distance, sorted by x-axis, otherwise sorted by y-axis.

## Examples

Given points = [[4,6],[4,7],[4,4],[2,5],[1,1]], origin = [0, 0], k = 3

Return [[1,1],[2,5],[4,4]]

## Analysis

Notice running time should be nlogk because each insert operation is based on the size of heap.

It's about basic skills writing custom comparator. Sort by distance, x-axis, and y-axis.

## Code

```java
public Point[] kClosest(Point[] points, Point origin, int k) {
    // nlogk
    PriorityQueue<Point> maxHeap = new PriorityQueue<>(k, new Comparator<Point>(){
        public int compare(Point p1, Point p2) {
            double d1 = getDistance(origin, p1);
            double d2 = getDistance(origin, p2);
            if (d1 == d2) {
                return p2.x == p1.x ? p2.y - p1.y : p2.x - p1.x;
            }

            return Double.compare(d2, d1);
        }
    });

    for (Point p : points) {
        maxHeap.offer(p);
        if (maxHeap.size() > k) {
            maxHeap.poll();
        }
    }

    Point[] res = new Point[k];
    for (int i = res.length - 1; i >= 0; i--) {
        res[i] = maxHeap.poll();
    }

    return res;
}

private double getDistance(Point origin, Point p) {
    return Math.sqrt(Math.pow(origin.x - p.x, 2) + Math.pow(origin.y - p.y, 2));
}
```