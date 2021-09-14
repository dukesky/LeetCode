# [953. Verifying an Alien Dictionary (Easy)](https://leetcode.com/problems/verifying-an-alien-dictionary/)

<p>In an alien language, surprisingly, they also use English lowercase letters, but possibly in a different <code>order</code>. The <code>order</code> of the alphabet is some permutation of lowercase letters.</p>

<p>Given a sequence of <code>words</code> written in the alien language, and the <code>order</code> of the alphabet, return <code>true</code> if and only if the given <code>words</code> are sorted lexicographically in this alien language.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> words = ["hello","leetcode"], order = "hlabcdefgijkmnopqrstuvwxyz"
<strong>Output:</strong> true
<strong>Explanation: </strong>As 'h' comes before 'l' in this language, then the sequence is sorted.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> words = ["word","world","row"], order = "worldabcefghijkmnpqstuvxyz"
<strong>Output:</strong> false
<strong>Explanation: </strong>As 'd' comes after 'l' in this language, then words[0] &gt; words[1], hence the sequence is unsorted.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> words = ["apple","app"], order = "abcdefghijklmnopqrstuvwxyz"
<strong>Output:</strong> false
<strong>Explanation: </strong>The first three characters "app" match, and the second string is shorter (in size.) According to lexicographical rules "apple" &gt; "app", because 'l' &gt; '∅', where '∅' is defined as the blank character which is less than any other character (<a href="https://en.wikipedia.org/wiki/Lexicographical_order" target="_blank">More info</a>).
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= words.length &lt;= 100</code></li>
	<li><code>1 &lt;= words[i].length &lt;= 20</code></li>
	<li><code>order.length == 26</code></li>
	<li>All characters in <code>words[i]</code> and <code>order</code> are English lowercase letters.</li>
</ul>


**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Walmart Labs](https://leetcode.com/company/walmart-labs), [eBay](https://leetcode.com/company/ebay), [Amazon](https://leetcode.com/company/amazon), [DE Shaw](https://leetcode.com/company/de-shaw)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/)

## Solution 1.

```py
class Solution:
    def isAlienSorted(self, words: List[str], order: str) -> bool:
        
        char_dict = collections.defaultdict(int)
        for i in range(0,len(order)):
            char_dict[order[i]] = i
            
        def compare(word1,word2,char_dict):
            p1,p2 = 0,0
            while  p1<len(word1)  and p2<len(word2) and word1[p1] == word2[p2]:
                p1 += 1
                p2 += 1
            if p1==len(word1):
                if p2<=len(word2):
                    return True
                else:
                    return False
            elif p2 == len(word2):
                return False
            else:
                if char_dict[word1[p1]] < char_dict[word2[p2]]:
                    return True
                else:
                    return False
                
        for i in range(len(words)-1):
            if not compare(words[i],words[i+1],char_dict):
                return False
            
        return True
```