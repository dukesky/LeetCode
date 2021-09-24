# [317. Shortest Distance from All Buildings (Hard)](https://leetcode.com/problems/shortest-distance-from-all-buildings/solution/)

<p>You are given an <code>m x n</code> grid <code>grid</code> of values <code>0</code>, <code>1</code>, or <code>2</code>, where:</p>

<ul>
	<li>each <code>0</code> marks <strong>an empty land</strong> that you can pass by freely,</li>
	<li>each <code>1</code> marks <strong>a building</strong> that you cannot pass through, and</li>
	<li>each <code>2</code> marks <strong>an obstacle</strong> that you cannot pass through.</li>
</ul>

<p>You want to build a house on an empty land that reaches all buildings in the <strong>shortest total travel</strong> distance. You can only move up, down, left, and right.</p>

<p>Return <em>the <strong>shortest travel distance</strong> for such a house</em>. If it is not possible to build such a house according to the above rules, return <code>-1</code>.</p>

<p>The <strong>total travel distance</strong> is the sum of the distances between the houses of the friends and the meeting point.</p>

<p>The distance is calculated using <a href="http://en.wikipedia.org/wiki/Taxicab_geometry" target="_blank">Manhattan Distance</a>, where <code>distance(p1, p2) = |p2.x - p1.x| + |p2.y - p1.y|</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/14/buildings-grid.jpg" style="width: 413px; height: 253px;">
<pre><strong>Input:</strong> grid = [[1,0,2,0,1],[0,0,0,0,0],[0,0,1,0,0]]
<strong>Output:</strong> 7
<strong>Explanation:</strong> Given three buildings at (0,0), (0,4), (2,2), and an obstacle at (0,2).
The point (1,2) is an ideal empty land to build a house, as the total travel distance of 3+3+1=7 is minimal.
So return 7.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> grid = [[1,0]]
<strong>Output:</strong> 1
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> grid = [[1]]
<strong>Output:</strong> -1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 50</code></li>
	<li><code>grid[i][j]</code> is either <code>0</code>, <code>1</code>, or <code>2</code>.</li>
	<li>There will be <strong>at least one</strong> building in the <code>grid</code>.</li>
</ul>


**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [DoorDash](https://leetcode.com/company/doordash), [Google](https://leetcode.com/company/google)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:
* [Walls and Gates (Medium)](https://leetcode.com/problems/walls-and-gates/)
* [Best Meeting Point (Hard)](https://leetcode.com/problems/best-meeting-point/)
* [As Far from Land as Possible (Medium)](https://leetcode.com/problems/as-far-from-land-as-possible/)

## Solution 1.

```py
class Solution:
    def shortestDistance(self, grid: List[List[int]]) -> int:
        
        
        ## use dp to count distance from one house to all '0', change all other '1's as '2's BFS  O(mn)
        ## find the minimal total distance for sum of all house  
        ## total T: O(m^2*n^2)  S:O(m^2*n^2)
        directions = [(-1,0),(1,0),(0,-1),(0,1)]
        distances = []
        houses = set()
        obstacles = set()
        space = set()
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == 1:
                    houses.add((i,j))
                elif grid[i][j] == 2:
                    obstacles.add((i,j))
                else:
                    space.add((i,j))
        if not houses or not space:
            return -1
        
        for house in houses:
            ## BFS to calculate distance to house for each '0' point
            ## O(mn)
            distance = dict()
            stack = collections.deque()
            stack.append(house)
            dist = 0
            seen = set([])
            while stack:
                total_pos = len(stack)
                for _ in range(total_pos):
                    pos_x,pos_y = stack.popleft()
                    if (pos_x,pos_y) not in houses:
                        distance[(pos_x,pos_y)] = dist
                    for _x,_y in directions:
                        if (pos_x+_x,pos_y+_y) not in seen and (pos_x+_x,pos_y+_y) not in houses and (pos_x+_x,pos_y+_y) not in obstacles and 0<=pos_x+_x<len(grid) and 0<=pos_y+_y<len(grid[0]):
                            stack.append((pos_x+_x,pos_y+_y))
                            seen.add((pos_x+_x,pos_y+_y))
                
                dist += 1
            distances.append(distance)
        # for i,house in enumerate(houses):
        #     print(house, distances[i])
        
        min_dist = float('inf')
        for pos_x,pos_y in space:
            cur_dist = 0
            for distance in distances:
                if (pos_x,pos_y) not in distance:
                    cur_dist = float('inf')
                    break
                cur_dist += distance[(pos_x,pos_y)]
            if cur_dist < min_dist:
                min_dist = cur_dist
                
        if min_dist == float('inf'):
            return -1 
        return min_dist
```


## Solution 2.

```py

```