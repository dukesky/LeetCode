# [186. Reverse Words in a String II (Medium)](https://leetcode.com/problems/reverse-words-in-a-string-ii/)

<p>Given a character array <code>s</code>, reverse the order of the <strong>words</strong>.</p>

<p>A <strong>word</strong> is defined as a sequence of non-space characters. The <strong>words</strong> in <code>s</code> will be separated by a single space.</p>

<p>Your code must solve the problem&nbsp;<strong>in-place,</strong> i.e. without allocating extra space.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> s = ["t","h","e"," ","s","k","y"," ","i","s"," ","b","l","u","e"]
<strong>Output:</strong> ["b","l","u","e"," ","i","s"," ","s","k","y"," ","t","h","e"]
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> s = ["a"]
<strong>Output:</strong> ["a"]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>5</sup></code></li>
	<li><code>s[i]</code> is an English letter (uppercase or lowercase), digit, or space <code>' '</code>.</li>
	<li>There is <strong>at least one</strong> word in <code>s</code>.</li>
	<li><code>s</code> does not contain leading or trailing spaces.</li>
	<li>All the words in <code>s</code> are guaranteed to be separated by a single space.</li>
</ul>


**Companies**:  
[Microsoft](https://leetcode.com/company/microsoft)

**Related Topics**:  
[Two Pointers](https://leetcode.com/tag/two-pointers/), [String](https://leetcode.com/tag/string/)

**Similar Questions**:
* [Reverse Words in a String (Medium)](https://leetcode.com/problems/reverse-words-in-a-string/)
* [Rotate Array (Medium)](https://leetcode.com/problems/rotate-array/)

## Solution 1.

```python
class Solution:
    def reverseWords(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        
        ## reverse the whole string and reverse each word
        def reverse(s,begin,end):
            left,right = begin,end
            while left < right:
                s[left],s[right] = s[right],s[left]
                left += 1
                right -= 1
                
        ## reverse whole string
        reverse(s,0,len(s)-1)
        left = 0
        for right in range(0,len(s)):
            if s[right] == ' ':
                reverse(s,left,right-1)
                left = right + 1
        reverse(s,left,right)


```