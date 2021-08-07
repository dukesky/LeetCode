# [1168. Optimize Water Distribution in a Village (Hard)](https://leetcode.com/problems/optimize-water-distribution-in-a-village/)

<p>There are <code>n</code> houses in a village. We want to supply water for all the houses by building wells and laying pipes.</p>

<p>For each house <code>i</code>, we can either build a well inside it directly with cost <code>wells[i - 1]</code> (note the <code>-1</code> due to <strong>0-indexing</strong>), or pipe in water from another well to it. The costs to lay pipes between houses are given by the array <code>pipes</code>, where each <code>pipes[j] = [house1<sub>j</sub>, house2<sub>j</sub>, cost<sub>j</sub>]</code> represents the cost to connect <code>house1<sub>j</sub></code> and <code>house2<sub>j</sub></code> together using a pipe. Connections are bidirectional.</p>

<p>Return <em>the minimum total cost to supply water to all houses</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<p><strong><img alt="" src="https://assets.leetcode.com/uploads/2019/05/22/1359_ex1.png" style="width: 189px; height: 196px;"></strong></p>

<pre><strong>Input:</strong> n = 3, wells = [1,2,2], pipes = [[1,2,1],[2,3,1]]
<strong>Output:</strong> 3
<strong>Explanation: </strong>
The image shows the costs of connecting houses using pipes.
The best strategy is to build a well in the first house with cost 1 and connect the other houses to it with cost 2 so the total cost is 3.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 10<sup>4</sup></code></li>
	<li><code>wells.length == n</code></li>
	<li><code>0 &lt;= wells[i] &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= pipes.length &lt;= 10<sup>4</sup></code></li>
	<li><code>pipes[j].length == 3</code></li>
	<li><code>1 &lt;= house1<sub>j</sub>, house2<sub>j</sub> &lt;= n</code></li>
	<li><code>0 &lt;= cost<sub>j</sub> &lt;= 10<sup>5</sup></code></li>
	<li><code>house1<sub>j</sub> != house2<sub>j</sub></code></li>
</ul>


**Companies**:  
[Google](https://leetcode.com/company/google), [Facebook](https://leetcode.com/company/facebook), [Yahoo](https://leetcode.com/company/yahoo)

**Related Topics**:  
[Union Find](https://leetcode.com/tag/union-find/), [Graph](https://leetcode.com/tag/graph/), [Minimum Spanning Tree](https://leetcode.com/tag/minimum-spanning-tree/)

## Solution 1.

```py

class Solution:
    def minCostToSupplyWater(self, n: int, wells: List[int], pipes: List[List[int]]) -> int:
        
        ## aim to connect/count all nodes
        ## minimal cost of connect all node + min(node.val) for each graph
        ## view as a ZERO node connect to all nodes with edge node.val, then problem goes to min edges to traverse the graph
        ## Build the graph,T:O(N+M)
        graphs = defaultdict(list)
        for [node1,node2,val] in pipes:
            graphs[node1].append((node2,val))
            graphs[node2].append((node1,val))
            
        # add edges to ZERO node
        for i,well in enumerate(wells):
            graphs[0].append((i+1,well))
        

        ## Prim's to traverse all nodes  O(N^2)  
        ## T: there are N while loop, N is the number of edges, in each while loop, lgN time to get shortest node, MlogN time to append connect node, but totaly append connect node will be N, so time in this step is O(mlogn + nlogn)  O((M+N)logN)  M-- number of nodes  N -- number of edges
        res_nodes = set([i for i in range(0,n+1)])
        seens = set()
        next_node_list = [(0,0)]
        total_cost = 0
        while res_nodes:

            dist, node = heapq.heappop(next_node_list)
            if node in seens:
                continue
            seens.add(node)
            res_nodes.remove(node)
            total_cost += dist
            for (connect_node,dist) in graphs[node]:
                if connect_node not in seens:
                    heapq.heappush(next_node_list,(dist,connect_node))
        
        return total_cost

```