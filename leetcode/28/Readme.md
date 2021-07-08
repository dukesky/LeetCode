# [718. Maximum Length of Repeated Subarray (Medium)](https://leetcode.com/problems/maximum-length-of-repeated-subarray/solution/)

<p>Given two integer arrays <code>nums1</code> and <code>nums2</code>, return <em>the maximum length of a subarray that appears in <strong>both</strong> arrays</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums1 = [1,2,3,2,1], nums2 = [3,2,1,4,7]
<strong>Output:</strong> 3
<strong>Explanation:</strong> The repeated subarray with maximum length is [3,2,1].
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums1 = [0,0,0,0,0], nums2 = [0,0,0,0,0]
<strong>Output:</strong> 5
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums1.length, nums2.length &lt;= 1000</code></li>
	<li><code>0 &lt;= nums1[i], nums2[i] &lt;= 100</code></li>
</ul>


**Companies**:  
[Karat](https://leetcode.com/company/karat), [Indeed](https://leetcode.com/company/indeed), [Apple](https://leetcode.com/company/apple), [Amazon](https://leetcode.com/company/amazon), [Intuit](https://leetcode.com/company/intuit), [Wayfair](https://leetcode.com/company/wayfair)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Binary Search](https://leetcode.com/tag/binary-search/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/), [Sliding Window](https://leetcode.com/tag/sliding-window/), [Rolling Hash](https://leetcode.com/tag/rolling-hash/), [Hash Function](https://leetcode.com/tag/hash-function/)

**Similar Questions**:
* [Minimum Size Subarray Sum (Medium)](https://leetcode.com/problems/minimum-size-subarray-sum/)

## Solution 1.

```python
class Solution:
    def findLength(self, nums1: List[int], nums2: List[int]) -> int:
        
        ## use DP solution, dps[i][j] represent longest subarray end with nums1[i],nums2[j]
        res = 0
        dps = [[0] * (len(nums2)+1) for _ in range(len(nums1)+1)]
        for i in range(len(nums1)):
            for j in range(len(nums2)):
                if nums1[i] == nums2[j]:
                    dps[i+1][j+1] = dps[i][j] + 1
                    if dps[i+1][j+1] > res:
                        res = dps[i+1][j+1]
                
        return res
        

```