# [366. Find Leaves of Binary Tree (Medium)](https://leetcode.com/problems/find-leaves-of-binary-tree/)

<p>Given the <code>root</code> of a binary tree, collect a tree's nodes as if you were doing this:</p>

<ul>
	<li>Collect all the leaf nodes.</li>
	<li>Remove all the leaf&nbsp;nodes.</li>
	<li>Repeat until the tree is empty.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/16/remleaves-tree.jpg" style="width: 500px; height: 215px;">
<pre><strong>Input:</strong> root = [1,2,3,4,5]
<strong>Output:</strong> [[4,5,3],[2],[1]]
Explanation:
[[3,5,4],[2],[1]] and [[3,4,5],[2],[1]] are also considered correct answers since per each level it does not matter the order on which elements are returned.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> root = [1]
<strong>Output:</strong> [[1]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[1, 100]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
</ul>


**Companies**:  
[LinkedIn](https://leetcode.com/company/linkedin), [Amazon](https://leetcode.com/company/amazon)

**Related Topics**:  
[Tree](https://leetcode.com/tag/tree/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Binary Tree](https://leetcode.com/tag/binary-tree/)

## Solution 1.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:

    def findLeaves(self, root: TreeNode) -> List[List[int]]:
        
        ## transfer to get_height of each node (leave is zero, increase of parents, parent get the max of two children)
        leaves = []
        def get_height(root):
            if not root:
                return -1
            if not root.left and not root.right:
                leaves.append((root.val,0))
                return 0
            
            height =  max(get_height(root.left),get_height(root.right))+1
            leaves.append((root.val,height))
            return height
        get_height(root)
        print(leaves)
        num_dict = dict()
        for val,key in leaves:
            if key not in num_dict:
                num_dict[key] = [val]
            else:
                num_dict[key].append(val)
        
        result = []
        for i in range(max(num_dict.keys())+1):
            result.append(num_dict[i])
        return result
            
```