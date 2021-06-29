# [1047. Remove All Adjacent Duplicates In String (Easy)](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)

<p>You are given a string <code>s</code> consisting of lowercase English letters. A <strong>duplicate removal</strong> consists of choosing two <strong>adjacent</strong> and <strong>equal</strong> letters and removing them.</p>

<p>We repeatedly make <strong>duplicate removals</strong> on <code>s</code> until we no longer can.</p>

<p>Return <em>the final string after all such duplicate removals have been made</em>. It can be proven that the answer is <strong>unique</strong>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "abbaca"
<strong>Output:</strong> "ca"
<strong>Explanation:</strong> 
For example, in "abbaca" we could remove "bb" since the letters are adjacent and equal, and this is the only possible move.  The result of this move is that the string is "aaca", of which only "aa" is possible, so the final string is "ca".
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "azxxzy"
<strong>Output:</strong> "ay"
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>5</sup></code></li>
	<li><code>s</code> consists of lowercase English letters.</li>
</ul>


**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Bloomberg](https://leetcode.com/company/bloomberg), [Microsoft](https://leetcode.com/company/microsoft), [Adobe](https://leetcode.com/company/adobe)

**Related Topics**:  
[String](https://leetcode.com/tag/string/), [Stack](https://leetcode.com/tag/stack/)

**Similar Questions**:
* [Remove All Adjacent Duplicates in String II (Medium)](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/)

## Solution 1.

```python
class Solution:
    def removeDuplicates(self, s: str) -> str:
        
        ## use a stack  O(n)
        stack = []
        for char in s:
            if stack:
                last = stack.pop()
                if last != char:
                    stack.append(last)
                    stack.append(char)
            else:
                stack.append(char)
        return ''.join(stack)

```