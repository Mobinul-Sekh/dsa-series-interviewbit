### Q link - https://www.interviewbit.com/problems/occurence-of-each-number/

> **Note:-**
> 1. Just a simple ordered map problem.

**Approach:-**
1. Store the number's with frequency in a ordered map, As the ordered map stores the elements in order so, take out frequencies and push to the answer array.

**T.C & S.C:-**  
```
Time Complexity - O(NlogN) 
Space Complexity - O(N)
```

**Code:-**
```c++
vector<int> Solution::findOccurrences(vector<int> &A) {
    map<int, int> mp;
    for(auto &x : A){
        mp[x]++;
    }
    vector<int> ans;
    for(auto &x : mp){
        ans.push_back(x.second);
    }
    return ans;
}

```