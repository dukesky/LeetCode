# [205. Isomorphic Strings (Easy)](https://leetcode.com/problems/isomorphic-strings/)

<p>Given two strings <code>s</code> and <code>t</code>, <em>determine if they are isomorphic</em>.</p>

<p>Two strings <code>s</code> and <code>t</code> are isomorphic if the characters in <code>s</code> can be replaced to get <code>t</code>.</p>

<p>All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> s = "egg", t = "add"
<strong>Output:</strong> true
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> s = "foo", t = "bar"
<strong>Output:</strong> false
</pre><p><strong>Example 3:</strong></p>
<pre><strong>Input:</strong> s = "paper", t = "title"
<strong>Output:</strong> true
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>t.length == s.length</code></li>
	<li><code>s</code> and <code>t</code> consist of any valid ascii character.</li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Uber](https://leetcode.com/company/uber)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/)

**Similar Questions**:
* [Word Pattern (Easy)](https://leetcode.com/problems/word-pattern/)

## Solution 1.

```python
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        ## use dictionary to map s and t to ordered value and compare s_dict[s[i]] and t_dict[t[i]] 
        char_count = 0
        s_dict = dict()
        t_dict = dict()
        for i in range(0,len(s)):
            if s[i] not in s_dict:
                if t[i] in t_dict:
                    return False
                else:
                    s_dict[s[i]] = char_count
                    t_dict[t[i]] = char_count
                    char_count += 1
            else:
                if t[i] not in t_dict:
                    return False
                elif s_dict[s[i]] != t_dict[t[i]]:
                    return False
        return True

```