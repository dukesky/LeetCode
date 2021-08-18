# [91. Decode Ways (Medium)](https://leetcode.com/problems/decode-ways/)

<p>A message containing letters from <code>A-Z</code> can be <strong>encoded</strong> into numbers using the following mapping:</p>

<pre>'A' -&gt; "1"
'B' -&gt; "2"
...
'Z' -&gt; "26"
</pre>

<p>To <strong>decode</strong> an encoded message, all the digits must be grouped then mapped back into letters using the reverse of the mapping above (there may be multiple ways). For example, <code>"11106"</code> can be mapped into:</p>

<ul>
	<li><code>"AAJF"</code> with the grouping <code>(1 1 10 6)</code></li>
	<li><code>"KJF"</code> with the grouping <code>(11 10 6)</code></li>
</ul>

<p>Note that the grouping <code>(1 11 06)</code> is invalid because <code>"06"</code> cannot be mapped into <code>'F'</code> since <code>"6"</code> is different from <code>"06"</code>.</p>

<p>Given a string <code>s</code> containing only digits, return <em>the <strong>number</strong> of ways to <strong>decode</strong> it</em>.</p>

<p>The answer is guaranteed to fit in a <strong>32-bit</strong> integer.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "12"
<strong>Output:</strong> 2
<strong>Explanation:</strong> "12" could be decoded as "AB" (1 2) or "L" (12).
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "226"
<strong>Output:</strong> 3
<strong>Explanation:</strong> "226" could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> s = "0"
<strong>Output:</strong> 0
<strong>Explanation:</strong> There is no character that is mapped to a number starting with 0.
The only valid mappings with 0 are 'J' -&gt; "10" and 'T' -&gt; "20", neither of which start with 0.
Hence, there are no valid ways to decode this since all digits need to be mapped.
</pre>

<p><strong>Example 4:</strong></p>

<pre><strong>Input:</strong> s = "06"
<strong>Output:</strong> 0
<strong>Explanation:</strong> "06" cannot be mapped to "F" because of the leading zero ("6" is different from "06").
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 100</code></li>
	<li><code>s</code> contains only digits and may contain leading zero(s).</li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Lyft](https://leetcode.com/company/lyft), [JPMorgan](https://leetcode.com/company/jpmorgan), [Microsoft](https://leetcode.com/company/microsoft), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [Cisco](https://leetcode.com/company/cisco), [Bloomberg](https://leetcode.com/company/bloomberg), [Snapchat](https://leetcode.com/company/snapchat), [Facebook](https://leetcode.com/company/facebook), [Uber](https://leetcode.com/company/uber), [Yahoo](https://leetcode.com/company/yahoo), [Nagarro](https://leetcode.com/company/nagarro), [Shopee](https://leetcode.com/company/shopee), [Karat](https://leetcode.com/company/karat)

**Related Topics**:  
[String](https://leetcode.com/tag/string/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

**Similar Questions**:
* [Decode Ways II (Hard)](https://leetcode.com/problems/decode-ways-ii/)

## Solution 1.

```py

class Solution:
    def numDecodings(self, s: str) -> int:
        
        ## use dp
        ## dp[i] represent total possible ways for s[:i+1]
        ## if s[i] == 0:  if s[i-1] 1/2, dp[i] = dp[i-2]
        ##                if s[i-1] not 1/2 return 0
        ## is s[i] > 6:   if s[i-1]=1: dp[i] = dp[i-1]+dp[i-2]
        ##                else dp[i] = dp[i-1]

        ## is 1<=s[i]<= 6: if s[i-1]=1,2: dp[i] = dp[i-1]+dp[i-2]
        ##                 else: dp[i] = dp[i-1]

        
        if len(s) == 0 or s[0]=='0': return 0
        if len(s) == 1: return 1
        
        dp = [1,1]
        for i,char in enumerate(s):
            if i == 0: continue
            if int(s[i]) == 0:
                if int(s[i-1]) in [1,2]:
                    dp.append(dp[i-1])
                else:
                    return 0
            elif int(s[i]) > 6:
                if int(s[i-1]) == 1:
                    dp.append(dp[i-1]+dp[i])
                else:
                    dp.append(dp[i])
            else :
                if int(s[i-1]) in [1,2]:
                    dp.append(dp[i-1]+dp[i])
                else:
                    dp.append(dp[i])

        return dp[-1]
```