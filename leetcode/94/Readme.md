# [1293. Shortest Path in a Grid with Obstacles Elimination (Hard)](https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/)

<p>You are given an <code>m x n</code> integer matrix <code>grid</code> where each cell is either <code>0</code> (empty) or <code>1</code> (obstacle). You can move up, down, left, or right from and to an empty cell in <strong>one step</strong>.</p>

<p>Return <em>the minimum number of <strong>steps</strong> to walk from the upper left corner </em><code>(0, 0)</code><em> to the lower right corner </em><code>(m - 1, n - 1)</code><em> given that you can eliminate <strong>at most</strong> </em><code>k</code><em> obstacles</em>. If it is not possible to find such walk return <code>-1</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> 
grid = 
[[0,0,0],
&nbsp;[1,1,0],
 [0,0,0],
&nbsp;[0,1,1],
 [0,0,0]], 
k = 1
<strong>Output:</strong> 6
<strong>Explanation: 
</strong>The shortest path without eliminating any obstacle is 10.&nbsp;
The shortest path with one obstacle elimination at position (3,2) is 6. Such path is <code>(0,0) -&gt; (0,1) -&gt; (0,2) -&gt; (1,2) -&gt; (2,2) -&gt; <strong>(3,2)</strong> -&gt; (4,2)</code>.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> 
grid = 
[[0,1,1],
&nbsp;[1,1,1],
&nbsp;[1,0,0]], 
k = 1
<strong>Output:</strong> -1
<strong>Explanation: 
</strong>We need to eliminate at least two obstacles to find such a walk.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 40</code></li>
	<li><code>1 &lt;= k &lt;= m * n</code></li>
	<li><code>grid[i][j] == 0 <strong>or</strong> 1</code></li>
	<li><code>grid[0][0] == grid[m - 1][n - 1] == 0</code></li>
</ul>


**Companies**:  
[Google](https://leetcode.com/company/google)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:
* [Shortest Path to Get Food (Medium)](https://leetcode.com/problems/shortest-path-to-get-food/)

## Solution 1.

```py
class Solution:
    def shortestPath(self, grid: List[List[int]], k: int) -> int:
        
        ## BFS, for each position, store two value, (shorted_dist, n_obstacle_eliminated)
        ##grid = 
# [[0,0,0],       [(0,0),(1,0),(2,0)]    
#  [1,1,0],       [(1,1),(2,1),(3,0)]
#  [0,0,0],  ==>  [(6,0),(5,0),(4,0)]     
#  [0,1,1],       [(3,1),(6,1),(5,1)]         
#  [0,0,0]],      [(4,1),(5,1),(6,1)]          
        ## 
        def is_valid(row,col,n_obstacle):
            if 0<=row<len(grid) and 0<=col<len(grid[0]) and grid[row][col]+n_obstacle<=k and ((row,col) not in seen or seen[(row,col)]>n_obstacle):
                return True
            else:
                return False
            
        stack = collections.deque()
        stack.append((0,0,0,0))
        directions = [(-1,0),(1,0),(0,-1),(0,1)]
        seen = dict()
        
        if len(grid) == len(grid[0]) == 1:
            print('only one space')
            if is_valid(0,0,0):
                return 0
            else:
                return -1
            
        seen[(0,0)] = 0
            
        while stack:
            dist_length = len(stack)
            for _ in range(dist_length):
                row,col,dist,obs = stack.popleft()
                for dir_row,dir_col in directions:
                    if is_valid(row+dir_row,col+dir_col,obs):
                        stack.append((row+dir_row,col+dir_col,dist+1,obs+grid[row+dir_row][col+dir_col]))
                        seen[(row+dir_row,col+dir_col)]=obs+grid[row+dir_row][col+dir_col]
                        if row+dir_row == len(grid)-1 and col+dir_col == len(grid[0])-1:
                            return dist + 1
            # print(seen)
            # print(stack)
        return -1
```