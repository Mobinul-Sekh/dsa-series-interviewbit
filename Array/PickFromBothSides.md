### Q.
#### Given an integer array A of size N. You have to pick exactly B elements from either left or right end of the array A to get the maximum sum. Find and return this maximum possible sum.
#### NOTE: Suppose B = 4 and array A contains 10 elements then You can pick the first four elements or can pick the last four elements or can pick 1 from the front and 3 from the back etc.
#### you need to return the maximum possible sum of elements you can pick.

#### link - https://www.interviewbit.com/problems/pick-from-both-sides/

> **Note:-**
> 1. First time solving this type of question, this one is very unique problem.
> 1. We have to solve this problem using prefix sum and suffix sum.
> 2. But it is not like normal prefix sum suffix sum problem, it's more like circular prefix sum and suffix sum.

**Approach:-**
1. First store 0th to Bth prefix sum in a variable.
2. Store that prefix sum as answer, and try to find larger sum than that from the right side.
3. To do that take out one element by one element from the prefix sum and put in elements from right most side of the array.
4. Keep tracking the max sum.
5. return max sum.

**Dry Rum:-**
> A = [5 -2 3 1 3], B = 3  
> preSum = sum(A[0, 3]) = 5 + (-2) + 3 = 6  
> ans = 6  
> 1st iteration, ans = max(6-3(B-i th index)+3(last index), 6) = 6  
> 2nd iteration, ans = max(6-(-2), 6) = 8
> 3rd/last iteration, ans = max(8-5, 8) = 8
> final answer - 8

**T.C & S.C:-**  
```
Time Complexity - O(B) 
Space Complexity - O(1)
```

**Code:-**
```javascript
solve : function(A, B){
    let preSum = 0;
    let n = A.length;
    
    for (let i=0; i<B; i++) {
        preSum += A[i];
    }
    
    let ans = preSum;
    
    for (let i=1; i<=B; i++) {
        preSum = preSum - A[B-i] + A[n-i];
        ans = Math.max(preSum, ans);
    }
    
    return ans;
}
```