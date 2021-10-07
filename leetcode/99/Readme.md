# [426. Convert Binary Search Tree to Sorted Doubly Linked List (Medium)](https://leetcode.com/problems/convert-binary-search-tree-to-sorted-doubly-linked-list/)

<p>Convert a <strong>Binary Search Tree</strong> to a sorted <strong>Circular Doubly-Linked List</strong> in place.</p>

<p>You can think of the left and right pointers as synonymous to the predecessor and successor pointers in a doubly-linked list. For a circular doubly linked list, the predecessor of the first element is the last element, and the successor of the last element is the first element.</p>

<p>We want to do the transformation <strong>in place</strong>. After the transformation, the left pointer of the tree node should point to its predecessor, and the right pointer should point to its successor. You should return the pointer to the smallest element of the linked list.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<p><img src="https://assets.leetcode.com/uploads/2018/10/12/bstdlloriginalbst.png" style="width: 100%; max-width: 300px;"></p>

<pre><strong>Input:</strong> root = [4,2,5,1,3]

<img src="https://assets.leetcode.com/uploads/2018/10/12/bstdllreturndll.png" style="width: 100%; max-width: 450px;">
<strong>Output:</strong> [1,2,3,4,5]

<strong>Explanation:</strong> The figure below shows the transformed BST. The solid line indicates the successor relationship, while the dashed line means the predecessor relationship.
<img src="https://assets.leetcode.com/uploads/2018/10/12/bstdllreturnbst.png" style="width: 100%; max-width: 450px;">
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> root = [2,1,3]
<strong>Output:</strong> [1,2,3]
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> root = []
<strong>Output:</strong> []
<strong>Explanation:</strong> Input is an empty tree. Output is also an empty Linked List.
</pre>

<p><strong>Example 4:</strong></p>

<pre><strong>Input:</strong> root = [1]
<strong>Output:</strong> [1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 2000]</code>.</li>
	<li><code>-1000 &lt;= Node.val &lt;= 1000</code></li>
	<li>All the values of the tree are <strong>unique</strong>.</li>
</ul>


**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft)

**Related Topics**:  
[Linked List](https://leetcode.com/tag/linked-list/), [Stack](https://leetcode.com/tag/stack/), [Tree](https://leetcode.com/tag/tree/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Binary Search Tree](https://leetcode.com/tag/binary-search-tree/), [Binary Tree](https://leetcode.com/tag/binary-tree/), [Doubly-Linked List](https://leetcode.com/tag/doubly-linked-list/)

**Similar Questions**:
* [Binary Tree Inorder Traversal (Easy)](https://leetcode.com/problems/binary-tree-inorder-traversal/)

## Solution 1.

```py
"""
# Definition for a Node.
class Node:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
"""

class Solution:

    def treeToDoublyList(self, root: 'Node') -> 'Node':
        
        ## recursion, 
        
        
        ## in-order traverse, with record of previous node
        
        if not root:
            return None
        def helper(root):
        
            if not root.left and not root.right:
                print('touch the end',root.val)
                return root,root
            print('current node',root.val)
            left_return,right_return = root,root
            if root.left:
                previous_small_node,previous_large_node = helper(root.left)
                root.left = previous_large_node
                root.left.right = root
                print(root.val,'left connect to',previous_large_node.val)
                left_return = previous_small_node
            if root.right:
                next_small_node,next_large_node = helper(root.right)
                print(root.val,'right connect to',next_small_node.val)
                root.right = next_small_node
                root.right.left = root
                right_return = next_large_node
            
            return left_return, right_return
        
        head,end = helper(root)
        print(head.val,end.val)
        head.left = end
        end.right = head
        return head
```


## Solution 2.

```py
class Solution:
    def treeToDoublyList(self, root: 'Node') -> 'Node':
        def helper(node):
            """
            Performs standard inorder traversal:
            left -> node -> right
            and links all nodes into DLL
            """
            nonlocal last, first
            if node:
                # left
                helper(node.left)
                # node 
                if last:
                    # link the previous node (last)
                    # with the current one (node)
                    last.right = node
                    node.left = last
                else:
                    # keep the smallest node
                    # to close DLL later on
                    first = node        
                last = node
                # right
                helper(node.right)
        
        if not root:
            return None
        
        # the smallest (first) and the largest (last) nodes
        first, last = None, None
        helper(root)
        # close DLL
        last.right = first
        first.left = last
        return first
```