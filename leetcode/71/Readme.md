# [330. Patching Array (Hard)](https://leetcode.com/problems/patching-array/)

<p>Given a sorted integer array <code>nums</code> and an integer <code>n</code>, add/patch elements to the array such that any number in the range <code>[1, n]</code> inclusive can be formed by the sum of some elements in the array.</p>

<p>Return <em>the minimum number of patches required</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,3], n = 6
<strong>Output:</strong> 1
Explanation:
Combinations of nums are [1], [3], [1,3], which form possible sums of: 1, 3, 4.
Now if we add/patch 2 to nums, the combinations are: [1], [2], [3], [1,3], [2,3], [1,2,3].
Possible sums are 1, 2, 3, 4, 5, 6, which now covers the range [1, 6].
So we only need 1 patch.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [1,5,10], n = 20
<strong>Output:</strong> 2
Explanation: The two patches can be [2, 4].
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> nums = [1,2,2], n = 5
<strong>Output:</strong> 0
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 1000</code></li>
	<li><code>1 &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
	<li><code>nums</code> is sorted in <strong>ascending order</strong>.</li>
	<li><code>1 &lt;= n &lt;= 2<sup>31</sup> - 1</code></li>
</ul>


**Companies**:  
[Google](https://leetcode.com/company/google)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Greedy](https://leetcode.com/tag/greedy/)

**Similar Questions**:
* [Maximum Number of Consecutive Values You Can Make (Medium)](https://leetcode.com/problems/maximum-number-of-consecutive-values-you-can-make/)

## Solution 1.

```py
class Solution:
    def minPatches(self, nums: List[int], n: int) -> int:
        
        
        ## to detect if could form nums from 1 to n, 
        ## shortest 1,2,4,8,16,..   1,2,3,4,5,6,7,8,9,10,11,..31
        ## if 1,7,26 --> 31   2,4,
        ## go through each element, to get the max total can reach with this element added, if there's a gap, add gap number
        ## exp1: [1,   5,10] 
        ## add      2,4
        ## max    1,3,7,12,22
        ## exp2: [1,   5,8,   34] n = 90
        ## add      2,4,      21,42,84
        ## max    1,3,7,12,20,41,83,167
        
        cur_max = 0
        added = 0
        pt = 0
        while pt < len(nums) and cur_max < n :
            if nums[pt]<= cur_max+1:
                cur_max += nums[pt]
                pt += 1
            else:
                added += 1
                cur_max = cur_max*2 + 1
                 
        while cur_max< n:
            added += 1
            cur_max = cur_max*2+1
            
        return added
```