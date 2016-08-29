```java
private static int[] tmp = int[a.length];
private void mergeSort(int[] a, int l, int r) {
  if (l == r) return;
  int mid = left + (right - left) / 2;
  mergeSort(a, l, mid);
  mergeSort(a, mid + 1, r);
  merge(a, l, mid + 1, r);
}

private void merge(int[] a, int l, int mid, int r) {
  int index = 0;
  int leftBoundary = mid;
  while(l < leftBoundary && mid <= r) {
    if (a[l] < a[mid])
      tmp[index++] = a[l];
    else 
      tmp[index++] = a[mid];
  }
  
  while (l < leftBoundary)
    tmp[index++] = a[l];
  while (mid <= r) {
    tmp[index++] = a[mid];
  }
  for (int j = 0; j < a.length; j++) {
    a[l + j] = tmp[j];
  }
}
```

