### Q link - https://www.interviewbit.com/problems/minimum-lights-to-activate/

> **Note:-**
> 1. A very good practical problem.

**Approach:-**  
1. Starting from 0th corridor find the rightmost functional light within the light's range (X-B+1 to X+B-1).
2. If we don't find any means that section of the corridor can't be lighten, so return -1.
3. Else jump to B-1 (light's range) corridor to the rightmost light's right side, as the light can lighten those section as it is under it's range, also update the light on count (cnt) by +1.
4. Then keep searching rightmost functional lights within range and repeat step 2 and 3.

**T.C & S.C:-**  
```
Time Complexity - O(N) 
Space Complexity - O(1)
```

**Code:-**
```javascript
solve : function(A, B){
    let i = 0;
    let cnt = 0;
    while (i < A.length) {
        let rightMost = -1;
        for (let j=Math.max(0,i-B+1); j<=Math.min(i+B-1, A.length-1); j++) {
            if (A[j] === 1) {
                rightMost = j;
            }
        }
        if (rightMost === -1) {
            return -1;
        }
        cnt += 1;
        i = rightMost+B;
    }
    
    return cnt;
}
```