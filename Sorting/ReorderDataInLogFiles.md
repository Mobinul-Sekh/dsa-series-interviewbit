### Q link - https://www.interviewbit.com/problems/reorder-data-in-log-files/

#### Note:-
> 1. This problem is less about DSA and more about array operations problem, I like this problem because this type of the question are the closest to what actually happen in the industry.
> 2. This entire problem depends on the comparator function.

#### Approach:-
1. First separate the array into digital logs array and letter logs array, then sort the letter logs array using custom comparator function according to the constraint.
2. Comparator function steps:  
A. Separate the identifier part and the log part for both strings.  
B. If the log part in equal then sort by the identifier part. Else sort normally by the log part.

#### T.C & S.C:-  
**Time Complexity -** 
1. Separation of Logs:  
Iterating through all logs in A to separate letter logs and digit logs.  
Time Complexity: O(N), where 𝑁 is the number of logs in the input vector.

2. Sorting Letter Logs:  
Sorting uses the comparator function:  
Sorting complexity is O(L⋅logL), where  L is the number of letter logs.

3. For each comparison:  
Splitting a log into identifier and content is O(K), where K is the average length of a log.  
Total cost for sorting: O(L⋅K⋅logL).

4. Appending Digit Logs:  
Appending all digit logs to the result.  
Time Complexity: O(D), where D is the number of digit logs.

Overall Time Complexity:  
O(N)+O(L⋅K⋅logL)+O(D).  
Since,  
N=L+D, the final complexity is: O(N+N⋅K⋅logN).
For K bounded by a constant (average length of logs),
the complexity simplifies to **O(N⋅logN)**.

**Space Complexity - O(N)**

#### Code:-
```c++
// this function is the most important part of the problem.
bool comparetor(string &str1, string &str2) {
    string log1, log2;
    string id1, id2;
    
    int i=0;
    while (str1[i] != '-') {
        i++;
    }
    log1 = str1.substr(i+1);
    id1 = str1.substr(0, i-1);
    
    i=0;
    while (str2[i] != '-') {
        i++;
    }
    log2 = str2.substr(i+1);
    id2 = str2.substr(0, i-1);
    
    if (log1 == log2) {
        return id1 < id2;
    } else {
        return log1 < log2;
    }
}

vector<string> Solution::reorderLogs(vector<string> &A) {
    vector<string> letterLogs, digitLogs;
    
    for (auto &log : A) {
        if (log[log.size()-1] >= 'a' && log[log.size()-1] <= 'z') {
            letterLogs.push_back(log);
        } else {
            digitLogs.push_back(log);
        }
    }
    
    sort(letterLogs.begin(), letterLogs.end(), comparetor);
    
    for (auto &log : digitLogs) {
        letterLogs.push_back(log);
    }
    
    return letterLogs;
}
```