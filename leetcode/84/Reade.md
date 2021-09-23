# [917. Reverse Only Letters (Easy)](https://leetcode.com/problems/reverse-only-letters/)

<p>Given a string <code>s</code>, reverse the string according to the following rules:</p>

<ul>
	<li>All the characters that are not English letters remain in the same position.</li>
	<li>All the English letters (lowercase or uppercase) should be reversed.</li>
</ul>

<p>Return <code>s</code><em> after reversing it</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> s = "ab-cd"
<strong>Output:</strong> "dc-ba"
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> s = "a-bC-dEf-ghIj"
<strong>Output:</strong> "j-Ih-gfE-dCba"
</pre><p><strong>Example 3:</strong></p>
<pre><strong>Input:</strong> s = "Test1ng-Leet=code-Q!"
<strong>Output:</strong> "Qedo1ct-eeLg=ntse-T!"
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 100</code></li>
	<li><code>s</code> consists of characters with ASCII values in the range <code>[33, 122]</code>.</li>
	<li><code>s</code> does not contain <code>'\"'</code> or <code>'\\'</code>.</li>
</ul>


**Companies**:  
[Apple](https://leetcode.com/company/apple), [Microsoft](https://leetcode.com/company/microsoft)

**Related Topics**:  
[Two Pointers](https://leetcode.com/tag/two-pointers/), [String](https://leetcode.com/tag/string/)

## Solution 1.

```py
class Solution:
    def reverseOnlyLetters(self, s: str) -> str:
        
        ## two pointer
        s = [char for char in s]
        letters = set([chr(ord('A')+i) for i in range(26)]+[chr(ord('a')+i) for i in range(26)])
        print(letters)

        left, right = 0,len(s)-1
        while left < right:
            while 0<=left < right<len(s) and s[left] not in letters:
                left += 1
            while 0<=left < right<len(s) and s[right] not in letters:
                right -= 1
            print(left,right)
            s[left],s[right] = s[right],s[left]
            left += 1
            right -= 1
        return ''.join(s)
                
            

```