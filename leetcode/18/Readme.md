# [363. Max Sum of Rectangle No Larger Than K (Hard)](https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/)

<p>Given an <code>m x n</code> matrix <code>matrix</code> and an integer <code>k</code>, return <em>the max sum of a rectangle in the matrix such that its sum is no larger than</em> <code>k</code>.</p>

<p>It is <strong>guaranteed</strong> that there will be a rectangle with a sum no larger than <code>k</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/18/sum-grid.jpg" style="width: 255px; height: 176px;">
<pre><strong>Input:</strong> matrix = [[1,0,1],[0,-2,3]], k = 2
<strong>Output:</strong> 2
<strong>Explanation:</strong> Because the sum of the blue rectangle [[0, 1], [-2, 3]] is 2, and 2 is the max number no larger than k (k = 2).
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> matrix = [[2,2,-1]], k = 3
<strong>Output:</strong> 3
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == matrix.length</code></li>
	<li><code>n == matrix[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 100</code></li>
	<li><code>-100 &lt;= matrix[i][j] &lt;= 100</code></li>
	<li><code>-10<sup>5</sup> &lt;= k &lt;= 10<sup>5</sup></code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> What if the number of rows is much larger than the number of columns?</p>


**Companies**:  
[Roblox](https://leetcode.com/company/roblox), [Google](https://leetcode.com/company/google), [Apple](https://leetcode.com/company/apple)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Binary Search](https://leetcode.com/tag/binary-search/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/), [Matrix](https://leetcode.com/tag/matrix/), [Ordered Set](https://leetcode.com/tag/ordered-set/)

## Solution 1.

```python
class Solution:
    def maxSumSubmatrix(self, matrix: List[List[int]], k: int) -> int:
        
        ## store the sum of left up corner to the current position
        ## check the reg one by one by iterate left up and right down corner
        ## exp: reg[(ai,bi),(aj,bj)] = sum(aj,bj) - sum(aj,bi) - sum(ai,bj) + sum(ai,bi)
        ## T: O(m^2*n^2)  S: O(m*n)   LTE
        rec_sum = [[0 for _ in range(len(matrix[0])+1)] for _ in range(len(matrix)+1)]
        for i in range(len(matrix)):
            for j in range(len(matrix[0])):
                rec_sum[i+1][j+1] = rec_sum[i][j+1] + rec_sum[i+1][j] + matrix[i][j] - rec_sum[i][j]
        # print(rec_sum)
        
        min_dif = float('inf')
        for i in range(0,len(rec_sum)):
            for j in range(0,len(rec_sum[0])):
                for p in range(i+1,len(rec_sum)):
                    for q in range(j+1,len(rec_sum[0])):
                        if p == 0 or q== 0:
                            continue
                        cur_sum = rec_sum[p][q] + rec_sum[i][j] - rec_sum[p][j] - rec_sum[i][q]
                        if cur_sum <= k and k - cur_sum < min_dif:
                            # print((i,j),(p,q))
                            # print('sum is', cur_sum)
                            min_dif = k - cur_sum
                            if min_dif == 0:
                                return k
        return k - min_dif
```

## Solution2.
```python
from sortedcontainers import SortedList
    
class Solution:
    def maxSumSubmatrix(self, M, k):
        ## similar as the first solution, but 
        ## transfer 2-D array into 1-D array
        ## and sorted pre-sum and use binary search
        ## to speed up each find with end pre_sum to find start position
        def countRangeSum(nums, U):
            SList, ans = SortedList([0]), -float("inf")
            for s in accumulate(nums):
                idx = SList.bisect_left(s - U) 
                if idx < len(SList): ans = max(ans, s - SList[idx])        
                SList.add(s)
            return ans
        
        m, n, ans = len(M), len(M[0]), -float("inf")
        
        for i, j in product(range(1, m), range(n)):
            M[i][j] += M[i-1][j]
                
        M = [[0]*n] + M
        
        for r1, r2 in combinations(range(m + 1), 2):
            row = [j - i for i, j in zip(M[r1], M[r2])]
            ans = max(ans, countRangeSum(row, k))
            
        return ans
```