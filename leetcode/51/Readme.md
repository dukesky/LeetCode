# [90. Subsets II (Medium)](https://leetcode.com/problems/subsets-ii/)

<p>Given an integer array <code>nums</code> that may contain duplicates, return <em>all possible subsets (the power set)</em>.</p>

<p>The solution set <strong>must not</strong> contain duplicate subsets. Return the solution in <strong>any order</strong>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [1,2,2]
<strong>Output:</strong> [[],[1],[1,2],[1,2,2],[2],[2,2]]
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [0]
<strong>Output:</strong> [[],[0]]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10</code></li>
	<li><code>-10 &lt;= nums[i] &lt;= 10</code></li>
</ul>


**Companies**:  
[Apple](https://leetcode.com/company/apple), [Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Bloomberg](https://leetcode.com/company/bloomberg), [ByteDance](https://leetcode.com/company/bytedance)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Backtracking](https://leetcode.com/tag/backtracking/), [Bit Manipulation](https://leetcode.com/tag/bit-manipulation/)

**Similar Questions**:
* [Subsets (Medium)](https://leetcode.com/problems/subsets/)

## Solution 1.

```py
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        
        ## DFS
        ## build a recursion function, go deep level by level untill end, append end to result, for each level, determain if add the number, to determain duplicate number, check previous number, if previous is this number and sol doesn't has this number, not append too
        
        nums = sorted(nums)
        result = []
        
        def helper(nums,level, sol):
            if level == len(nums):
                result.append(list(sol))
                return
            
            if len(sol) != 0 and level != 0 and nums[level] == nums[level-1] and sol[-1] == nums[level]:
                sol.append(nums[level])
                helper(nums,level+1,sol)
                sol.pop()
            else:
                helper(nums,level+1, sol)
                sol.append(nums[level])
                helper(nums, level+1, sol)
                sol.pop()
        
        
        helper(nums,0,[])
        return result
```