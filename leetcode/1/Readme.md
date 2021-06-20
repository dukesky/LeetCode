# [307. Range Sum Query - Mutable (Medium)](https://leetcode.com/problems/range-sum-query-mutable/solution/)

<p>Given an integer array <code>nums</code>, handle multiple queries of the following types:</p>

<ol>
	<li><strong>Update</strong> the value of an element in <code>nums</code>.</li>
	<li>Calculate the <strong>sum</strong> of the elements of <code>nums</code> between indices <code>left</code> and <code>right</code> <strong>inclusive</strong> where <code>left &lt;= right</code>.</li>
</ol>

<p>Implement the <code>NumArray</code> class:</p>

<ul>
	<li><code>NumArray(int[] nums)</code> Initializes the object with the integer array <code>nums</code>.</li>
	<li><code>void update(int index, int val)</code> <strong>Updates</strong> the value of <code>nums[index]</code> to be <code>val</code>.</li>
	<li><code>int sumRange(int left, int right)</code> Returns the <strong>sum</strong> of the elements of <code>nums</code> between indices <code>left</code> and <code>right</code> <strong>inclusive</strong> (i.e. <code>nums[left] + nums[left + 1] + ... + nums[right]</code>).</li>
</ul>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input</strong>
["NumArray", "sumRange", "update", "sumRange"]
[[[1, 3, 5]], [0, 2], [1, 2], [0, 2]]
<strong>Output</strong>
[null, 9, null, 8]

<strong>Explanation</strong>
NumArray numArray = new NumArray([1, 3, 5]);
numArray.sumRange(0, 2); // return 1 + 3 + 5 = 9
numArray.update(1, 2);   // nums = [1, 2, 5]
numArray.sumRange(0, 2); // return 1 + 2 + 5 = 8
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>-100 &lt;= nums[i] &lt;= 100</code></li>
	<li><code>0 &lt;= index &lt; nums.length</code></li>
	<li><code>-100 &lt;= val &lt;= 100</code></li>
	<li><code>0 &lt;= left &lt;= right &lt; nums.length</code></li>
	<li>At most <code>3 * 10<sup>4</sup></code> calls will be made to <code>update</code> and <code>sumRange</code>.</li>
</ul>


**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon)

**Related Topics**:  
[Binary Indexed Tree](https://leetcode.com/tag/binary-indexed-tree/), [Segment Tree](https://leetcode.com/tag/segment-tree/)

**Similar Questions**:
* [Range Sum Query - Immutable (Easy)](https://leetcode.com/problems/range-sum-query-immutable/)
* [Range Sum Query 2D - Mutable (Hard)](https://leetcode.com/problems/range-sum-query-2d-mutable/)

## Solution 1.

```python
    def __init__(self, nums):
        # self.nums = nums
        self.n = len(nums)
        self.tree = [0] * 2*self.n
        for i in range(0,self.n):
            self.tree[self.n+i] = nums[i]
        for i in range(len(nums)-1,0,-1):
            self.tree[i] = self.tree[i*2] + self.tree[i*2+1]
            
    def update(self,index, val):
        diff = val - self.tree[self.n+index]
        idx = self.n + index
        while idx > 0:
            self.tree[idx] += diff
            idx = idx // 2
        
    def sumRange(self, left, right):
        left += self.n
        right += self.n
        result = 0
        while left <= right:
            if left % 2 == 1:
                result += self.tree[left]
                left += 1
            if right % 2  == 0:
                result += self.tree[right]
                right -= 1
            left //= 2
            right //= 2
        return result
```