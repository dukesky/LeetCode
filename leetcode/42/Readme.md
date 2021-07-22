# [915. Partition Array into Disjoint Intervals (Medium)](https://leetcode.com/problems/partition-array-into-disjoint-intervals/)

<p>Given an array <code>nums</code>, partition it&nbsp;into two (contiguous) subarrays&nbsp;<code>left</code>&nbsp;and <code>right</code>&nbsp;so that:</p>

<ul>
	<li>Every element in <code>left</code>&nbsp;is less than or equal to every element in <code>right</code>.</li>
	<li><code>left</code> and <code>right</code> are non-empty.</li>
	<li><code>left</code>&nbsp;has the smallest possible size.</li>
</ul>

<p>Return the <strong>length</strong> of <code>left</code> after such a partitioning.&nbsp; It is guaranteed that such a partitioning exists.</p>

<p>&nbsp;</p>

<p><strong>Example 1:</strong></p>

<pre><strong>Input: </strong>nums = <span id="example-input-1-1">[5,0,3,8,6]</span>
<strong>Output: </strong><span id="example-output-1">3</span>
<strong>Explanation: </strong>left = [5,0,3], right = [8,6]
</pre>

<div>
<p><strong>Example 2:</strong></p>

<pre><strong>Input: </strong>nums = <span id="example-input-2-1">[1,1,1,0,6,12]</span>
<strong>Output: </strong><span id="example-output-2">4</span>
<strong>Explanation: </strong>left = [1,1,1,0], right = [6,12]
</pre>

<p>&nbsp;</p>
</div>

<p><strong>Note:</strong></p>

<ol>
	<li><code>2 &lt;= nums.length&nbsp;&lt;= 30000</code></li>
	<li><code>0 &lt;= nums[i] &lt;= 10<sup>6</sup></code></li>
	<li>It is guaranteed there is at least one way to partition <code>nums</code> as described.</li>
</ol>

<div>
<div>&nbsp;</div>
</div>


**Companies**:  
[Microsoft](https://leetcode.com/company/microsoft)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/)

## Solution 1.

```py
class Solution:
    def partitionDisjoint(self, nums: List[int]) -> int:
        
        ## T:O(n)
        ## build two list, one track the max number from 0 to i, one track the min number from len(num) to i, the seperate point would be the position where left_max_number < right_min_number
        max_from_left,min_from_right = [nums[0]]*len(nums),[nums[-1]]*len(nums)

        for i in range(1,len(nums)):
            if nums[i] > max_from_left[i-1]:
                max_from_left[i] = nums[i]
            else:
                max_from_left[i] = max_from_left[i-1]
        for i in range(len(nums)-2,-1,-1):
            if nums[i] < min_from_right[i+1]:
                min_from_right[i] = nums[i]
            else:
                min_from_right[i] = min_from_right[i+1]
        for i in range(len(nums)-1):
            if max_from_left[i] <= min_from_right[i+1]:
                return i+1
        

```