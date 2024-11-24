### Q link - https://www.interviewbit.com/problems/maximum-absolute-difference/

> **Note:-**
> 1. This is more of a mathematical question than DSA.
> 2. Code is easy but have to explain why it's happening.


**Approach:-**  
1. If we expand | A[i] - A[j] | + | i - j |, we will have 4 cases,  
**case 1 ->** where (A[i] - A[j]) is positive and (i - j) also positive, **(A[i] - A[j]) + (i - j)**.  
**case 2 ->** where (A[i] - A[j]) and (i - j) both negative, -(A[i] - A[j]) - (i - j).  
or, as we will only consider the value not sign, so we can do a whole negation of this expression, so, **(A[i] - A[j]) + (i - j)**, which is equals to case 1.  
**case 3 ->** (A[i] - A[j]) is negative and (i - j) is positive,  
-(A[i] - A[j]) + (i - j).  
or, **(A[i] - A[j]) - (i - j)**, after doing whole negation.  
**case 4 ->** (A[i] - A[j]) is positive and (i - j) is negative, **(A[i] - A[j]) - (i - j)**, which is equals to case 3.
2. we can see out of the 4 cases we are getting 2 unique cases.
3. so we have to traverse through the array and find out the maximum and minimum for those expression, and will store the maxValue of those expressions by doing max - min.
4. At the end will return the maximum of the two maxValues.

**T.C & S.C:-**  
```
Time Complexity - O(N) 
Space Complexity - O(1)
```

#### Best Resource - https://www.youtube.com/watch?v=KqDIeQ9S5Vc&t=444s

**Code:-**
```c++
int Solution::maxArr(vector<int> &A) {
    int maxI = INT_MIN, maxJ = INT_MIN;
    int minI = INT_MAX, minJ = INT_MAX;
    
    for (int i=0; i<A.size(); i++) {
        maxI = max(A[i] + (i+1), maxI);
        minI = min(A[i] + (i+1), minI);
        
        maxJ = max(A[i] - (i+1), maxJ);
        minJ = min(A[i] - (i+1), minJ);
    }
    
    return max(maxI - minI, maxJ - minJ);
}

```