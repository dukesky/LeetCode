# [926. Flip String to Monotone Increasing (Medium)](https://leetcode.com/problems/flip-string-to-monotone-increasing/)

<p>A binary string is monotone increasing if it consists of some number of <code>0</code>'s (possibly none), followed by some number of <code>1</code>'s (also possibly none).</p>

<p>You are given a binary string <code>s</code>. You can flip <code>s[i]</code> changing it from <code>0</code> to <code>1</code> or from <code>1</code> to <code>0</code>.</p>

<p>Return <em>the minimum number of flips to make </em><code>s</code><em> monotone increasing</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "00110"
<strong>Output:</strong> 1
<strong>Explanation:</strong> We flip the last digit to get 00111.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "010110"
<strong>Output:</strong> 2
<strong>Explanation:</strong> We flip to get 011111, or alternatively 000111.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> s = "00011000"
<strong>Output:</strong> 2
<strong>Explanation:</strong> We flip to get 00000000.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>5</sup></code></li>
	<li><code>s[i]</code> is either <code>'0'</code> or <code>'1'</code>.</li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon)

**Related Topics**:  
[String](https://leetcode.com/tag/string/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

## Solution 1.

```py
class Solution:
    def minFlipsMonoIncr(self, s: str) -> int:
        
        ## defind a split point, left are all '0', right are all '1', iterate split point from left(0) to right (n), calculate each split point, how many split needed. 
        ## to calculate this, we need to know in advance how many 0,1 in the whole string and how many in the left of split point
        total,total_1 = len(s),0
        for char in s:
            if char=='1':
                total_1 += 1
        total_0 = total - total_1
        if total_0 == total or total_1 == total:
            return 0
        min_flip = min(total_0,total_1)
        cur_1 = 0
        for i in range(0,len(s)): 
            if s[i] == '1':
                cur_1 += 1
            n_flip = cur_1 + len(s) - (i + 1) - (total_1 - cur_1)
            if n_flip < min_flip:
                min_flip = n_flip
        return min_flip
```