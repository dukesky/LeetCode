# [54. Spiral Matrix (Medium)](https://leetcode.com/problems/spiral-matrix/solution/)

<p>Given an <code>m x n</code> <code>matrix</code>, return <em>all elements of the</em> <code>matrix</code> <em>in spiral order</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg" style="width: 242px; height: 242px;">
<pre><strong>Input:</strong> matrix = [[1,2,3],[4,5,6],[7,8,9]]
<strong>Output:</strong> [1,2,3,6,9,8,7,4,5]
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg" style="width: 322px; height: 242px;">
<pre><strong>Input:</strong> matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
<strong>Output:</strong> [1,2,3,4,8,12,11,10,9,5,6,7]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == matrix.length</code></li>
	<li><code>n == matrix[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 10</code></li>
	<li><code>-100 &lt;= matrix[i][j] &lt;= 100</code></li>
</ul>


**Companies**:  
[Microsoft](https://leetcode.com/company/microsoft), [Apple](https://leetcode.com/company/apple), [Amazon](https://leetcode.com/company/amazon), [Adobe](https://leetcode.com/company/adobe), [Bloomberg](https://leetcode.com/company/bloomberg), [Oracle](https://leetcode.com/company/oracle), [VMware](https://leetcode.com/company/vmware), [Intuit](https://leetcode.com/company/intuit), [Google](https://leetcode.com/company/google), [Facebook](https://leetcode.com/company/facebook), [Walmart Labs](https://leetcode.com/company/walmart-labs), [ByteDance](https://leetcode.com/company/bytedance), [Tesla](https://leetcode.com/company/tesla), [Accolite](https://leetcode.com/company/accolite), [Flipkart](https://leetcode.com/company/flipkart), [HBO](https://leetcode.com/company/hbo)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Matrix](https://leetcode.com/tag/matrix/), [Simulation](https://leetcode.com/tag/simulation/)

**Similar Questions**:
* [Spiral Matrix II (Medium)](https://leetcode.com/problems/spiral-matrix-ii/)
* [Spiral Matrix III (Medium)](https://leetcode.com/problems/spiral-matrix-iii/)

## Solution 1.

```py

class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        
        res = []
        for i in range(min((len(matrix)+1)//2,(len(matrix[0])+1)//2)):
            horiz = len(matrix[0]) - 2*i
            ver = len(matrix) - 2*i
            if horiz==1:
                res += [matrix[i+j][i] for j in range(ver)]
                return res
            elif ver==1:
                res += matrix[i][i:i+horiz]
                return res
            res += [matrix[i][i+j] for j in range(horiz-1)]
            res += [matrix[i+j][len(matrix[0])-i-1] for j in range(ver-1)]
            res += [matrix[len(matrix)-i-1][len(matrix[0])-i-j-1] for j in range(horiz-1)]
            res += [matrix[len(matrix)-i-1-j][i] for j in range(ver-1)]

        return res
```