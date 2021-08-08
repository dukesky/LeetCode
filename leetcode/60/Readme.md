# [1632. Rank Transform of a Matrix (Hard)](https://leetcode.com/problems/rank-transform-of-a-matrix/)

<p>Given an <code>m x n</code> <code>matrix</code>, return <em>a new matrix </em><code>answer</code><em> where </em><code>answer[row][col]</code><em> is the </em><em><strong>rank</strong> of </em><code>matrix[row][col]</code>.</p>

<p>The <strong>rank</strong> is an <strong>integer</strong> that represents how large an element is compared to other elements. It is calculated using the following rules:</p>

<ul>
	<li>The rank is an integer starting from <code>1</code>.</li>
	<li>If two elements <code>p</code> and <code>q</code> are in the <strong>same row or column</strong>, then:
	<ul>
		<li>If <code>p &lt; q</code> then <code>rank(p) &lt; rank(q)</code></li>
		<li>If <code>p == q</code> then <code>rank(p) == rank(q)</code></li>
		<li>If <code>p &gt; q</code> then <code>rank(p) &gt; rank(q)</code></li>
	</ul>
	</li>
	<li>The <strong>rank</strong> should be as <strong>small</strong> as possible.</li>
</ul>

<p>It is guaranteed that <code>answer</code> is unique under the given rules.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/18/rank1.jpg" style="width: 442px; height: 162px;">
<pre><strong>Input:</strong> matrix = [[1,2],[3,4]]
<strong>Output:</strong> [[1,2],[2,3]]
<strong>Explanation:</strong>
The rank of matrix[0][0] is 1 because it is the smallest integer in its row and column.
The rank of matrix[0][1] is 2 because matrix[0][1] &gt; matrix[0][0] and matrix[0][0] is rank 1.
The rank of matrix[1][0] is 2 because matrix[1][0] &gt; matrix[0][0] and matrix[0][0] is rank 1.
The rank of matrix[1][1] is 3 because matrix[1][1] &gt; matrix[0][1], matrix[1][1] &gt; matrix[1][0], and both matrix[0][1] and matrix[1][0] are rank 2.
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/18/rank2.jpg" style="width: 442px; height: 162px;">
<pre><strong>Input:</strong> matrix = [[7,7],[7,7]]
<strong>Output:</strong> [[1,1],[1,1]]
</pre>

<p><strong>Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/18/rank3.jpg" style="width: 601px; height: 322px;">
<pre><strong>Input:</strong> matrix = [[20,-21,14],[-19,4,19],[22,-47,24],[-19,4,19]]
<strong>Output:</strong> [[4,2,3],[1,3,4],[5,1,6],[1,3,4]]
</pre>

<p><strong>Example 4:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/18/rank4.jpg" style="width: 601px; height: 242px;">
<pre><strong>Input:</strong> matrix = [[7,3,6],[1,4,5],[9,8,2]]
<strong>Output:</strong> [[5,1,4],[1,2,3],[6,3,1]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == matrix.length</code></li>
	<li><code>n == matrix[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 500</code></li>
	<li><code>-10<sup>9</sup> &lt;= matrix[row][col] &lt;= 10<sup>9</sup></code></li>
</ul>


**Companies**:  
[Google](https://leetcode.com/company/google)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Greedy](https://leetcode.com/tag/greedy/), [Union Find](https://leetcode.com/tag/union-find/), [Graph](https://leetcode.com/tag/graph/), [Topological Sort](https://leetcode.com/tag/topological-sort/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:
* [Rank Transform of an Array (Easy)](https://leetcode.com/problems/rank-transform-of-an-array/)

## Solution 1.

```py

class Solution:
    def matrixRankTransform(self, matrix: List[List[int]]) -> List[List[int]]:
        
        ## total O(MN(M+N)) or O(N^3)   N- # of rows, M - # of cols
        ## first use a dictionary to store all row,col for val
        num_dict = defaultdict(list)
        for row in range(len(matrix)):
            for col in range(len(matrix[0])):
                num_dict[matrix[row][col]].append((row,col))
        # print(num_dict)
        
        ## find all ranks, for numbers from small to large, search it's same row and col, find the exist max number, rank would be + 1 
        ## if find same value in the same row/colum, put them in set, find the max rank, apply to all in set 
        res = [[0 for _ in range(len(matrix[0]))] for _ in range(len(matrix))]
        pos = []
        
        track_nums = sorted(num_dict.keys())
        for num in track_nums:       ## iterate through times O(MN)
            if len(num_dict[num]) == 1:  # no duplicate num
                row = num_dict[num][0][0]
                col = num_dict[num][0][1]
                res[row][col] = max(max(res[row]),max([res[i][col] for i in range(len(res))]))+1 # find max O(M+N)
            else:
                num_set = set(num_dict[num]) ## have duplicate num, check if share same value first 
                while num_set:
                    row,col = num_set.pop()
                    ## find save value share row/col of cur value, use BFS to find all  O(M+N) (could also use UNION FIND which cost less time?)
                    share_set = set([(row,col)])
                    queue = collections.deque([(row,col)])
                    while queue:
                        for _ in range(len(queue)):
                            (row,col) = queue.pop()
                            for i in range(len(matrix)):
                                if i!=row and matrix[i][col] == matrix[row][col] and (i,col) not in share_set:
                                    queue.appendleft((i,col))
                                    share_set.add((i,col))
                                    num_set.remove((i,col))
                            for j in range(len(matrix[0])):
                                if j!=col and matrix[row][j] == matrix[row][col] and (row,j) not in share_set:
                                    queue.appendleft((row,j))
                                    share_set.add((row,j))
                                    num_set.remove((row,j))
                    # print('share_set',share_set)
                    ## find max_rank shared for all same value number
                    max_val = 0
                    for row,col in share_set:
                        this_max =  max(max(res[row]),max([res[i][col] for i in range(len(res))]))
                        if this_max > max_val:
                            max_val = this_max
                    ## update max_val to all share set
                    for row,col in share_set:
                        res[row][col] = max_val+1
                    
        return res
```

## Solution 2.

```py
    ## solution2 optimized
    ## 1. for max value earch in row and col for one point, maintain two list, MaxRow and MaxCol, update in each iteration, then we can use O(1) time to find max value in specific row and col
    ## 2. avoid use BFS to find all same number share row or col, use Union find, which will cost log(N)+log(M) instead of O(M+N)
    
class Solution:
    def matrixRankTransform(self, matrix: List[List[int]]) -> List[List[int]]:
        
        ## total O(MN(log(N))) N- # of rows, M - # of cols
        ## first use a dictionary to store all row,col for val
        num_dict = defaultdict(list)
        for row in range(len(matrix)):
            for col in range(len(matrix[0])):
                num_dict[matrix[row][col]].append((row,col))
        # print(num_dict)
        
        ## find all ranks, for numbers from small to large, search from MaxRow and MaxCol, rank would be + 1, update MaxRow, MaxCol 
        ## if find same value in the same row/colum, put them in set, find the max rank, apply to all in set 
        res = [[0 for _ in range(len(matrix[0]))] for _ in range(len(matrix))]
        MaxRow = [0 for _ in range(len(matrix))]
        MaxCol = [0 for _ in range(len(matrix[0]))]
        track_nums = sorted(num_dict.keys())
        
        for num in track_nums:       ## iterate through times O(MN)
            if len(num_dict[num]) == 1:  # no duplicate num
                row = num_dict[num][0][0]
                col = num_dict[num][0][1]
                res[row][col] = max(MaxRow[row],MaxCol[col])+1 # find max O(M+N)
                MaxRow[row] = res[row][col]
                MaxCol[col] = res[row][col]
            else:
                num_set = set(num_dict[num]) ## have duplicate num, check if share same value first 
                col_dict = defaultdict(list)
                row_dict = defaultdict(list)
                for (row,col) in num_set:
                    col_dict[col].append(row)
                    row_dict[row].append(col)
                    
                while num_set:
                    row,col = num_set.pop()
                    ## find save value share row/col of cur value, use BFS to find all  O(M+N) (could also use UNION FIND which cost less time?)
                    share_set = set([(row,col)])
                    queue = collections.deque([(row,col)])
                    while queue:
                        for _ in range(len(queue)):
                            (row,col) = queue.pop()
                            for i in col_dict[col]:
                                if i!=row and  (i,col) not in share_set:
                                    queue.appendleft((i,col))
                                    share_set.add((i,col))
                                    num_set.remove((i,col))
                            for j in row_dict[row]:
                                if j!=col and (row,j) not in share_set:
                                    queue.appendleft((row,j))
                                    share_set.add((row,j))
                                    num_set.remove((row,j))
                    # print('share_set',share_set)
                    ## find max_rank shared for all same value number
                    max_val = 0
                    for row,col in share_set:
                        this_max =  max(MaxRow[row],MaxCol[col])
                        if this_max > max_val:
                            max_val = this_max
                    ## update max_val to all share set
                    for row,col in share_set:
                        res[row][col] = max_val+1
                        MaxRow[row] = res[row][col]
                        MaxCol[col] = res[row][col]
                    
        return res
    
    
```

## Solution 3.
 Solution LC provided with Union Find
```py
class Solution:
    def matrixRankTransform(self, matrix: List[List[int]]) -> List[List[int]]:
        m = len(matrix)
        n = len(matrix[0])

        # implement find and union
        def find(UF, x):
            if x != UF[x]:
                UF[x] = find(UF, UF[x])
            return UF[x]

        def union(UF, x, y):
            UF.setdefault(x, x)
            UF.setdefault(y, y)
            UF[find(UF, x)] = find(UF, y)

        # link row and col together
        UFs = {}  # UFs[v]: the Union-Find of value v
        for i in range(m):
            for j in range(n):
                v = matrix[i][j]
                if v not in UFs:
                    UFs[v] = {}
                # union i to j
                union(UFs[v], i, ~j)

        # put points into `value2index` dict, grouped by connection
        value2index = {}
        for i in range(m):
            for j in range(n):
                v = matrix[i][j]
                if v not in value2index:
                    value2index[v] = {}
                f = find(UFs[v], i)
                if f not in value2index[v]:
                    value2index[v][f] = []
                value2index[v][f].append((i, j))

        answer = [[0]*n for _ in range(m)]  # the required rank matrix
        rowmax = [0] * m  # rowmax[i]: the max rank in i row
        colmax = [0] * n  # colmax[j]: the max rank in j col
        for v in sorted(value2index.keys()):
            # update by connected points with same value
            for points in value2index[v].values():
                rank = 1
                for i, j in points:
                    rank = max(rank, max(rowmax[i], colmax[j]) + 1)
                for i, j in points:
                    answer[i][j] = rank
                    # update rowmax and colmax
                    rowmax[i] = max(rowmax[i], rank)
                    colmax[j] = max(colmax[j], rank)

        return answer

```