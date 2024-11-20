### Q link - https://www.interviewbit.com/problems/max-sum-contiguous-subarray/

> **Note:-**
> 1. Just basic application of Kadane's Algorithm, to solve you have to remember the algorithm and implementation.

**Approach:-**  
1. The idea of Kadane’s algorithm is to traverse over the array from left to right and for each element, find the maximum sum among all subarrays ending at that element. The result will be the maximum of all these values.
2. But, the main issue is how to calculate maximum sum among all the subarrays ending at an element in O(1) time?
3. To calculate the maximum sum of subarray ending at current element, say maxEnding, we can use the maximum sum ending at the previous element. So for any element, we have two choices:
4. Choice 1: Extend the maximum sum subarray ending at the previous element by adding the current element to it. If the maximum subarray sum ending at the previous index is positive, then it is always better to extend the subarray.
5. Choice 2: Start a new subarray starting from the current element. If the maximum subarray sum ending at the previous index is negative, it is always better to start a new subarray from the current element.
This means that maxEnding at index i = max(maxEnding at index (i – 1) + arr[i], arr[i]) and the maximum value of maxEnding at any index will be our answer. 

**T.C & S.C:-**  
```
Time Complexity - O(N) 
Space Complexity - O(1)
```

**Code:-**
```c++
int Solution::maxSubArray(const vector<int> &A) {
    int sum = A[0];
    int maxSum = sum;
    for (int i=1; i<A.size(); i++) {
        sum = max(A[i], sum + A[i]);
        maxSum = max(sum, maxSum);
    }
    return maxSum;
}

```