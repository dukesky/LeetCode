# [118. Pascal's Triangle (Easy)](https://leetcode.com/problems/pascals-triangle/)

<p>Given an integer <code>numRows</code>, return the first numRows of <strong>Pascal's triangle</strong>.</p>

<p>In <strong>Pascal's triangle</strong>, each number is the sum of the two numbers directly above it as shown:</p>
<img alt="" src="https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif" style="height:240px; width:260px">
<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> numRows = 5
<strong>Output:</strong> [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> numRows = 1
<strong>Output:</strong> [[1]]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= numRows &lt;= 30</code></li>
</ul>


**Companies**:  
[Microsoft](https://leetcode.com/company/microsoft), [Google](https://leetcode.com/company/google), [Apple](https://leetcode.com/company/apple), [Adobe](https://leetcode.com/company/adobe), [Amazon](https://leetcode.com/company/amazon), [Uber](https://leetcode.com/company/uber), [Yahoo](https://leetcode.com/company/yahoo), [Goldman Sachs](https://leetcode.com/company/goldman-sachs)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/)

**Similar Questions**:
* [Pascal's Triangle II (Easy)](https://leetcode.com/problems/pascals-triangle-ii/)

## Solution 1.

```python
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        
        ## Iterate level by level
        ## Time: O(n^2)
        ## Soace: O(n)
        if numRows == 1:
            return [[1]]
        result = []
        pre = [1]
        result.append(pre)
        for _ in range(numRows-1):
            now = []
            for i in range(0,len(pre)+1):
                if i==0:
                    now.append(pre[i])
                elif i==len(pre):
                    now.append(pre[i-1])
                else:
                    now.append(pre[i-1]+pre[i])
            result.append(list(now))
            pre = now
            
        return result
```