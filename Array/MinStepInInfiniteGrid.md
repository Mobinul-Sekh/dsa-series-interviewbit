### Q link - https://www.interviewbit.com/problems/min-steps-in-infinite-grid/

> **Note:-**
> 1. This is a very misleading problem, interviewer can ask this problem to confuse you to think of a hard graph approach but reality is different.
> 2. This problem's solution follows a very particular formula, and the solution code is very easy one, but the tricky part is to explain it why it's work.

**Approach:-**
1. As we are allowed to traverse any direction of 8, so the shortest path b/t to points will always be the diagonal one, if the other point has not exists in exact diagonal of first point, then we will traverse diagonally to the nearest x-axis or y-axis then we can go along with that axis.
2. This distance happens to be equals to -> max(abs(x1 - x2), abs(y1 - y2)), where (x1, y1) is the coordinate of p1 and (x2, y2) is the coordinate of p2, draw a plot to better understand and better explain.

**T.C & S.C:-**  
```
Time Complexity - O(N) 
Space Complexity - O(1)
```

***Best Resource***
1. https://www.youtube.com/watch?v=tiUHfhJYKdU
2. https://www.youtube.com/watch?v=UHjs6iTqLAE&t=236s

**Code:-**
```javascript
coverPoints : function(A, B){
    const n = A.length;
    let totalDistance = 0;
    
    for (let i=0; i<n-1; i++) {
        // this variable initialization can be avoided for space optimization.
        let p1 = [A[i], B[i]]
        let p2 = [A[i+1], B[i+1]]
        
        totalDistance += Math.max(Math.abs(p1[0] - p2[0]), Math.abs(p1[1] - p2[1]));
    }
    
    return totalDistance;
}
```