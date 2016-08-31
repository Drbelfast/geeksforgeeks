A heap is a binary tree with these characteristics:

- it's complete
- it's (usually) implemented as an array
- Each node in a heap satisfies the *heap condition*



## Building a heap

1. for an array of n input elements, easier way is to do n times insertion

   which is O(N log N).

2. But a Faster method exisits:  [link]( https://en.wikipedia.org/wiki/Binary_heap) , time complexity is O(N). Also see CLRS 6.3 , clearly explained why it is O(N).

```java
public static void sort(Comparable[] a)
  {
     int N = a.length;
  // k = N /2 is beacause the last row amounts to half of the nodes and dont have to be heapify.
  
  	// construct a heap
     for (int k = N/2; k >= 1; k--) 
        sink(a, k, N);
  
  	// sort
     while (N > 1)
     {
        exch(a, 1, N--);
        sink(a, 1, N);
     }
}

// sink funciton
private void sink(int k)
  {
     while (2*k <= N)
     {
        int j = 2*k;
        if (j < N && less(j, j+1)) j++;
        if (!less(k, j)) break;
        exch(k, j);
        k = j;
} }
```



> Building a max heap and min heap from array. or Vice versa.

Regard the array as unordered heap, and do inplace heapify. which would cost O(N) time.

