# [827. Making A Large Island (Hard)](https://leetcode.com/problems/making-a-large-island/)

<p>You are given an <code>n x n</code> binary matrix <code>grid</code>. You are allowed to change <strong>at most one</strong> <code>0</code> to be <code>1</code>.</p>

<p>Return <em>the size of the largest <strong>island</strong> in</em> <code>grid</code> <em>after applying this operation</em>.</p>

<p>An <strong>island</strong> is a 4-directionally connected group of <code>1</code>s.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> grid = [[1,0],[0,1]]
<strong>Output:</strong> 3
<strong>Explanation:</strong> Change one 0 to 1 and connect two 1s, then we get an island with area = 3.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> grid = [[1,1],[1,0]]
<strong>Output:</strong> 4
<strong>Explanation: </strong>Change the 0 to 1 and make the island bigger, only one island with area = 4.</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> grid = [[1,1],[1,1]]
<strong>Output:</strong> 4
<strong>Explanation:</strong> Can't change any 0 to 1, only one island with area = 4.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 &lt;= n &lt;= 500</code></li>
	<li><code>grid[i][j]</code> is either <code>0</code> or <code>1</code>.</li>
</ul>

**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Apple](https://leetcode.com/company/apple)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Union Find](https://leetcode.com/tag/union-find/), [Matrix](https://leetcode.com/tag/matrix/)

## Solution 1.

```py

class Solution:
    def largestIsland(self, grid: List[List[int]]) -> int:
        
        ## store each position [total_size_of_connect_point, area_identify_num]  O(N^2)
        ## for each 0, search 4 sides of this pos, accumulate all area sum 
        res_graph = [[[0,0] for _ in range(len(grid))] for _ in range(len(grid[0]))]
        ## step1: find all connect areas with shape --> BFS
        add_ons = [[0,-1],[0,1],[-1,0],[1,0]]
        area_count = 1
        seen = set()
        
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                ## find a new pos
                if grid[i][j] == 1 and (i,j) not in seen:
                    ## use BFS to store all connect points 1 to pos_set and seen
                    pos_set = set()
                    pos_set.add((i,j))
                    seen.add((i,j))
                    queue = collections.deque([(i,j)])
                    while queue:
                        n = len(queue)
                        for _ in range(n):
                            cur_pos_i,cur_pos_j = queue.pop()
                            for add_on_i,add_on_j in add_ons:
                                ## find a new connected 1
                                if 0<=add_on_i+cur_pos_i<len(grid) and 0<=add_on_j+cur_pos_j<len(grid[0]) and grid[add_on_i+cur_pos_i][add_on_j+cur_pos_j] == 1 and (add_on_i+cur_pos_i,add_on_j+cur_pos_j) not in seen:
                                    queue.appendleft((cur_pos_i+add_on_i,cur_pos_j+add_on_j))
                                    pos_set.add((cur_pos_i+add_on_i,cur_pos_j+add_on_j))
                                    seen.add((cur_pos_i+add_on_i,cur_pos_j+add_on_j))
                    
                    size = len(pos_set)
                    print('find one area',area_count,'connect of size',size, pos_set)
                    for pos_i,pos_j in pos_set:
                        res_graph[pos_i][pos_j] = [size,area_count]
                    area_count += 1
        if res_graph[0][0][0] == len(grid)*len(grid[0]):
            return len(grid) * len(grid[0])
        
        max_area = 0
        
        for i in range(0,len(grid)):
            for j in range(0,len(grid[0])):
                if grid[i][j] == 0:
                    areas = set()
                    area = 1
                    for add_on_i,add_on_j in add_ons:
                        if 0<=i+add_on_i<len(grid) and 0<=j+add_on_j<len(grid[0]) and grid[i+add_on_i][j+add_on_j]==1 and res_graph[i+add_on_i][j+add_on_j][1] not in areas:
                            area += res_graph[i+add_on_i][j+add_on_j][0]
                            areas.add(res_graph[i+add_on_i][j+add_on_j][1])
                    if area> max_area:
                        max_area = area
        return max_area
                    

```