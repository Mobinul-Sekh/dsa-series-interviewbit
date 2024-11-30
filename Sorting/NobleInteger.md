### Q link - https://www.interviewbit.com/problems/noble-integer/

> **Note:-**
> 1. Pretty straight forward sorting problem.

**Approach:-**
1. Sort the array, check every number if it satisfy the given constraint or not.
2. Remember to check for the equal numbers, if equal number skip them then check the constraint.

**T.C & S.C:-**  
```
Time Complexity - O(NlogN) 
Space Complexity - O(1)
```

**Code:-**
```c++
int Solution::solve(vector<int> &A) {
    int n = A.size();
    sort(A.begin(), A.end());
    
    for (int i=0; i<n; i++) {
        if (i != n-1 && A[i] == A[i+1]) {
            continue;
        }
        if (A[i] == n - 1 - i) {
            return 1;
        }
    }
    
    return -1;
}
```