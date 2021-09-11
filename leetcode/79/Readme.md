# [764. Largest Plus Sign (Medium)](https://leetcode.com/problems/largest-plus-sign/solution/)

<p>You are given an integer <code>n</code>. You have an <code>n x n</code> binary grid <code>grid</code> with all values initially <code>1</code>'s except for some indices given in the array <code>mines</code>. The <code>i<sup>th</sup></code> element of the array <code>mines</code> is defined as <code>mines[i] = [x<sub>i</sub>, y<sub>i</sub>]</code> where <code>grid[x<sub>i</sub>][y<sub>i</sub>] == 0</code>.</p>

<p>Return <em>the order of the largest <strong>axis-aligned</strong> plus sign of </em>1<em>'s contained in </em><code>grid</code>. If there is none, return <code>0</code>.</p>

<p>An <strong>axis-aligned plus sign</strong> of <code>1</code>'s of order <code>k</code> has some center <code>grid[r][c] == 1</code> along with four arms of length <code>k - 1</code> going up, down, left, and right, and made of <code>1</code>'s. Note that there could be <code>0</code>'s or <code>1</code>'s beyond the arms of the plus sign, only the relevant area of the plus sign is checked for <code>1</code>'s.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/06/13/plus1-grid.jpg" style="width: 404px; height: 405px;">
<pre><strong>Input:</strong> n = 5, mines = [[4,2]]
<strong>Output:</strong> 2
<strong>Explanation:</strong> In the above grid, the largest plus sign can only be of order 2. One of them is shown.
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/06/13/plus2-grid.jpg" style="width: 84px; height: 85px;">
<pre><strong>Input:</strong> n = 1, mines = [[0,0]]
<strong>Output:</strong> 0
<strong>Explanation:</strong> There is no plus sign, so return 0.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 500</code></li>
	<li><code>1 &lt;= mines.length &lt;= 5000</code></li>
	<li><code>0 &lt;= x<sub>i</sub>, y<sub>i</sub> &lt; n</code></li>
	<li>All the pairs <code>(x<sub>i</sub>, y<sub>i</sub>)</code> are <strong>unique</strong>.</li>
</ul>


**Companies**:  
[Uber](https://leetcode.com/company/uber)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

**Similar Questions**:
* [Maximal Square (Medium)](https://leetcode.com/problems/maximal-square/)

## Solution 1.

```py
class Solution:
    def orderOfLargestPlusSign(self, n: int, mines: List[List[int]]) -> int:
        
        ## brute force O(N^3)
        zeros = set([(i,j) for i,j in mines])
        max_length = 0
        for i in range(n):
            for j in range(n):
                if (i,j) in zeros:
                    continue
                
                length = 0
                while 0<=(i+length)<n and 0<=(i-length)<n and \
                     0<=(j+length)<n and 0<=(j-length)<n and \
                    (i+length,j) not in zeros and (i-length,j) not in zeros and \
                    (i,j+length) not in zeros and (i,j-length) not in zeros:
                        length +=1
                print('position',(i,j),'with length',length)
                if length> max_length:
                    max_length = length
        return max_length
```

## Solution 2.

```py
class Solution:
    def orderOfLargestPlusSign(self, n: int, mines: List[List[int]]) -> int:
        ## use four matrix to store consequence 1 from left,right,up,down
        ## then for each position, check these four direction and get max_length
        ## O(n^2)
        max_length  = 0 
        zeros = set([(i,j) for i,j in mines])
        # design 4 matrix represent total continue 1s from left,right,up,down
        left,right,up,down = [[0 for _ in range(n)] for _ in range(n)],[[0 for _ in range(n)] for _ in range(n)],[[0 for _ in range(n)] for _ in range(n)],[[0 for _ in range(n)] for _ in range(n)]
        
        for i in range(0,n):
            for j in range(0,n):
                if (i,j) not in zeros:
                    if i!=0:
                        up[i][j] = up[i-1][j] + 1
                    else:
                        up[i][j] = 1
                    if j != 0:
                        left[i][j] = left[i][j-1] + 1
                    else:
                        left[i][j] = 1
                        
        for i in range(n-1,-1,-1):
            for j in range(n-1,-1,-1):
                if (i,j) not in zeros:
                    if i!=n-1:
                        down[i][j] = down[i+1][j] + 1
                    else:
                        down[i][j] = 1
                    if j != n-1:
                        right[i][j] = right[i][j+1] + 1
                    else:
                        right[i][j] = 1
        
        for i in range(0,n):
            for j in range(0,n):
                if (i,j) not in zeros:
                    length = min(left[i][j],right[i][j],up[i][j],down[i][j])
                    if length > max_length:
                        # print('in position',(i,j),'left',left[i][j],'right',right[i][j],'up',up[i][j],'down',down[i][j])
                        max_length = length
        return max_length
```