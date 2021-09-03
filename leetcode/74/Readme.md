# [322. Coin Change (Medium)](https://leetcode.com/problems/coin-change/)

<p>You are given an integer array <code>coins</code> representing coins of different denominations and an integer <code>amount</code> representing a total amount of money.</p>

<p>Return <em>the fewest number of coins that you need to make up that amount</em>. If that amount of money cannot be made up by any combination of the coins, return <code>-1</code>.</p>

<p>You may assume that you have an infinite number of each kind of coin.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> coins = [1,2,5], amount = 11
<strong>Output:</strong> 3
<strong>Explanation:</strong> 11 = 5 + 5 + 1
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> coins = [2], amount = 3
<strong>Output:</strong> -1
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> coins = [1], amount = 0
<strong>Output:</strong> 0
</pre>

<p><strong>Example 4:</strong></p>

<pre><strong>Input:</strong> coins = [1], amount = 1
<strong>Output:</strong> 1
</pre>

<p><strong>Example 5:</strong></p>

<pre><strong>Input:</strong> coins = [1], amount = 2
<strong>Output:</strong> 2
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= coins.length &lt;= 12</code></li>
	<li><code>1 &lt;= coins[i] &lt;= 2<sup>31</sup> - 1</code></li>
	<li><code>0 &lt;= amount &lt;= 10<sup>4</sup></code></li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Google](https://leetcode.com/company/google), [Apple](https://leetcode.com/company/apple), [Walmart Labs](https://leetcode.com/company/walmart-labs), [Bloomberg](https://leetcode.com/company/bloomberg), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [Adobe](https://leetcode.com/company/adobe), [Uber](https://leetcode.com/company/uber), [Citadel](https://leetcode.com/company/citadel), [Zoom](https://leetcode.com/company/zoom), [tcs](https://leetcode.com/company/tcs)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/)

**Similar Questions**:
* [Minimum Cost For Tickets (Medium)](https://leetcode.com/problems/minimum-cost-for-tickets/)

## Solution 1.

```py
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        
        ## use DP m*n  DP[i][j] is minimal coins by use coins[:i] to form j
        ## we want to count DP[len(coins)][amount]
        
        # coins = sorted(coins)
        # DP = [[float('inf') for _ in range(amount+1)] for _ in range(len(coins)+1)]
        # for i in range(1,len(coins)+1):
        #     for j in range(amount+1):
        #         if j == 0:
        #             DP[i][j] = 0
        #         elif j >= coins[i-1]:
        #             DP[i][j] = min(DP[i][j-coins[i-1]]+1,DP[i-1][j])
        #         else:
        #             DP[i][j] = DP[i-1][j]
        # if DP[-1][-1] == float('inf'):
        #     return -1
        # return DP[-1][-1]
    
        ## Optimized with O(m) space
        DP = [float('inf') for _ in range(amount+1)]
        DP[0] = 0
        for i in range(0,len(coins)):
            for j in range(amount+1):
                if j >= coins[i]:
                    DP[j] = min(DP[j-coins[i]]+1,DP[j])
        if DP[-1] == float('inf'):
            return -1
        return DP[-1]        
```