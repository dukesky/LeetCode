# [1428. Leftmost Column with at Least a One (Medium)](https://leetcode.com/problems/leftmost-column-with-at-least-a-one/)

<p><em>(This problem is an <strong>interactive problem</strong>.)</em></p>

<p>A <strong>row-sorted binary matrix</strong> means that all elements are <code>0</code> or <code>1</code> and each row of the matrix is sorted in non-decreasing order.</p>

<p>Given a <strong>row-sorted binary matrix</strong> <code>binaryMatrix</code>, return <em>the index (0-indexed) of the <strong>leftmost column</strong> with a 1 in it</em>. If such an index does not exist, return <code>-1</code>.</p>

<p><strong>You can't access the Binary Matrix directly.</strong> You may only access the matrix using a <code>BinaryMatrix</code> interface:</p>

<ul>
	<li><code>BinaryMatrix.get(row, col)</code> returns the element of the matrix at index <code>(row, col)</code> (0-indexed).</li>
	<li><code>BinaryMatrix.dimensions()</code> returns the dimensions of the matrix as a list of 2 elements <code>[rows, cols]</code>, which means the matrix is <code>rows x cols</code>.</li>
</ul>

<p>Submissions making more than <code>1000</code> calls to <code>BinaryMatrix.get</code> will be judged <em>Wrong Answer</em>. Also, any solutions that attempt to circumvent the judge will result in disqualification.</p>

<p>For custom testing purposes, the input will be the entire binary matrix <code>mat</code>. You will not have access to the binary matrix directly.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<p><strong><img alt="" src="https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-5.jpg" style="width: 81px; height: 81px;"></strong></p>

<pre><strong>Input:</strong> mat = [[0,0],[1,1]]
<strong>Output:</strong> 0
</pre>

<p><strong>Example 2:</strong></p>

<p><strong><img alt="" src="https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-4.jpg" style="width: 81px; height: 81px;"></strong></p>

<pre><strong>Input:</strong> mat = [[0,0],[0,1]]
<strong>Output:</strong> 1
</pre>

<p><strong>Example 3:</strong></p>

<p><strong><img alt="" src="https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-3.jpg" style="width: 81px; height: 81px;"></strong></p>

<pre><strong>Input:</strong> mat = [[0,0],[0,0]]
<strong>Output:</strong> -1</pre>

<p><strong>Example 4:</strong></p>

<p><strong><img alt="" src="https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-6.jpg" style="width: 161px; height: 121px;"></strong></p>

<pre><strong>Input:</strong> mat = [[0,0,0,1],[0,0,1,1],[0,1,1,1]]
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>rows == mat.length</code></li>
	<li><code>cols == mat[i].length</code></li>
	<li><code>1 &lt;= rows, cols &lt;= 100</code></li>
	<li><code>mat[i][j]</code> is either <code>0</code> or <code>1</code>.</li>
	<li><code>mat[i]</code> is sorted in non-decreasing order.</li>
</ul>


**Companies**:  
[Facebook](https://leetcode.com/company/facebook)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Binary Search](https://leetcode.com/tag/binary-search/), [Matrix](https://leetcode.com/tag/matrix/), [Interactive](https://leetcode.com/tag/interactive/)

## Solution 1.

```py
"""
This is BinaryMatrix's API interface.
You should not implement it, or speculate about its implementation
"""
class BinaryMatrix(object):
   def get(self, row: int, col: int) -> int:
   def dimensions(self) -> list[]:

class Solution:
    def leftMostColumnWithOne(self, binaryMatrix: 'BinaryMatrix') -> int:
        
        ## maintain a list of col to find the first '1'  O(mn)
        total_row, total_col = binaryMatrix.dimensions()
        for col in range(total_col):
            for row in range(total_row):
                if binaryMatrix.get(row,col)==1:
                    return col
                    break
        return -1

```

## Solution 2.

```py

        ## binary search to find first '1' in first row, then check same index in second row, if not '1', find first '1' in first part of second row
        
        
class Solution:
    def leftMostColumnWithOne(self, binaryMatrix: 'BinaryMatrix') -> int:
        
        def find_first_one(binaryMatrix,row,end_index):
            # total_row,total_col = binaryMatrix.dimensions()
            if binaryMatrix.get(row,end_index) == 0:
                return -1
            left,right = 0,end_index
            while left<right:
                mid = (left+right)//2
                if binaryMatrix.get(row,mid) == 1:
                    right = mid
                else:
                    left = mid + 1

            return left
        
        total_row,total_col = binaryMatrix.dimensions()
        if sum([binaryMatrix.get(i,total_col-1) for i in range(total_row)]) == 0:
            return -1
        row = 0
        while find_first_one(binaryMatrix,row,total_col-1) == -1:
            row += 1
        
        first_col = find_first_one(binaryMatrix,row,total_col-1)
        row += 1
        
        while row < total_row:
            next_one = find_first_one(binaryMatrix,row,first_col)
            if next_one != -1:
                first_col = next_one
            row += 1
            
        return first_col

```