---
title: A&DS-Topological Sort
date: 2016-08-08 15:28:00
tags:
categories: Algorithm
---
One application is *Builder System*, where each package has to wait for all its dependencies to finish building.
A digraph has a topological sort if and only if it is a DAG(Directed Acyclic Graph)

Reverse postorder in a DAG is a topological sort. see Algorithm 4th edition P579