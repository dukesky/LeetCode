# [611. Valid Triangle Number (Medium)](https://leetcode.com/problems/valid-triangle-number/)

<p>Given an integer array <code>nums</code>, return <em>the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [2,2,3,4]
<strong>Output:</strong> 3
<strong>Explanation:</strong> Valid combinations are: 
2,3,4 (using the first 2)
2,3,4 (using the second 2)
2,2,3
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [4,2,3,4]
<strong>Output:</strong> 4
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 1000</code></li>
	<li><code>0 &lt;= nums[i] &lt;= 1000</code></li>
</ul>


**Companies**:  
[Bloomberg](https://leetcode.com/company/bloomberg), [LinkedIn](https://leetcode.com/company/linkedin), [ByteDance](https://leetcode.com/company/bytedance)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Two Pointers](https://leetcode.com/tag/two-pointers/), [Binary Search](https://leetcode.com/tag/binary-search/), [Greedy](https://leetcode.com/tag/greedy/), [Sorting](https://leetcode.com/tag/sorting/)

**Similar Questions**:
* [3Sum Smaller (Medium)](https://leetcode.com/problems/3sum-smaller/)

## Solution 1.

```python
class Solution:
    def triangleNumber(self, nums: List[int]) -> int:
        
        ## (a(max),b,c(min)) form trangle ==> a<b+c   a>b-c(default)
        ## solution1: brute force, three loop, compared any three pair  O(n^3)
        
        ## better solution
        ## solution2: sorted the nums at first, two loop to choose b and c, a is greate than b,c, use binary search to find the max possible a O(n^2*logn)
        
        ## solution3: maintain three pointer to form a winder, slid in the sorted nums
        if len(nums) < 3:
            return 0
        nums = sorted(nums)
        cnt = 0

        for i in range(0,len(nums)-2):
            if nums[i] == 0:
                continue
            k = i + 2
            for j in range(i+1,len(nums)-1):
                if nums[j] == 0:
                    continue
                while k<len(nums) and nums[k]<nums[i]+nums[j]:
                    k += 1
                cnt += k - j - 1
        return cnt
        
        
```