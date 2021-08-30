# [663. Equal Tree Partition (Medium)](https://leetcode.com/problems/equal-tree-partition/)

<p>Given the <code>root</code> of a binary tree, return <code>true</code><em> if you can partition the tree into two trees with equal sums of values after removing exactly one edge on the original tree</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/05/03/split1-tree.jpg" style="width: 500px; height: 204px;">
<pre><strong>Input:</strong> root = [5,10,10,null,null,2,3]
<strong>Output:</strong> true
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/05/03/split2-tree.jpg" style="width: 277px; height: 302px;">
<pre><strong>Input:</strong> root = [1,2,10,null,null,2,20]
<strong>Output:</strong> false
<strong>Explanation:</strong> You cannot split the tree into two trees with equal sums after removing exactly one edge on the tree.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[1, 10<sup>4</sup>]</code>.</li>
	<li><code>-10<sup>5</sup> &lt;= Node.val &lt;= 10<sup>5</sup></code></li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon)

**Related Topics**:  
[Tree](https://leetcode.com/tag/tree/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Binary Tree](https://leetcode.com/tag/binary-tree/)

## Solution 1.

```py

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def checkEqualTree(self, root: Optional[TreeNode]) -> bool:
        
        ## get the total sum of all nodes
        ## traverse all nodes as root, find the sum of this subtree (use post-order), if sum is total/2, return true, else return false
        ## T:O(n),S:O(logn)
        
        def getSum(root):
            if not root:
                return 0
            return getSum(root.left) + root.val + getSum(root.right)
            
        def findHalf(root,target):
            if not root:
                return 0,False
            else:
                left_total,leftHalf = findHalf(root.left,target)
                right_total,rightHalf = findHalf(root.right,target)
                total = left_total + root.val + right_total
                isHalf = leftHalf or rightHalf

            if total == target:
                isHalf = True
            return total, isHalf
        
        total = getSum(root)
        print(total)
        if total%2 !=0:
            return False
        return findHalf(root.left,total//2)[1] or findHalf(root.right,total//2)[1]
        
```