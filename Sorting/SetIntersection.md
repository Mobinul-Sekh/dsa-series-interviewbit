### Q link - https://www.interviewbit.com/problems/set-intersection/

#### Note:-
> 1. This problem was challenging to me, as I could not understand :-   
**A.** why we are initializing the 'secondMaxEnd' with end-1?  
**B.** why we are sorting the intervals in the particular way?
> 2. Ans :-  
**A.** As I was mistaken previously the 'secondMaxEnd' is not the left value of the interval, rather it's the second largest right value possible. And we need it because in our question it's stated that we have to have 2 values from each intervals in the intersection set. So, we are tracking the max end and second max end of the previous range, cause in the worst case, the next range's left value (which is the smallest) if bigger than the previous maxEnd means next entire range does not fit-in in our intersection set, in the second worst scenario, the left value is smaller than maxEnd but larger than the secondMaxEnd means at-least we have one value which can be part of our set.  
**B.** From my observation, for this algorithm to work we need to sort the intervals in this particular way, we need to have the bigger left values at the front for correct counting. I could not found more intuitive answer for this.

#### Approach:-
1. Sort the intervals in a way where, if the current right range is equals to the next one, which ever's left range is larger will sit first, else, who's right range is smaller will sit first.
2. Take two variables to track the max end and the second max end of the previous interval.
3. If, current interval's start is greater than the maxEnd, add 2 to the answer as the current interval does not intersect with our current set entirely and we have to add 2 new elements to our set.
4. Else if, current interval's start is lesser than the maxEnd but greater than secondMaxEnd, add 1 to the answer as we have one intersecting value.
5. Else, the entire range is intersecting with out set, so no element need to add.

#### Time Complexity - 
> O(N⋅logN), where, N = intervals.

#### Space Complexity - 
> O(1).

#### Code:-
```c++
bool comparator(vector<int> &a, vector<int> &b) {
    return a[1] == b[1] ? a[0] > b[0] : a[1] < b[1];
}

int Solution::setIntersection(vector<vector<int> > &A) {
    sort(A.begin(), A.end(), comparator);
    
    int maxEnd = -1, secondMaxEnd = -1;
    int ans = 0;
    
    for (auto &vec : A) {
        int start = vec[0], end = vec[1];
        
        if (start > maxEnd) {
            ans += 2;
            // this is the important step to understand, here secondMaxEnd is not the previous range's left value that's why
            // we are not initializing it with 'start' rather it's the second largest right range value (rightRange - 1).
            secondMaxEnd = end - 1;
            maxEnd = end;
        } else if (start > secondMaxEnd) {
            ans += 1;
            secondMaxEnd = maxEnd;
            maxEnd = end;
        }
    }
    
    return ans;
}
```