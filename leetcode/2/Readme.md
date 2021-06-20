# [1905. Count Sub Islands (Medium)](https://leetcode.com/problems/count-sub-islands/)

<p>You are given two <code>m x n</code> binary matrices <code>grid1</code> and <code>grid2</code> containing only <code>0</code>'s (representing water) and <code>1</code>'s (representing land). An <strong>island</strong> is a group of <code>1</code>'s connected <strong>4-directionally</strong> (horizontal or vertical). Any cells outside of the grid are considered water cells.</p>

<p>An island in <code>grid2</code> is considered a <strong>sub-island </strong>if there is an island in <code>grid1</code> that contains <strong>all</strong> the cells that make up <strong>this</strong> island in <code>grid2</code>.</p>

<p>Return the <em><strong>number</strong> of islands in </em><code>grid2</code> <em>that are considered <strong>sub-islands</strong></em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/06/10/test1.png" style="width: 493px; height: 205px;">
<pre><strong>Input:</strong> grid1 = [[1,1,1,0,0],[0,1,1,1,1],[0,0,0,0,0],[1,0,0,0,0],[1,1,0,1,1]], grid2 = [[1,1,1,0,0],[0,0,1,1,1],[0,1,0,0,0],[1,0,1,1,0],[0,1,0,1,0]]
<strong>Output:</strong> 3
<strong>Explanation: </strong>In the picture above, the grid on the left is grid1 and the grid on the right is grid2.
The 1s colored red in grid2 are those considered to be part of a sub-island. There are three sub-islands.
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/06/03/testcasex2.png" style="width: 491px; height: 201px;">
<pre><strong>Input:</strong> grid1 = [[1,0,1,0,1],[1,1,1,1,1],[0,0,0,0,0],[1,1,1,1,1],[1,0,1,0,1]], grid2 = [[0,0,0,0,0],[1,1,1,1,1],[0,1,0,1,0],[0,1,0,1,0],[1,0,0,0,1]]
<strong>Output:</strong> 2 
<strong>Explanation: </strong>In the picture above, the grid on the left is grid1 and the grid on the right is grid2.
The 1s colored red in grid2 are those considered to be part of a sub-island. There are two sub-islands.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == grid1.length == grid2.length</code></li>
	<li><code>n == grid1[i].length == grid2[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 500</code></li>
	<li><code>grid1[i][j]</code> and <code>grid2[i][j]</code> are either <code>0</code> or <code>1</code>.</li>
</ul>


**Companies**:  
[Twitter](https://leetcode.com/company/twitter)

**Related Topics**:  
[Depth-first Search](https://leetcode.com/tag/depth-first-search/), [Union Find](https://leetcode.com/tag/union-find/)

**Similar Questions**:
* [Number of Islands (Medium)](https://leetcode.com/problems/number-of-islands/)
* [Number of Distinct Islands (Medium)](https://leetcode.com/problems/number-of-distinct-islands/)

## Solution 1.

```python
// OJ: https://leetcode.com/problems/count-sub-islands/
// Author: Please set your name in options page
// Time: O()
// Space: O()
class Solution:
    def countSubIslands(self, grid1: List[List[int]], grid2: List[List[int]]) -> int:
        islands = []
        grids = set()
        for i in range(0,len(grid2)):
            for j in range(0,len(grid2[0])):
                grids.add((i,j))
        ## bfs search all islands in grid2
        add_ons = [[-1,0],[1,0],[0,-1],[0,1]]
        while grids:
            point = grids.pop()
            island = []
            if grid2[point[0]][point[1]] == 1:
                stack = collections.deque()
                stack.appendleft(point)
                while stack:
                    for _ in range(0,len(stack)):
                        point = stack.pop()
                        island.append(point)
                        for add_on in add_ons:
                            if 0<=point[0]+add_on[0] < len(grid2) and 0<=point[1]+add_on[1] < len(grid2[0]) and (point[0]+add_on[0],point[1]+add_on[1]) in grids:
                                if grid2[point[0]+add_on[0]][point[1]+add_on[1]] == 1:
                                    stack.appendleft((point[0]+add_on[0],point[1]+add_on[1]))
                                grids.remove((point[0]+add_on[0],point[1]+add_on[1]))
                    # print(island)
            if island:
                islands.append(island)
        # print(islands)
        result = len(islands)
        for island in islands:
            for point in island:
                if grid1[point[0]][point[1]] ==0:
                    result -= 1
                    break
        return result
```