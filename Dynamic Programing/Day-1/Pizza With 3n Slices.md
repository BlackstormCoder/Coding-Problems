##  Pizza With 3n Slices
There is a pizza with 3n slices of varying size, you and your friends will take slices of pizza as follows:

You will pick any pizza slice.
Your friend Alice will pick the next slice in the anti-clockwise direction of your pick.
Your friend Bob will pick the next slice in the clockwise direction of your pick.
Repeat until there are no more slices of pizzas.
Given an integer array slices that represent the sizes of the pizza slices in a clockwise direction, return the maximum possible sum of slice sizes that you can pick.

 
## Example 1


```bash
Input: slices = [1,2,3,4,5,6]
Output: 10
Explanation: Pick pizza slice of size 4, Alice and Bob will pick slices with size 3 and 5 respectively. Then Pick slices with size 6, finally Alice and Bob will pick slice of size 2 and 1 respectively. Total = 4 + 6.


Input: slices = [8,9,8,6,1,1]
Output: 16
Explanation: Pick pizza slice of size 8 in each turn. If you pick slice with size 9 your partners will pick slices of size 8.
```
## Solution 1 (recursion)
```Python
class Solution:
    def maxSizeSlices(self, slices: List[int]) -> int:
        
        k = len(slices)
        case1 = self.solve(0,k-2,slices,k/3)
        case2 = self.solve(1,k-1,slices,k/3)
        
        return max(case1,case2)
    
    def solve(self,index,n,slices,step):
        
        if step==0 or index>n:
            return 0
        
        include = slices[index] + self.solve(index+2,n,slices,step-1)
        
        exclude = 0 + self.solve(index+1,n,slices,step)
        
        return max(include,exclude)

    
```
```bash
Time Complexity : O(2^n)
Space Complexity : O(n) --> Recursion Stack space
```
## Solution 2 (memoiation)
```python

class Solution:
    def maxSizeSlices(self, slices: List[int]) -> int:
        
        k = len(slices)
        
        dp1 = [[-1 for _ in range(k)]for __ in range(k)]     
        dp2 = [[-1 for _ in range(k)]for __ in range(k)]
        
        case1 = self.solve(0,k-2,slices,int(k/3),dp1)
        case2 = self.solve(1,k-1,slices,int(k/3),dp2)
        
        return max(case1,case2)
    
    def solve(self,index,n,slices,step,dp):
        
        if step==0 or index>n:
            return 0
        
        if dp[index][step] != -1:
            return dp[index][step]
        
        include = slices[index] + self.solve(index+2,n,slices,step-1,dp)
        
        exclude = 0 + self.solve(index+1,n,slices,step,dp)
        
        dp[index][step] = max(include,exclude)
        
        return dp[index][step]

        
```
## Solution 3 (Tabulation)
```python

class Solution:
    def maxSizeSlices(self, slices: List[int]) -> int:
        
        k = len(slices)
        n = int(k/3)
        
        dp1 = [[-1 for _ in range(k+2)]for __ in range(k+2)]
        dp2 = [[-1 for _ in range(k+2)]for __ in range(k+2)]
        
        for i in range(k-2,-1,-1):
            for j in range(1,n+2):
                
                include = slices[i] + dp1[i+2][j-1]
                exclude = 0 + dp1[i+1][j]
                
                dp1[i][j] =max(include,exclude)
        
        case1 = dp1[0][n]
                
        for i in range(k-1,0,-1):
            for j in range(1,n+2):
                
                include = slices[i] + dp2[i+2][j-1]
                exclude = 0 + dp2[i+1][j]
                
                dp2[i][j] = max(include,exclude)  
        
        case2 = dp2[1][n]
        
        ans =  max(case1,case2) + 1
        
        return ans
        
```

```bash
Time Complexity : O(n^2)
Space Complexity : O(n)
```
## LeetCode
[Pizza With 3n Slices](https://leetcode.com/problems/pizza-with-3n-slices/)
