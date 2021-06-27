# [1915. Number of Wonderful Substrings (Medium)](https://leetcode.com/problems/number-of-wonderful-substrings/)

<p>A <strong>wonderful</strong> string is a string where <strong>at most one</strong> letter appears an <strong>odd</strong> number of times.</p>

<ul>
	<li>For example, <code>"ccjjc"</code> and <code>"abab"</code> are wonderful, but <code>"ab"</code> is not.</li>
</ul>

<p>Given a string <code>word</code> that consists of the first ten lowercase English letters (<code>'a'</code> through <code>'j'</code>), return <em>the <strong>number of wonderful non-empty substrings</strong> in </em><code>word</code><em>. If the same substring appears multiple times in </em><code>word</code><em>, then count <strong>each occurrence</strong> separately.</em></p>

<p>A <strong>substring</strong> is a contiguous sequence of characters in a string.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> word = "aba"
<strong>Output:</strong> 4
<strong>Explanation:</strong> The four wonderful substrings are underlined below:
- "<u><strong>a</strong></u>ba" -&gt; "a"
- "a<u><strong>b</strong></u>a" -&gt; "b"
- "ab<u><strong>a</strong></u>" -&gt; "a"
- "<u><strong>aba</strong></u>" -&gt; "aba"
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> word = "aabb"
<strong>Output:</strong> 9
<strong>Explanation:</strong> The nine wonderful substrings are underlined below:
- "<strong><u>a</u></strong>abb" -&gt; "a"
- "<u><strong>aa</strong></u>bb" -&gt; "aa"
- "<u><strong>aab</strong></u>b" -&gt; "aab"
- "<u><strong>aabb</strong></u>" -&gt; "aabb"
- "a<u><strong>a</strong></u>bb" -&gt; "a"
- "a<u><strong>abb</strong></u>" -&gt; "abb"
- "aa<u><strong>b</strong></u>b" -&gt; "b"
- "aa<u><strong>bb</strong></u>" -&gt; "bb"
- "aab<u><strong>b</strong></u>" -&gt; "b"
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> word = "he"
<strong>Output:</strong> 2
<strong>Explanation:</strong> The two wonderful substrings are underlined below:
- "<b><u>h</u></b>e" -&gt; "h"
- "h<strong><u>e</u></strong>" -&gt; "e"
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= word.length &lt;= 10<sup>5</sup></code></li>
	<li><code>word</code> consists of lowercase English letters from <code>'a'</code>&nbsp;to <code>'j'</code>.</li>
</ul>


**Related Topics**:  
[String](https://leetcode.com/tag/string/), [Bit Manipulation](https://leetcode.com/tag/bit-manipulation/)

## Solution 1.

```python
class Solution:
    def wonderfulSubstrings(self, word: str) -> int:
        # loop check for begin and end pointer: O(n^2)  TLE
        count = 0
        for i in range(0,len(word)):
            char_dict = dict()
            for j in range(i,len(word)):
                is_wonderful = True
                if word[j] not in char_dict:
                    char_dict[word[j]] = 1
                else:
                    char_dict[word[j]] += 1
                    if char_dict[word[j]] % 2 == 0:
                        char_dict[word[j]] = 0
                # print(i,j,char_dict)
                odd_count = 0
                for char in char_dict:
                    if char_dict[char] == 1:
                        odd_count += 1
                        if odd_count > 1:
                            is_wonderful = False
                            break
                if is_wonderful:
                    # print('find wondeful',word[i:j+1])
                    count += 1
        return count
```

## Solution 2.

``` python
## bit mask
    def wonderfulSubstrings(self, word):
        count = [1] + [0] * 1024
        res = cur = 0
        for c in word:
            cur ^= 1 << (ord(c) - ord('a'))
            res += count[cur]
            res += sum(count[cur ^ (1 << i)] for i in xrange(10))
            count[cur] += 1
        return res


```