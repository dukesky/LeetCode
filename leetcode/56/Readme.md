# [132. Palindrome Partitioning II (Hard)](https://leetcode.com/problems/palindrome-partitioning-ii/)

<p>Given a string <code>s</code>, partition <code>s</code> such that every substring of the partition is a palindrome.</p>

<p>Return <em>the minimum cuts needed</em> for a palindrome partitioning of <code>s</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "aab"
<strong>Output:</strong> 1
<strong>Explanation:</strong> The palindrome partitioning ["aa","b"] could be produced using 1 cut.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "a"
<strong>Output:</strong> 0
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> s = "ab"
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 2000</code></li>
	<li><code>s</code> consists of lower-case English letters only.</li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Bloomberg](https://leetcode.com/company/bloomberg)

**Related Topics**:  
[String](https://leetcode.com/tag/string/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

**Similar Questions**:
* [Palindrome Partitioning (Medium)](https://leetcode.com/problems/palindrome-partitioning/)
* [Palindrome Partitioning IV (Hard)](https://leetcode.com/problems/palindrome-partitioning-iv/)

## Solution 1.

```py
class Solution:
    def minCut(self, s: str) -> int:
        
        ## brute force
        ## 'aaabbbaaa'
        ## 'abaaba'
        ## 'abbaab'
        def isPalindorme(s):
            if s == s[::-1]:
                return True
            else:
                return False
        
        ## DP: dp[i] in the total split for s[:i+1]
        ## dp[i] = dp[i-j] + 1 if s[j+1:i+1] is panlindorm 
        ## loop from dp[0] to dp[n] --> N time, in each loop, check all previous status --> N time, in each check, check a panlidorm from previous status to current status, N time, total O(N^3)
        dp = [-1,0]
        for i in range(1,len(s)):
            min_split = float('inf')
            for j in range(0,len(dp)):
                if isPalindorme(s[j:i+1]):
                    cur_count = dp[j] + 1
                    if cur_count < min_split:
                        min_split = cur_count
            dp.append(min_split)
        return dp[-1]
            
```