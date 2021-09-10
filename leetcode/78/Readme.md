# [446. Arithmetic Slices II - Subsequence (Hard)](https://leetcode.com/problems/arithmetic-slices-ii-subsequence/solution/)

<p>Given an integer array <code>nums</code>, return <em>the number of all the <strong>arithmetic subsequences</strong> of</em> <code>nums</code>.</p>

<p>A sequence of numbers is called arithmetic if it consists of <strong>at least three elements</strong> and if the difference between any two consecutive elements is the same.</p>

<ul>
	<li>For example, <code>[1, 3, 5, 7, 9]</code>, <code>[7, 7, 7, 7]</code>, and <code>[3, -1, -5, -9]</code> are arithmetic sequences.</li>
	<li>For example, <code>[1, 1, 2, 5, 7]</code> is not an arithmetic sequence.</li>
</ul>

<p>A <strong>subsequence</strong> of an array is a sequence that can be formed by removing some elements (possibly none) of the array.</p>

<ul>
	<li>For example, <code>[2,5,10]</code> is a subsequence of <code>[1,2,1,<strong><u>2</u></strong>,4,1,<u><strong>5</strong></u>,<u><strong>10</strong></u>]</code>.</li>
</ul>

<p>The test cases are generated so that the answer fits in <strong>32-bit</strong> integer.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [2,4,6,8,10]
<strong>Output:</strong> 7
<strong>Explanation:</strong> All arithmetic subsequence slices are:
[2,4,6]
[4,6,8]
[6,8,10]
[2,4,6,8]
[4,6,8,10]
[2,4,6,8,10]
[2,6,10]
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [7,7,7,7,7]
<strong>Output:</strong> 16
<strong>Explanation:</strong> Any subsequence of this array is arithmetic.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1&nbsp; &lt;= nums.length &lt;= 1000</code></li>
	<li><code>-2<sup>31</sup> &lt;= nums[i] &lt;= 2<sup>31</sup> - 1</code></li>
</ul>


**Companies**:  
[Google](https://leetcode.com/company/google)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

**Similar Questions**:
* [Arithmetic Slices (Medium)](https://leetcode.com/problems/arithmetic-slices/)

## Solution 1.

```py
class Solution:
    def numberOfArithmeticSlices(self, nums: List[int]) -> int:
        
        ## find all arithmetic list, for each list, count total combination O(2^n)
        ## 
        
        
        ## DP  dps[i] is a dictionary what store all key is diff, value is total length of suquence end in nums[i]
        total = 0
        dps = [collections.defaultdict(int) for _ in range(len(nums))]
        for i in range(0,len(nums)):
            for j in range(0,i):
                diff = nums[i] - nums[j]
                dps[i][diff] += 1
                if diff in dps[j]:
                    dps[i][diff] += dps[j][diff]
                    total += dps[j][diff]
        return total
```