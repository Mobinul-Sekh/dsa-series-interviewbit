### Q link - https://www.interviewbit.com/problems/flip/

> **Note:-**
> 1. This is a very good question, if you don't know the trick than it can be very hard to solve.

**Approach:-**  
1. Convert all to 0s to 1 and 1s to -1, one edge case while converting check if the all numbers are 1 or not if yes than we already have the max.
2. After converting the number this problem become a Kadane's Algorithms application problem.
3. Apply Kadane's Algorithm, but we have know when to store the range, as Kadane's algorithm tracks max sub-array sum at that index so, when we get a better sum we will directly store the right range(R) which will be current index in the resultant array, and for the left range(L), we will keep a variable and update it with current index where ever we reset the sum, but will store it in the resultant array when we are store the R.

**T.C & S.C:-**  
```
Time Complexity - O(N) 
Space Complexity - O(1)
```

#### Best resource - https://www.youtube.com/watch?v=Etkf8sRQdbU

**Code:-**
```c++
vector<int> Solution::flip(string A) {
    bool isMaxed = true;
    vector<int> ans(2);
    
    for (int i=0; i<A.size(); i++) {
        if (A[i] == '0') {
            A[i] = 1;
            isMaxed = false;
        } else {
            A[i] = -1;
        }
    }
    
    if (isMaxed) {
        return {};
    }
    
    int currSum = 0;
    int maxSum = 0;
    int left = 0;
    
    for (int i=0; i<A.size(); i++) {
        currSum += A[i];
        
        if (currSum > maxSum) {
            maxSum = currSum;
            ans[0] = left+1;
            ans[1] = i+1;
        }
        if (currSum < 0) {
            currSum = 0;
            left = i+1;
        }
    }
    
    return ans;
}
```