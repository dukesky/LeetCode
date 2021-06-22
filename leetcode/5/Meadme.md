# [792. Number of Matching Subsequences (Medium)](https://leetcode.com/problems/number-of-matching-subsequences/)

<p>Given a string <code>s</code> and an array of strings <code>words</code>, return <em>the number of</em> <code>words[i]</code> <em>that is a subsequence of</em> <code>s</code>.</p>

<p>A <strong>subsequence</strong> of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.</p>

<ul>
	<li>For example, <code>"ace"</code> is a subsequence of <code>"abcde"</code>.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "abcde", words = ["a","bb","acd","ace"]
<strong>Output:</strong> 3
<strong>Explanation:</strong> There are three strings in words that are a subsequence of s: "a", "acd", "ace".
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "dsahjpjauf", words = ["ahjpjau","ja","ahbwzgqnuk","tnmlanowax"]
<strong>Output:</strong> 2
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>1 &lt;= words.length &lt;= 5000</code></li>
	<li><code>1 &lt;= words[i].length &lt;= 50</code></li>
	<li><code>s</code> and <code>words[i]</code> consist of only lowercase English letters.</li>
</ul>


**Companies**:  
[Google](https://leetcode.com/company/google), [Amazon](https://leetcode.com/company/amazon), [Coupang](https://leetcode.com/company/coupang)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/)

**Similar Questions**:
* [Is Subsequence (Easy)](https://leetcode.com/problems/is-subsequence/)
* [Shortest Way to Form String (Medium)](https://leetcode.com/problems/shortest-way-to-form-string/)

## Solution 1.

```python
class Solution:
    def numMatchingSubseq(self, s: str, words: List[str]) -> int:
        # Solution1
        # iterate over string list
        # Time: O(mn)  m-len(s) n-len(word)   Space: O(1)
        # LTE
        count = 0
        for word in words:
            s_pt = 0
            word_pt = 0
            while word_pt < len(word) and s_pt < len(s):
                if s[s_pt] == word[word_pt]:
                    word_pt += 1
                s_pt +=1
            if word_pt == len(word):
                count += 1
        return count
```

## Solution 2.
```python
class Solution:
    def numMatchingSubseq(self, s: str, words: List[str]) -> int:
        ## Solution2
        ## Store all letters in s to a dictionary, compared the letter in word with words in dictionary. if could found letter,
        ## Time: O(n^2)  n-len(word)  Space:O(m) m-len(s)
        s_dict = dict()
        for i,char in enumerate(s):
            if char not in s_dict:
                s_dict[char] = [i]
            else:
                s_dict[char].append(i)
        count = 0
        for word in words:
            word_count = [0] * 26
            word_pt = 0
            s_pt = -1
            not_find = False
            # print(s_dict)
            while word_pt< len(word):
                char = word[word_pt]
                char_in_dict = word_count[ord(word[word_pt])-ord('a')]
                if char in s_dict and char_in_dict < len(s_dict[char]):
                    while char_in_dict < len(s_dict[char]) and s_dict[char][char_in_dict] <= s_pt:
                        char_in_dict += 1
                        
                    if char_in_dict < len(s_dict[char]):
                        s_pt = s_dict[char][char_in_dict]
                    else:
                        not_find = True
                        # print(char,'out limit')
                        break
                else:
                    not_find = True
                    # print(char,'out limit')
                    break
                word_count[ord(word[word_pt])-ord('a')] = char_in_dict
                # print('word:',word,'find',char,'in',s_pt)
                word_pt += 1
            if not not_find:
                    count += 1
        # print(word_count)
        return count
```