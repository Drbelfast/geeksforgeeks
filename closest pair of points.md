Input: An array of n points `P[]`

Output: The smallest distance between two points in the given array.

As a pre-processing step, input array is sorted according to x coordinates

1. Find the middle point in the sorted array. We can take P[n/2] as middle point
2. Divide the given array in two halves. The first sub array contains points from P[0] to P[n/2]. The second subarray contains points from P[n/2+1] to P[n-1].
3. Recursively find the smallest distances in both subarrays. Let the distance be `dl` and `dr`. Find the minimum `dl` and `dr`. Let the minimum be `d`. 
4. From above 3 steps, we have an upper bound `d` of minimum distance. Now we need to consider the pairs such that point in pair is from left half and other is from right half. Consider the vertical line passing through passing through P[n/2] and find all points whose x coordinate is closer than d to the middle vertical line. Build an array strip[] of all such points.
5. Sort the array strip[] according to y coordinates. This step is O(nLogn). *It can be optimized to O(n) by recursively sorting and merging.*
6.  Find the smallest distance in strip[]. This is tricky. From first look, it seems to be a O(n^2) step, but it is actually O(n). It can be proved geometrically that for every point in strip, we only need to check at most 7 points after it (note that strip is sorted according to Y coordinate). See [this ](http://people.csail.mit.edu/indyk/6.838-old/handouts/lec17.pdf)for more analysis.
7. Finally return the minimum of d and distance calculated in above step (step 6)

Correctness claim, see Ref 2:

1. p and q are members of strip pairs Sy
2. p and q are at most 7 positions apart in Sy

```java
import java.util.Arrays;
import java.util.Comparator;

public class CloestPair {
	private static double bestDistance = Double.POSITIVE_INFINITY;
	public static double dist(Point p1, Point p2) {
		return Math.sqrt((p1.x - p2.x) * (p1.x - p2.x) + (p1.y - p2.y) * (p1.y - p2.y));
	}
	
	public static double bruteForce(Point[] p) {
		double min = Double.MAX_VALUE;
		for (int i = 0; i < p.length - 1; i++) {
			for (int j = 1; j < p.length; j++) {
				double dist = dist(p[i], p[j]);
				if(dist < min) min = dist;
			}
		}
		return min;
		
	}
	
	public static double cloest(Point[] p) {
		int n = p.length;
		Point[] pointsByX = new Point[n];
		Point[] pointsByY = new Point[n];
		for (int i = 0;  i < n; i++) {
			pointsByX[i] = p[i];
			
		}
		Arrays.sort(pointsByX, new Comparator<Point>() {
			@Override
			public int compare(Point p1, Point p2) {
				return p1.x - p2.x;
			}
		});
		for (int i = 0; i < n; i++) {
			pointsByY[i] = pointsByX[i];
		}
		Point[] aux = new Point[n];
		return helper(pointsByX, pointsByY, aux, 0, n - 1);
	}
	
	public static double helper(Point[] pointsByX, Point[] pointsByY, Point[] aux, int lo, int hi) {
		if (lo >= hi) return Double.POSITIVE_INFINITY;
		
		int mid = lo + (hi - lo) / 2;
		Point midPoint = pointsByX[mid];
		
		// compute the closest pair in left sub part and right sub part
		double delta1 = helper(pointsByX, pointsByY, aux, lo, mid);
		double delta2 = helper(pointsByX, pointsByY, aux, mid + 1, hi);
		double delta = Math.min(delta1, delta2);
		
		// merge back so pointsByY[lo...hi] are sorted by y-coordinate.
		merge(pointsByY, aux, lo, mid, hi);
		
		// aux[0...m-1]  = sequence of points closer than delta, sorted by y-coordiante
		int m = 0;
		for (int i = lo; i <= hi; i++) {
			if (Math.abs(pointsByY[i].x - midPoint.x) < delta) {
				aux[m++] = pointsByY[i];
			}
		}
		
		// compare each point to its neighbors with y-coordinate closer than delta
        for (int i = 0; i < m; i++) {
            // a geometric packing argument shows that this loop iterates at most 7 times
            for (int j = i+1; (j < m) && (aux[j].y - aux[i].y < delta); j++) {
                double distance = dist(aux[i], aux[j]);
                if (distance < delta) {
                    delta = distance;
                    if (distance < bestDistance) {
                        bestDistance = delta;
                    }
                }
            }
        }
        return delta;
		
	}
	
	private static void merge(Point[] a, Point[] aux, int lo, int mid, int hi) {
		for (int k = lo; k <= hi; k++) {
			aux[k] = a[k];
		}
		
		// merge back to a[]
		int i = lo, j = mid + 1;
		for (int k = lo; k <= hi; k++) {
			if ( i > mid) a[k] = aux[j++];
			else if (j > hi) a[k] = aux[i++];
			else if (aux[i].y < aux[j].y) a[k] = aux[i++];
			else a[k] = aux[j++];
		}
	}
	

	public static void main(String[] args) {
		Point P[] = {new Point(2,3), new Point(12, 30), new Point(40, 50), new Point(5 ,1), new Point(12, 10), new Point(3, 4)};
		cloest(P);
		System.out.println(bestDistance);
		

	}

}

class Point{
	int x, y;
	public Point(int x, int y) {
		this.x = x;
		this.y = y;
	}

}

```



## Reference

1. [How to solve this @coursera](https://www.youtube.com/watch?v=vS4Zn1a9KUc)
2. [Correctness about 7 positions @coursera](https://www.youtube.com/watch?v=BhQCj59sW_s)
3. [Closest pair implementation](http://algs4.cs.princeton.edu/99hull/ClosestPair.java.html)