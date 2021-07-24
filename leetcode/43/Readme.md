# [814. Binary Tree Pruning (Medium)](https://leetcode.com/problems/binary-tree-pruning/)

<p>Given the <code>root</code> of a binary tree, return <em>the same tree where every subtree (of the given tree) not containing a </em><code>1</code><em> has been removed</em>.</p>

<p>A subtree of a node <code>node</code> is <code>node</code> plus every node that is a descendant of <code>node</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/06/1028_2.png" style="width: 500px; height: 140px;">
<pre><strong>Input:</strong> root = [1,null,0,0,1]
<strong>Output:</strong> [1,null,0,null,1]
<strong>Explanation:</strong> 
Only the red nodes satisfy the property "every subtree not containing a 1".
The diagram on the right represents the answer.
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/06/1028_1.png" style="width: 500px; height: 115px;">
<pre><strong>Input:</strong> root = [1,0,1,0,0,0,1]
<strong>Output:</strong> [1,null,1,null,1]
</pre>

<p><strong>Example 3:</strong></p>
<img alt="" src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/05/1028.png" style="width: 500px; height: 134px;">
<pre><strong>Input:</strong> root = [1,1,0,1,1,0,1,0]
<strong>Output:</strong> [1,1,0,1,1,null,1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[1, 200]</code>.</li>
	<li><code>Node.val</code> is either <code>0</code> or <code>1</code>.</li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google)

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

#    1
#  /  \
#  1   0
# /\   /\
# 0 1  0 1
class Solution:
    def pruneTree(self, root: TreeNode) -> TreeNode:
        ## use recursion, each recursion function return either this node or None,
        ## check node value, it's left and right child value
        ## 1. if node is none: return None (base)
        ## 2. if node is 1: return node, with new left and right node
        ## 3. if node is 0: check if left and right is node
        ## T: O(n)
        if not root:
            return None
        left_node = None
        right_node = None
        if root.left:
            left_node = self.pruneTree(root.left)
        if root.right:
            right_node = self.pruneTree(root.right)
        if root.val:
            root.left = left_node
            root.right = right_node
            return root
        else:
            if not left_node and not right_node:
                return None
            else:
                root.left = left_node
                root.right = right_node
                return root
        
```