### Q link - https://www.interviewbit.com/problems/wave-array/

#### Note:-
> 1. One of the easiest problem.

#### Approach:-
1. Sort the array.
2. Swap adjacent elements in pairs.

#### Time Complexity - 
> O(N⋅logN), where, N = no. of elements.

#### Space Complexity - 
> O(1).

#### Code:-
```c++
vector<int> Solution::wave(vector<int> &A) {
    sort(A.begin(), A.end());
    for (int i=0; i<A.size(); i+=2) {
        if (i+1 >= A.size()) {
            break;
        }
        int tmp = A[i];
        A[i] = A[i+1];
        A[i+1] = tmp;
    }
    return A;
}
```