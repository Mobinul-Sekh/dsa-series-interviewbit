### Q. Given a number A. Find the factorial of the number.
#### link - https://www.interviewbit.com/problems/large-factorial

> **Note:-**
> 1. This is a medium level question because of it's implementation.
> 2. This problem is important because, we can not save a large number in normal integer variable so we have to find a way to save the entire number and return it.
> 3. I was confused how the carry can be greater than 9, cause I thought the number we're multiplying are always will be less than 10,  but I soon realize the value of 'i' can go beyond 9, thus carry can be greater than 9.
> 4. Always dry run this for better understanding.

**Approach:-**
1. As the result will be very long so we have to store the result in an array or in a string, I used string.
2. We have to basically breakdown every multiplication step. And we have to store this multiplication results in reverse order.  
ex ->  24 * 5 = 120, should be saved like 0 2 1.
3. Take a 'ans' string variable and pre populate it with one, we will update this variable after every multiplication step.
4. As multiplication step result can be more than single digit so to store it we will use another string variable 'stepAns' and will store the remainder of multiplication steps.
5. Also store the carry and remainder of the multiplication step.
6. Before multiplying make sure to add previous steps carry to it.
7. After each step multiplication update the 'ans' with 'stepAns' and add carry if any.
8. Finally return the reverse 'ans' as answer.

> **T.C & S.C:-**  
> Time Complexity - **O(A^2⋅log(A))**  
> Space Complexity - **O(A⋅log(A))**
>> Because size of 'ans' grows with the number of digits in n!, which is 𝑂(n⋅log(n)) by Stirling's approximation.

#### Best Resource - https://www.youtube.com/watch?v=O3fwYjcMV_M

**Code:-**
```javascript
solve : function(A){
    let ans = "1";
    let carry = 0;
    let multi = 1;
    let rem = 0;
    let stepAns = "";
    
    for (let i=2; i<=A; i++) {
        stepAns = "";
        carry = 0;
        multi = 1;
        rem = 0;
        for (let j=0; j<ans.length; j++) {
            multi = (i*Number(ans[j]))+carry;
            rem = Math.floor(multi%10);
            stepAns += rem.toString();
            carry = Math.floor(multi/10);
        }
        ans = stepAns;
        while (carry > 0) {
            ans += String(Math.floor(carry%10));
            carry = Math.floor(carry/10);
        }
    }
    
    return ans.split("").reverse().join("");
}
```