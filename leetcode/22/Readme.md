# [1220. Count Vowels Permutation (Hard)](https://leetcode.com/problems/count-vowels-permutation/)

<p>Given an integer <code>n</code>, your task is to count how many strings of length <code>n</code> can be formed under the following rules:</p>

<ul>
	<li>Each character is a lower case vowel&nbsp;(<code>'a'</code>, <code>'e'</code>, <code>'i'</code>, <code>'o'</code>, <code>'u'</code>)</li>
	<li>Each vowel&nbsp;<code>'a'</code> may only be followed by an <code>'e'</code>.</li>
	<li>Each vowel&nbsp;<code>'e'</code> may only be followed by an <code>'a'</code>&nbsp;or an <code>'i'</code>.</li>
	<li>Each vowel&nbsp;<code>'i'</code> <strong>may not</strong> be followed by another <code>'i'</code>.</li>
	<li>Each vowel&nbsp;<code>'o'</code> may only be followed by an <code>'i'</code> or a&nbsp;<code>'u'</code>.</li>
	<li>Each vowel&nbsp;<code>'u'</code> may only be followed by an <code>'a'.</code></li>
</ul>

<p>Since the answer&nbsp;may be too large,&nbsp;return it modulo <code>10^9 + 7.</code></p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> n = 1
<strong>Output:</strong> 5
<strong>Explanation:</strong> All possible strings are: "a", "e", "i" , "o" and "u".
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> n = 2
<strong>Output:</strong> 10
<strong>Explanation:</strong> All possible strings are: "ae", "ea", "ei", "ia", "ie", "io", "iu", "oi", "ou" and "ua".
</pre>

<p><strong>Example 3:&nbsp;</strong></p>

<pre><strong>Input:</strong> n = 5
<strong>Output:</strong> 68</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 2 * 10^4</code></li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon)

**Related Topics**:  
[Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

## Solution 1.

```python
class Solution:
    def countVowelPermutation(self, n: int) -> int:
        # self.count = 0
        ## DFS  probabily TLE --> O(5^n)
        

                
        ## T: O(n) use an array represent # of ways begin with letter['a','e','i','o','u'] 
        # rearrange the current array which represent # of combination what has second letter follow with first letter in ['a','e','i','o','u'] to # of combination second letter in ['a','e','i','o','u']

            
        MOD = 10**9 + 7  
        def next_array(arr):
            a = (arr[1] + arr[2] + arr[4]) % MOD
            e = (arr[0] + arr[2]) % MOD
            i = (arr[1] + arr[3] ) % MOD
            o = arr[2]  % MOD
            u = (arr[2] + arr[3]) % MOD
            return [a,e,i,o,u]
        
        arr = [1,1,1,1,1]
        for i in range(n-1):
            arr = next_array(arr)

        return (sum(arr)) % MOD
```