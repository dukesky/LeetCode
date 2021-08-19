# [1339. Maximum Product of Splitted Binary Tree (Medium)](https://leetcode.com/problems/maximum-product-of-splitted-binary-tree/)

<p>Given the <code>root</code> of a binary tree, split the binary tree into two subtrees by removing one edge such that the product of the sums of the subtrees is maximized.</p>

<p>Return <em>the maximum product of the sums of the two subtrees</em>. Since the answer may be too large, return it <strong>modulo</strong> <code>10<sup>9</sup> + 7</code>.</p>

<p><strong>Note</strong> that you need to maximize the answer before taking the mod and not after taking it.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/01/21/sample_1_1699.png" style="width: 500px; height: 167px;">
<pre><strong>Input:</strong> root = [1,2,3,4,5,6]
<strong>Output:</strong> 110
<strong>Explanation:</strong> Remove the red edge and get 2 binary trees with sum 11 and 10. Their product is 110 (11*10)
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/01/21/sample_2_1699.png" style="width: 500px; height: 211px;">
<pre><strong>Input:</strong> root = [1,null,2,3,4,null,null,5,6]
<strong>Output:</strong> 90
<strong>Explanation:</strong> Remove the red edge and get 2 binary trees with sum 15 and 6.Their product is 90 (15*6)
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> root = [2,3,9,10,7,8,6,5,4,11,1]
<strong>Output:</strong> 1025
</pre>

<p><strong>Example 4:</strong></p>

<pre><strong>Input:</strong> root = [1,1]
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[2, 5 * 10<sup>4</sup>]</code>.</li>
	<li><code>1 &lt;= Node.val &lt;= 10<sup>4</sup></code></li>
</ul>


**Companies**:  
[ByteDance](https://leetcode.com/company/bytedance), [Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft)

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
    def maxProduct(self, root: Optional[TreeNode]) -> int:
        
        ## post-order can traverse a tree
        ## get total sum and sum of each tree, find the closest sub-tree sum to total/2
        MOD = 10**9+7
        tree_sums = []
        
        def get_tree_sum(root):
            if not root:
                return 0
            
            left = get_tree_sum(root.left)
            right= get_tree_sum(root.right)
            tree_sums.append(left+right+root.val)
            return left+right+root.val
        
        get_tree_sum(root)
        print(tree_sums)
        total = tree_sums[-1]
        dist = float('inf')
        min_sub_sum = 0
        for sub_sum in tree_sums:
            if abs(sub_sum - total/2)<dist:
                dist = abs(sub_sum - total/2)
                min_sub_sum = sub_sum
        return ((total-min_sub_sum)%MOD * min_sub_sum%MOD)%MOD
```