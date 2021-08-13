# [73. Set Matrix Zeroes (Medium)](https://leetcode.com/problems/set-matrix-zeroes/)

<p>Given an <code>m x n</code> integer matrix <code>matrix</code>, if an element is <code>0</code>, set its entire row and column to <code>0</code>'s, and return <em>the matrix</em>.</p>

<p>You must do it <a href="https://en.wikipedia.org/wiki/In-place_algorithm" target="_blank">in place</a>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg" style="width: 450px; height: 169px;">
<pre><strong>Input:</strong> matrix = [[1,1,1],[1,0,1],[1,1,1]]
<strong>Output:</strong> [[1,0,1],[0,0,0],[1,0,1]]
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg" style="width: 450px; height: 137px;">
<pre><strong>Input:</strong> matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
<strong>Output:</strong> [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == matrix.length</code></li>
	<li><code>n == matrix[0].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 200</code></li>
	<li><code>-2<sup>31</sup> &lt;= matrix[i][j] &lt;= 2<sup>31</sup> - 1</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong></p>

<ul>
	<li>A straightforward solution using <code>O(mn)</code> space is probably a bad idea.</li>
	<li>A simple improvement uses <code>O(m + n)</code> space, but still not the best solution.</li>
	<li>Could you devise a constant space solution?</li>
</ul>


**Companies**:  
[Microsoft](https://leetcode.com/company/microsoft), [Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Qualtrics](https://leetcode.com/company/qualtrics)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:
* [Game of Life (Medium)](https://leetcode.com/problems/game-of-life/)

## Solution 1.

```py
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        # solution1: store all 0 element with it's row,col, use them to change other values inplace, maintain two set seen_rows and seen_cols to store all zero row and cols after previous change
        # T: O(mn)    S: O(mn)
        zeros = set()
        seen_rows = set()
        seen_cols = set()
        for row in range(len(matrix)):
            for col in range(len(matrix[0])):
                if matrix[row][col] == 0:
                    zeros.add((row,col))
        for row,col in zeros:
            if row not in seen_rows:
                for i in range(0,len(matrix[0])):
                    matrix[row][i] = 0
                seen_rows.add(row)
            if col not in seen_cols:
                for i in range(0,len(matrix)):
                    matrix[i][col] = 0
                seen_cols.add(col)
        
```

## Solution 2.

```py
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        ## Solution2:   T:O(mn),S:O(m+n)
        ## Search all elements in matrix, store changed row and col to sets
        
        
        ## Solution3:  S:O(1)
        ## fitst, go through all elements in matrix, when find zero, change the begining of this row and col to NA
        ## then, go through all beginning for row and cols, change all NA row,col to all zeros
        
        ## find NA
        for row in range(1,len(matrix)):
            for col in range(1,len(matrix[0])):
                if matrix[row][col] == 0:
                    if matrix[row][0] != 0:
                        matrix[row][0] = None
                    if matrix[0][col] != 0:
                        matrix[0][col] = None
                    
        print(matrix)
        ## change all NA row/cols
        for row in range(1,len(matrix)):
            if not matrix[row][0]:
                for col in range(1,len(matrix[0])):
                    matrix[row][col] = 0
        for col in range(1,len(matrix[0])):
            if not matrix[0][col]:
                for row in range(1,len(matrix)):
                    matrix[row][col] = 0
        ## deal with first col and first row
        if matrix[0][0] == 0:
            for i in range(0,len(matrix)):
                matrix[i][0] = 0
            for j in range(0,len(matrix[0])):
                matrix[0][j] = 0
        else:
            corner = matrix[0][0]
            for i in range(1,len(matrix)):
                if matrix[i][0] == 0:
                    corner = 0
                    for j in range(1,len(matrix)):
                        matrix[j][0] = 0
                    break
                elif not matrix[i][0]:
                    matrix[i][0] = 0
            for j in range(1,len(matrix[0])):
                if matrix[0][j] == 0:
                    corner = 0
                    for j in range(1,len(matrix[0])):
                        matrix[0][j] = 0
                    break
                elif not matrix[0][j]:
                    matrix[0][j] = 0
            matrix[0][0] = corner
        
                    
            
```