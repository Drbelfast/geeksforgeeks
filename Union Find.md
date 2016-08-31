---
title: A&DS-Union Find
date: 2016-08-09 22:21:58
tags:
categories: Algorithm
---

A **disjoint-set data structure**, also called a **union-find data structure**, is a data structure that keeps track of a set of elements partitioned into a number of disjoint(nonoverlapping) subsets. It supports two useful operations:

- Find: Determine which subset a particular element is in. This can be used for determining if two elements are in the same subset.
- Union: Join two subsets into a single subset.


`Union(A, B)` connects two elements A and B.

`Find(A, B)` is there any path connection elements A and B.

Why do we prefer Union-find than DFS in this scenario?

DFS need to traverse all the graph, this is bad when graph nodes are dynamically added or deleted. So use Union-find instead.

> When the edges of the graph are static—not changing over time—we can compute the connected components faster by using depth-first search. (CLRS)




## Application

1. [Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/), and its [union find solution](https://discuss.leetcode.com/topic/40685/java-union-find-dfs-bfs-code-very-clean)
2. [Detect cycle in a an undirected Graph](http://www.geeksforgeeks.org/union-find/)


> - Union-Find is used to determine the **connected componenets** in a graph. We can determine whether 2 nodes are in the same connected componenet or not in the graph.
>
>   We can also determine that by adding an edge between 2 nodes whether it leads to cycle in the graph or not. We learned that we can reduce its complexity to a very optimum level, so in case of very large and dense graph, we can use this data structure.
>
> - It is used to determine the cycles in the graph. In the **Kruskal's Algorithm**, Union Find Data Structure is used as a subroutine to find the cycles in the graph, which helps in finding the minimum spanning tree.



## Implementation

### Detect cycle in undirected graph

Consider the following graph:

```java
  0
  |  \
  |    \
  1-----2
```

We can keep track of the subsets in a 1D array, `parent[]`

The idea is: **for each edge, make subsets using both the vertices of the edge. if both the vertices are in the same subset, a cycle is found.**

Initially, all slots of parent array are initialized to -1. (means there is only one item in every subset)

```java
0   1   2
-1 -1  -1 
```

Now process all edges one by one.

*Edge 0 -1*: Find the subsets in which vertices 0 and 1 are. Since they are in different subsets, we take the union of them. For taking the unin, either make node 0 as parent of node 1 or vice-versa

```java
0   1   2    <----- 1 is made parent of 0 (1 is now representative of subset {0, 1})
1  -1  -1
```

 *Edge 1-2*: 1is in subset 1 and 2 is in subset 2. So, take union

```java
0   1   2    <----- 2 is made parent of 1 (2 is now representative of subset {0, 1, 2})
1   2  -1
```

*Edge 0-2*: 0 is in subset 2 and 2 is also in subset 2. Hence, including this edge forms a cycle.

```java
// Here comes code
package part1;


public class Graph {
	int V, E; // V -> no. of vertices & E -> no. of edges
	Edge edge[];
	class Edge {
		int src, dest;
	};
	
	// Creates a graph with V vertices and E edges
	Graph(int v, int e) {
		V = v;
		E = e;
		edge = new Edge[E];
		for (int i = 0; i < e; i++) {
			edge[i] = new Edge();
		}
	}
	
	// A utility function to find the subset of an element i
	int find(int[] parent, int i) {
		if (parent[i] == -1) {
			return i;
		}
		return find(parent, parent[i]);
	}
	// A utility function to do union of two subsets
	void Union(int[] parent, int x, int y) {
		int xset = find(parent, x);
		int yset = find(parent, y);
		parent[xset] = yset;
	}
	// The main function to check whether a given graph
	// contains cycle or not
	int isCycle(Graph graph) {
		
		// Allocate memory for creating V subsets
		int parent[] = new int[graph.V];
		
		// Initialize all subsets as single element sets
		for (int i = 0; i < graph.V; i++) {
			parent[i] = -1;
		}
		
		// Iterate throught all edges of graph, find subset of both
		// vertices of every edge, if both subsets are same, then 
		// there is a cycle in graph
		for (int i = 0; i < graph.E; i++) {
			int x = graph.find(parent, graph.edge[i].src);
			int y = graph.find(parent, graph.edge[i].dest);
			
			if (x == y)
				return 1;
			
			graph.Union(parent, x, y);
		}
		return 0;
	}
	
	
	
	public static void main (String[] args)
    {
        /* Let us create following graph
         0
        |  \
        |    \
        1-----2 */
        int V = 3, E = 3;
        Graph graph = new Graph(V, E);
 
        // add edge 0-1
        graph.edge[0].src = 0;
        graph.edge[0].dest = 1;
 
        // add edge 1-2
        graph.edge[1].src = 1;
        graph.edge[1].dest = 2;
 
        // add edge 0-2
        graph.edge[2].src = 0;
        graph.edge[2].dest = 2;
 
        if (graph.isCycle(graph)==1)
            System.out.println( "graph contains cycle" );
        else
            System.out.println( "graph doesn't contain cycle" );
    }
	
}
```

The implementation of `union()` and `find()` is naive and takes O(n) time in worst case. These methods can be improved to O(logn) using [*Union by Rank or Weight*](http://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/).




## Reference:

1. [Disjoint-set data structre @wiki](https://en.wikipedia.org/wiki/Disjoint-set_data_structure)

2. [A dead simple explaination](https://www.hackerearth.com/notes/disjoint-set-union-union-find/)

   see this to see why we chose to implement union find using parent

3. [Detect cycle in undirected graph](http://www.geeksforgeeks.org/union-find/)

   ​