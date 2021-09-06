# [1120. Maximum Average Subtree (Medium)](https://leetcode.com/problems/maximum-average-subtree/)

<p>Given the <code>root</code> of a binary tree, return <em>the maximum <strong>average</strong> value of a <strong>subtree</strong> of that tree</em>. Answers within <code>10<sup>-5</sup></code> of the actual answer will be accepted.</p>

<p>A <strong>subtree</strong> of a tree is any node of that tree plus all its descendants.</p>

<p>The <strong>average</strong> value of a tree is the sum of its values, divided by the number of nodes.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2019/04/09/1308_example_1.png" style="width: 132px; height: 123px;">
<pre><strong>Input:</strong> root = [5,6,1]
<strong>Output:</strong> 6.00000
<strong>Explanation:</strong> 
For the node with value = 5 we have an average of (5 + 6 + 1) / 3 = 4.
For the node with value = 6 we have an average of 6 / 1 = 6.
For the node with value = 1 we have an average of 1 / 1 = 1.
So the answer is 6 which is the maximum.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> root = [0,null,1]
<strong>Output:</strong> 1.00000
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[1, 10<sup>4</sup>]</code>.</li>
	<li><code>0 &lt;= Node.val &lt;= 10<sup>5</sup></code></li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon)

**Related Topics**:  
[Tree](https://leetcode.com/tag/tree/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Binary Tree](https://leetcode.com/tag/binary-tree/)

**Similar Questions**:
* [Count Nodes Equal to Sum of Descendants (Medium)](https://leetcode.com/problems/count-nodes-equal-to-sum-of-descendants/)

## Solution 1.

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def __init__(self):
        self.max_avg = float('-inf')
        
    def maximumAverageSubtree(self, root: Optional[TreeNode]) -> float:
        
        ## recursion function return average and total number of nodes in this tree
        def helper(root):
            if not root:
                return 0,0
            left_avg,left_nums = helper(root.left)
            right_avg,right_nums = helper(root.right)
            
            avg = round((left_avg*left_nums + right_avg*right_nums+root.val)/(left_nums+right_nums+1),5)
            if avg>self.max_avg:
                self.max_avg = avg
            return avg,left_nums+right_nums+1
        helper(root)
        return self.max_avg
```