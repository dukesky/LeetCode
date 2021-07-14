# [791. Custom Sort String (Medium)](https://leetcode.com/problems/custom-sort-string/)

<p><code>order</code> and <code>str</code> are strings composed of lowercase letters. In <code>order</code>, no letter occurs more than once.</p>

<p><code>order</code> was sorted in some custom order previously. We want to permute the characters of <code>str</code> so that they match the order that <code>order</code> was sorted. More specifically, if <code>x</code> occurs before <code>y</code> in <code>order</code>, then <code>x</code> should occur before <code>y</code> in the returned string.</p>

<p>Return any permutation of <code>str</code> (as a string) that satisfies this property.</p>

<pre><strong>Example:</strong>
<strong>Input:</strong> 
order = "cba"
str = "abcd"
<strong>Output:</strong> "cbad"
<strong>Explanation:</strong> 
"a", "b", "c" appear in order, so the order of "a", "b", "c" should be "c", "b", and "a". 
Since "d" does not appear in order, it can be at any position in the returned string. "dcba", "cdba", "cbda" are also valid outputs.
</pre>

<p>&nbsp;</p>

<p><strong>Note:</strong></p>

<ul>
	<li><code>order</code> has length at most <code>26</code>, and no character is repeated in <code>order</code>.</li>
	<li><code>str</code> has length at most <code>200</code>.</li>
	<li><code>order</code> and <code>str</code> consist of lowercase letters only.</li>
</ul>


**Companies**:  
[Facebook](https://leetcode.com/company/facebook)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Sorting](https://leetcode.com/tag/sorting/)

## Solution 1.

```python
class Solution:
    def customSortString(self, order: str, str: str) -> str:
         
        # T:O(n) store frequence of letter in order happend in str, if letter in str not appear in order, append it into a additional str, 
        str_dict = dict()
        add_str = ''
        for char in order:
            str_dict[char] = 0
        for char in str:
            if char in str_dict:
                str_dict[char] += 1
            else:
                add_str += char
        result = ''.join([char * str_dict[char] for char in order]) + add_str
        return result
            
        

```