Naive way is compare one by one and time complexity is O(n^2).

We have nO(logn) methods

1. merge sort
2. balanced binary search tree
3. binary indexed tree

## Merge sort

During the merge, count the inversion numbers.

```java
public class CountInversions {
	public static int count(int[] nums) {
		int[] tmp = new int[nums.length];
		return mergeSort(nums, 0, nums.length - 1, tmp);
	}
	
	private static int mergeSort(int[] nums, int l, int r, int[] tmp) {
		int mid, invCount = 0;
		if (l < r) {
			mid = l + (r - l) / 2;
			invCount += mergeSort(nums, l, mid, tmp);
			invCount += mergeSort(nums, mid + 1, r, tmp);
			
			invCount += merge(nums, l, mid + 1, r, tmp);
		}
		return invCount;
	}
	
	private static int merge(int[] nums, int l, int mid, int r, int[] tmp) {
		int leftBound = mid - 1;
		int i = l, k = l;
		int j = mid;
		int invCount = 0;
		while ( i <= leftBound && j <= r) {
			if (nums[i] < nums[j])
				tmp[k++] = nums[i++];
			else{
				tmp[k++] = nums[j++];
				invCount += mid - i;
			}
				
		}
		while (i <= leftBound) {
			tmp[k++] = nums[i++];
		}
		while (j <= r) {
			tmp[k++] = nums[j++];
			
		}
		for (int m = l; m <= r; m++) {
			nums[m] = tmp[m];
		}
		return invCount;
		
		
		
	}
	
	public static void main(String[] args) {
		int[] test = {1, 20, 6, 4, 5};
		System.out.println(count(test));
	}
}
```

## Balanced Binary Search tree

