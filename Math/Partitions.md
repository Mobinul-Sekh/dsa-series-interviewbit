### Q link - https://www.interviewbit.com/problems/partitions/

> **Note:-**
> 1. I find this problem very interesting, at first we can think that to solve this we have to use some complex method but this problem can be solved with a good mathematical intuitive approach.

**Approach:-**  
1. Calculate the total sum, one_third_sum and two_third_sum of the sum of the array.
2. Traverse the prefix sum array and keep track of the counts of the one_thirds. we will calculate the totalWays using this one_third count.
3. If, the prefix sum is equals to one_third of the total sum increase the one_third counter by one.
3. If, the prefix sum is equals to two_third sum of the total sum, increase the totalWays with one-third count.  
a. Because, if we found the two_third sum also in the array prefix sum that means the third/last part always will be in the rest of the array.  
b. And increasing the totalWays by one_third count because surely we can reach to the two_third sum by that many ways.  
c. Similarly, we increase the totalWays by  one_third count if we found the two_third sum in the array, as that represent the combination of ways.

**T.C & S.C:-**  
```
Time Complexity - O(N) 
Space Complexity - O(1)
```

#### Best Resource - https://www.youtube.com/watch?v=31W_QU1xJcg


**Code:-**
```c++
int Solution::solve(int A, vector<int> &B) {
    int n = B.size();
    int totalSum = 0;
    
    for (int i=0; i<n; i++) {
        totalSum += B[i];
    }
    
    // if not divisible by 3 than can't be partition into 3 equal sum parts.
    if (totalSum % 3 != 0) {
        return 0;
    }
    
    int one_third_sum = totalSum/3;
    int two_third_sum = 2*one_third_sum;
    int one_third_cnt = 0;
    int waysCnt = 0;
    
    int currSum = 0;
    // we can't go till the end to cnt the second part, we have to leave space for thrid part.
    for (int i=0; i<n-1; i++) {
        currSum += B[i];
        
        // if any moment we get the two_third_sum that means we can get here with all one_third_cnt ways.
        if (currSum == two_third_sum) {
            waysCnt += one_third_cnt;
        }
        
        // cnt all the one_third_sums 
        if (currSum == one_third_sum) {
            one_third_cnt += 1;
        }
    }
    
    return waysCnt;
}
```