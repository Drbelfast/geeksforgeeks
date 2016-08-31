---
title: A&DS-Dijsktra's algorithm
date: 2016-08-11 22:23:00
tags:
categories: Algorithm
---

Dijsktra's algorithm is very similar to prim's algorithm except that when update adjacent node's value, Dijsktra updates the value as the sume of path, and prim just updates the weight of that edge.


In other words:

Dijsktra's algorithm finds the minimum distance **from node i to all nodes** (you specify i). So in return you get the minimum distance tree from node i.

Prims algorithm gets you the minimum spaning tree **for a given graph**. A tree that connects all nodes while the sum of all costs is the minimum possible.

So with Dijkstra **you can go from the selected node to any other with the minimum cost**, you don't get this with Prim's