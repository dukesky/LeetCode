# [135. Candy (Hard)](https://leetcode.com/problems/candy/)

<p>There are <code>n</code> children standing in a line. Each child is assigned a rating value given in the integer array <code>ratings</code>.</p>

<p>You are giving candies to these children subjected to the following requirements:</p>

<ul>
	<li>Each child must have at least one candy.</li>
	<li>Children with a higher rating get more candies than their neighbors.</li>
</ul>

<p>Return <em>the minimum number of candies you need to have to distribute the candies to the children</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> ratings = [1,0,2]
<strong>Output:</strong> 5
<strong>Explanation:</strong> You can allocate to the first, second and third child with 2, 1, 2 candies respectively.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> ratings = [1,2,2]
<strong>Output:</strong> 4
<strong>Explanation:</strong> You can allocate to the first, second and third child with 1, 2, 1 candies respectively.
The third child gets 1 candy because it satisfies the above two conditions.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == ratings.length</code></li>
	<li><code>1 &lt;= n &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>0 &lt;= ratings[i] &lt;= 2 * 10<sup>4</sup></code></li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Apple](https://leetcode.com/company/apple)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Greedy](https://leetcode.com/tag/greedy/)

## Solution 1.

```python
class Solution:
    def candy(self, ratings: List[int]) -> int:
        ## from left and from right, get total increase number to index i, find max(left, right) for each index
        ## T: O(n)  S:O(n)
        left,right = [0],[0]
        pre = ratings[0]
        count = 0
        for i in range(1,len(ratings)):
            if ratings[i] > pre:
                count +=1
                left.append(count)
            else:
                count = 0
                left.append(0)
            pre = ratings[i]
        pre = ratings[-1]
        count = 0
        for i in range(len(ratings)-2,-1,-1):
            if ratings[i] > pre:
                count += 1
                right.insert(0,count)
            else:
                count = 0
                right.insert(0,0)
            pre = ratings[i]
        # print(left)
        # print(right)
        return sum([max(left[i],right[i])+1 for i in range(len(left))])
```