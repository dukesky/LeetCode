# [265. Paint House II (Hard)](https://leetcode.com/problems/paint-house-ii/)

<p>There are a row of <code>n</code> houses, each house can be painted with one of the <code>k</code> colors. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.</p>

<p>The cost of painting each house with a certain color is represented by an <code>n x k</code> cost matrix costs.</p>

<ul>
	<li>For example, <code>costs[0][0]</code> is the cost of painting house <code>0</code> with color <code>0</code>; <code>costs[1][2]</code> is the cost of painting house <code>1</code> with color <code>2</code>, and so on...</li>
</ul>

<p>Return <em>the minimum cost to paint all houses</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> costs = [[1,5,3],[2,9,4]]
<strong>Output:</strong> 5
<strong>Explanation:</strong>
Paint house 0 into color 0, paint house 1 into color 2. Minimum cost: 1 + 4 = 5; 
Or paint house 0 into color 2, paint house 1 into color 0. Minimum cost: 3 + 2 = 5.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> costs = [[1,3],[2,4]]
<strong>Output:</strong> 5
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>costs.length == n</code></li>
	<li><code>costs[i].length == k</code></li>
	<li><code>1 &lt;= n &lt;= 100</code></li>
	<li><code>2 &lt;= k &lt;= 20</code></li>
	<li><code>1 &lt;= costs[i][j] &lt;= 20</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Could you solve it in <code>O(nk)</code> runtime?</p>


**Companies**:  
[LinkedIn](https://leetcode.com/company/linkedin)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

**Similar Questions**:
* [Product of Array Except Self (Medium)](https://leetcode.com/problems/product-of-array-except-self/)
* [Sliding Window Maximum (Hard)](https://leetcode.com/problems/sliding-window-maximum/)
* [Paint House (Medium)](https://leetcode.com/problems/paint-house/)
* [Paint Fence (Medium)](https://leetcode.com/problems/paint-fence/)

## Solution 1.

```py

class Solution:
    def minCostII(self, costs: List[List[int]]) -> int:
        
        ## brute force DFS find the min T: O(k^n)
        
        
        ## use DP  T: O(k^2n)

        n = len(costs)
        if n == 0: return 0
        k = len(costs[0])

        for house in range(1, n):
            # Find the colors with the minimum and second to minimum
            # in the previous row.
            min_color = second_min_color = None
            for color in range(k):
                cost = costs[house - 1][color]
                if min_color is None or cost < costs[house - 1][min_color]:
                    second_min_color = min_color
                    min_color = color
                elif second_min_color is None or cost < costs[house - 1][second_min_color]:
                    second_min_color = color
            # And now update the costs for the current row.
            for color in range(k):
                if color == min_color:
                    costs[house][color] += costs[house - 1][second_min_color]
                else:
                    costs[house][color] += costs[house - 1][min_color]
        print(costs)
        #The answer will now be the minimum of the last row.
        return min(costs[-1])
```