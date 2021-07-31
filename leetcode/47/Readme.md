# [542. 01 Matrix (Medium)](https://leetcode.com/problems/01-matrix/)

<p>Given an <code>m x n</code> binary matrix <code>mat</code>, return <em>the distance of the nearest </em><code>0</code><em> for each cell</em>.</p>

<p>The distance between two adjacent cells is <code>1</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/04/24/01-1-grid.jpg" style="width: 253px; height: 253px;">
<pre><strong>Input:</strong> mat = [[0,0,0],[0,1,0],[0,0,0]]
<strong>Output:</strong> [[0,0,0],[0,1,0],[0,0,0]]
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/04/24/01-2-grid.jpg" style="width: 253px; height: 253px;">
<pre><strong>Input:</strong> mat = [[0,0,0],[0,1,0],[1,1,1]]
<strong>Output:</strong> [[0,0,0],[0,1,0],[1,2,1]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == mat.length</code></li>
	<li><code>n == mat[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 10<sup>4</sup></code></li>
	<li><code>1 &lt;= m * n &lt;= 10<sup>4</sup></code></li>
	<li><code>mat[i][j]</code> is either <code>0</code> or <code>1</code>.</li>
	<li>There is at least one <code>0</code> in <code>mat</code>.</li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Google](https://leetcode.com/company/google), [Uber](https://leetcode.com/company/uber), [Apple](https://leetcode.com/company/apple)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:
* [Shortest Path to Get Food (Medium)](https://leetcode.com/problems/shortest-path-to-get-food/)

## Solution 1.

```py
class Solution:
    def updateMatrix(self, mat: List[List[int]]) -> List[List[int]]:
        
        ## solution1:
        ## use BFS, maintain a set of each (row,col) pair that the position we see before
        ## first find all 0, then find all near pos
        res = mat.copy()
        seen = set()
        add_ons = [[0,-1],[0,1],[-1,0],[1,0]]
        for i,row in enumerate(mat):
            for j,num in enumerate(row):
                if num == 0:
                    seen.add((i,j))
        queue = collections.deque(list(seen))
        level = 1
        while queue:
            n_nodes = len(queue)
            # print(n_nodes,level,queue,seen)
            for _ in range(n_nodes):
                node_i,node_j = queue.pop()
                for add_on_i,add_on_j in add_ons:
                    # print((node_i,node_j),(add_on_i,add_on_j))
                    if 0<=node_i + add_on_i<len(mat) and 0<=node_j + add_on_j<len(mat[0]) and (node_i + add_on_i,node_j+add_on_j) not in seen:
                        seen.add((node_i + add_on_i,node_j+add_on_j))
                        queue.appendleft((node_i + add_on_i,node_j+add_on_j))
                        res[node_i + add_on_i][node_j+add_on_j] = level
            level += 1
        return res
        
            
            
        
        ## solution2: is it possible maintain 4 direction distance to one?

```