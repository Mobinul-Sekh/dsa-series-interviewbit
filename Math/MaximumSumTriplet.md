### Q link - https://www.interviewbit.com/problems/maximum-sum-triplet/

> **Note:-**
> 1. Never did this kind of problem before, the best approach is interesting.
> 2. For a good approach, we can traverse through two nested loops. While traversing through each number(assume as middle element(Aj)), find maximum number on the of Aj and maximum number(Ak) greater than Aj on the right.
> 3. The time complexity will be O(n^2) and space complexity will be liner.

**Approach:-**  
1. Best and efficient approach is use the concept of maximum suffix-array and binary search/ordered set.
2. For finding maximum number greater than given number beyond it, we can maintain a maximum suffix-array array such that for any number(suffix[i]) it would contain maximum number from index i, i+1, … N-1. Suffix array can be calculated in O(N) time.
3. For finding maximum number smaller than the given number preceding it, we can maintain a sorted list of numbers before a given number such we can simply perform a binary search to find a number which is just smaller than the given number, I used ordered set for that purpose instead of binary search.

**T.C & S.C:-**  
```
Time Complexity - O(NlogN) 
Space Complexity - O(N)
```

#### Best Resource - https://www.youtube.com/watch?v=Ttyr_NCLlYs


**Code:-**
```c++
int Solution::solve(vector<int> &A) {
	int n = A.size();
	vector<int> rightMax = A;
	int ans = 0;
	
	// right side max
	for (int i=n-2; i>=0; i--) {
		rightMax[i] = max(rightMax[i], rightMax[i+1]);
	}
	
	set<int> leftMax;
	// no left element available
	leftMax.insert(A[0]);
    
    // left side max
	for (int i=1; i<n-1; i++) {
		leftMax.insert(A[i]);
		
		// finding out the closest smeller element of A[i], as per the question constraints.
        auto it = leftMax.find(A[i]);
        
        // if the current element is the among all previous left, skip.
        // second condition is to check if the current ele is not equal
        // to it's rightMax, as it has to be lesser than it's rightMax.
        if (it != leftMax.begin() && rightMax[i] != A[i]) {
            ans = max(ans, (*--it) + A[i] + rightMax[i]);
        }
	}
	
	return ans;
}
```