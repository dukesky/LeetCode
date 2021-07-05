# [566. Reshape the Matrix (Easy)](https://leetcode.com/problems/reshape-the-matrix/)

<p>In MATLAB, there is a handy function called <code>reshape</code>&nbsp;which can reshape an <code>m x n</code> matrix into a new one with a different size <code>r x c</code>&nbsp;keeping its original data.</p>

<p>You are given an <code>m x n</code>&nbsp;matrix <code>mat</code> and two integers <code>r</code> and <code>c</code> representing the row number and column number of the wanted reshaped matrix.</p>

<p>The reshaped matrix should be filled with all the elements of the original matrix in the same row-traversing order as they were.</p>

<p>If the <code>reshape</code>&nbsp;operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/04/24/reshape1-grid.jpg" style="width: 613px; height: 173px;">
<pre><strong>Input:</strong> mat = [[1,2],[3,4]], r = 1, c = 4
<strong>Output:</strong> [[1,2,3,4]]
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/04/24/reshape2-grid.jpg" style="width: 453px; height: 173px;">
<pre><strong>Input:</strong> mat = [[1,2],[3,4]], r = 2, c = 4
<strong>Output:</strong> [[1,2],[3,4]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == mat.length</code></li>
	<li><code>n == mat[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 100</code></li>
	<li><code>-1000 &lt;= mat[i][j] &lt;= 1000</code></li>
	<li><code>1 &lt;= r, c &lt;= 300</code></li>
</ul>


**Companies**:  
[Mathworks](https://leetcode.com/company/mathworks)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Matrix](https://leetcode.com/tag/matrix/), [Simulation](https://leetcode.com/tag/simulation/)

## Solution 1.

```python
class Solution:
    def matrixReshape(self, mat: List[List[int]], r: int, c: int) -> List[List[int]]:
        pre_r = len(mat)
        pre_c = len(mat[0])
        if pre_r * pre_c != r * c:
            return mat
        result = [[0] * c for _ in range(r)]
        r_pt = 0
        c_pt = 0
        for i in range(pre_r):
            for j in range(pre_c):
                result[r_pt][c_pt] = mat[i][j]
                if c_pt < c - 1:
                    c_pt += 1
                else:
                    r_pt += 1
                    c_pt = 0
        return result

```