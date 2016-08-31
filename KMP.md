---
title: A&DS-KMP
date: 2016-08-15 22:21:58
tags:
categories: Algorithm
---
2 stages:
1. prefix function
2. String matching


**prefix:** All the characters in a string with one or more cut off the end

**suffix:** All the characters in a string, with one ore more cut off the beginning

The values in the prefix table are:

The length of the longest proper prefix that matches a proper suffix in the same subpatter.



The key is to build the pre-fix table of pattern so that It can skip several letters when it has same prefix and suffix.

But if the pattern has no same subpattern, this is the worst case of KMP and has same Complexity as Naive implemenation.

```java
// practice
For the pattern “AABAACAABAA”, lps[] is [0, 1, 0, 1, 2, 0, 1, 2, 3, 4, 5]
For the pattern “ABCDE”, lps[] is [0, 0, 0, 0, 0]
For the pattern “AAAAA”, lps[] is [0, 1, 2, 3, 4]
For the pattern “AAABAAA”, lps[] is [0, 1, 2, 0, 1, 2, 3]
For the pattern “AAACAAAAAC”, lps[] is [0, 1, 2, 0, 1, 2, 3, 3, 3, 4]
```





function to calculate prefix table

```java
public static int[] computeLPSArray(String pattern) {
		int[] res = new int[pattern.length()];
		
		int j = 0;
		for (int i = 1; i < pattern.length(); i++) {
			while (j > 0 && pattern.charAt(j) != pattern.charAt(i)) {
				j = res[j - 1];
			}
			
			if (pattern.charAt(j) == pattern.charAt(i)) {
				j++;
			}
			res[i] = j;
		}
		return res;
		
	}
```

and the KMP search

```java
public static void KMPSearch(String pattern, String text) {
		int M = pattern.length();
		int N = text.length();
		
		// calculate prefix array
		
		int[] lps = computeLPSArray(pattern);
		int i = 0; // index for text;
		int j = 0; // index for pattern;
		
		while (i < N) {
			if (pattern.charAt(j) == text.charAt(i)) {
				i++;
				j++;
			}
			if (j == M) {
				System.out.println("Found pattern at index" +(i - j));
				j = lps[j - 1];
			}
			// mismatch after j matches
			else if (i < N && pattern.charAt(j) != text.charAt(i)) {
				if (j != 0) {
					j = lps[j - 1];
				} else {
					i = i + 1;
				}
			}
		}
	}
```




## Reference:
[The best explanation](https://www.youtube.com/watch?v=5i7oKodCRJo&index=42&list=PLqD_OdMOd_6YixsHkd9f4sNdof4IhIima)
