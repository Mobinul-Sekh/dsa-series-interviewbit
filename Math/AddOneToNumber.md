### Q link - https://www.interviewbit.com/problems/add-one-to-number/

**Approach:-**  
1. Start from the end of the array and add carry(initially take carry 1), then keep track of carry and remainder, update the answer array with remainder till the first element.
2. If the carry is still 1, push 1 to the answer array.
3. Remove all the trailing zeros, and return reversed array.

**T.C & S.C:-**  
```
Time Complexity - O(N) 
Space Complexity - O(1)
```

**Code:-**
```c++
vector<int> Solution::plusOne(vector<int> &A) {
    int carry = 1;
    int n = A.size();
    vector<int> ans;
    if (n == 1 && A[0] == 0) {
        return {1};
    }
    
    for (int i=n-1; i>=0; i--) {
        int afterAddition = A[i] + carry;
        int rem = afterAddition%10;
        carry = afterAddition/10;
        ans.push_back(rem);
    }
    
    if (carry == 1) {
        ans.push_back(1);
    }
    
    while (ans[ans.size()-1] == 0) {
        ans.pop_back();
    }
    
    reverse(ans.begin(), ans.end());
    return ans;
}

```