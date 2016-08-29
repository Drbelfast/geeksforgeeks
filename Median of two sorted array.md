1. Assume we have two arrays `a1` and `a2`. and `a1.length >= a2.length`

2. Find median of `a1` and `a2` separately, which will be marked as `m1`, `m2`

   1. if `m1 == m2`

      This is the median of two arrays. return

   2. if `m1 > m2`

      The median will only show up in `a1[0] ~ m1` and `m2 ~ a2[lastIndex]`

   3. if `m1 < m2`

      The median will only show up in `m1 ~ a1[lastIndex]` and `a2[0] ~ m2`

```java
public double findMedianSortedArrays(int A[], int B[]) {  
    if((A.length+B.length)%2==1)  
        return helper(A,B,0,A.length-1,0,B.length-1,(A.length+B.length)/2+1);  
    else  
        return (helper(A,B,0,A.length-1,0,B.length-1,(A.length+B.length)/2)    
               +helper(A,B,0,A.length-1,0,B.length-1,(A.length+B.length)/2+1))/2.0;  
}  
private int helper(int A[], int B[], int i, int i2, int j, int j2, int k)  
{  
    int m = i2-i+1;  
    int n = j2-j+1;  
    if(m>n)  
        return helper(B,A,j,j2,i,i2,k); // always assume a.length < b.length 
    if(m==0)  
        return B[j+k-1];  
    if(k==1)  
        return Math.min(A[i],B[j]);  
    int posA = Math.min(k/2,m); // k / 2 > m could happen
    int posB = k-posA;  
    if(A[i+posA-1]==B[j+posB-1])  
        return A[i+posA-1];  
    else if(A[i+posA-1]<B[j+posB-1])  
        return helper(A,B,i+posA,i2,j,j+posB-1,k-posA);  
    else  
        return helper(A,B,i,i+posA-1,j+posB,j2,k-posB);  
}  
```



Similar questions:

1. we have `m` sorted arrays with size `n` . Find the top K element, `k > m && k > n`

   ​