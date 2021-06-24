# [576. Out of Boundary Paths (Medium)](https://leetcode.com/problems/out-of-boundary-paths/)

<p>There is an <code>m x n</code> grid with a ball. The ball is initially at the position <code>[startRow, startColumn]</code>. You are allowed to move the ball to one of the four adjacent four cells in the grid (possibly out of the grid crossing the grid boundary). You can apply <strong>at most</strong> <code>maxMove</code> moves to the ball.</p>

<p>Given the five integers <code>m</code>, <code>n</code>, <code>maxMove</code>, <code>startRow</code>, <code>startColumn</code>, return the number of paths to move the ball out of the grid boundary. Since the answer can be very large, return it <strong>modulo</strong> <code>10<sup>9</sup> + 7</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/04/28/out_of_boundary_paths_1.png" style="width: 500px; height: 296px;">
<pre><strong>Input:</strong> m = 2, n = 2, maxMove = 2, startRow = 0, startColumn = 0
<strong>Output:</strong> 6
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/04/28/out_of_boundary_paths_2.png" style="width: 500px; height: 293px;">
<pre><strong>Input:</strong> m = 1, n = 3, maxMove = 3, startRow = 0, startColumn = 1
<strong>Output:</strong> 12
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= m, n &lt;= 50</code></li>
	<li><code>0 &lt;= maxMove &lt;= 50</code></li>
	<li><code>0 &lt;= startRow &lt;= m</code></li>
	<li><code>0 &lt;= startColumn &lt;= n</code></li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon)

**Related Topics**:  
[Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

**Similar Questions**:
* [Knight Probability in Chessboard (Medium)](https://leetcode.com/problems/knight-probability-in-chessboard/)

## Solution1 

```python
class Solution:
    def findPaths(self, m: int, n: int, maxMove: int, startRow: int, startColumn: int) -> int:
        
        self.total = 0
        MOD = 10**9 + 7
        add_ons = [(-1,0),(1,0),(0,-1),(0,1)]
        ## solution1
        # DFS?  TLE  O(4^maxMove) 
        
        def helper(m,n,startRow, startColumn, remainMove):
            if remainMove <= 0:
                return
            for add_on in add_ons:
                if 0<=startRow + add_on[0]< m and 0<=startColumn+add_on[1]<n:
                    helper(m,n,startRow + add_on[0],startColumn+add_on[1],remainMove-1)
                else:
                    self.total = (self.total + 1) % MOD
        
        helper(m,n,startRow, startColumn,maxMove)
        return self.total
```    
## solution2
``` python
class Solution:
    def findPaths(self, m: int, n: int, maxMove: int, startRow: int, startColumn: int) -> int:
        
        MOD = 10**9 + 7
        add_ons = [(-1,0),(1,0),(0,-1),(0,1)]        
        ## iterate by number of Movement  O(maxMove*m*n) 
        ## use two movemap of m*n to store in step k and step k-1 the times t of move to position i,j, so in step k, the total add is number of go out of bound for position in step k-1 p*number of times appear in this position t -- p*t
        pre_movemap,cur_movemap = [[0 for _ in range(n)] for _ in range(m)], [[0 for _ in range(n)] for _ in range(m)]
        total = 0
        pre_movemap[startRow][startColumn] = 1
        for _ in range(maxMove):
            for i in range(0,m):
                for j in range(0,n):
                    if pre_movemap[i][j] >= 1:
                        print(i,j,'has 1')
                        for add_on in add_ons:
                            if 0<=i+add_on[0]<m and 0<=j+add_on[1]<n:
                                cur_movemap[i+add_on[0]][j+add_on[1]] +=pre_movemap[i][j]
                            else:
                                print('pos',(i,j),'to',(i+add_on[0],j+add_on[1]))
                                total = (total+pre_movemap[i][j]) % MOD
            
            pre_movemap = cur_movemap
            cur_movemap = [[0 for _ in range(n)] for _ in range(m)]
            print(pre_movemap,total)
        return total
```