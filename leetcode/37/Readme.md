# [25. Reverse Nodes in k-Group (Hard)](https://leetcode.com/problems/reverse-nodes-in-k-group/)

<p>Given a linked list, reverse the nodes of a linked list <em>k</em> at a time and return its modified list.</p>

<p><em>k</em> is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of <em>k</em> then left-out nodes, in the end, should remain as it is.</p>

<p>You may&nbsp;not alter the values in the list's nodes, only nodes themselves may be changed.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg" style="width: 542px; height: 222px;">
<pre><strong>Input:</strong> head = [1,2,3,4,5], k = 2
<strong>Output:</strong> [2,1,4,3,5]
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg" style="width: 542px; height: 222px;">
<pre><strong>Input:</strong> head = [1,2,3,4,5], k = 3
<strong>Output:</strong> [3,2,1,4,5]
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> head = [1,2,3,4,5], k = 1
<strong>Output:</strong> [1,2,3,4,5]
</pre>

<p><strong>Example 4:</strong></p>

<pre><strong>Input:</strong> head = [1], k = 1
<strong>Output:</strong> [1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list&nbsp;is in the range <code>sz</code>.</li>
	<li><code>1 &lt;= sz &lt;= 5000</code></li>
	<li><code>0 &lt;= Node.val &lt;= 1000</code></li>
	<li><code>1 &lt;= k &lt;= sz</code></li>
</ul>

<p>&nbsp;</p>
<strong>Follow-up:</strong> Can you solve the problem in O(1) extra memory space?

**Companies**:  
[Microsoft](https://leetcode.com/company/microsoft), [Amazon](https://leetcode.com/company/amazon), [Facebook](https://leetcode.com/company/facebook), [Apple](https://leetcode.com/company/apple), [eBay](https://leetcode.com/company/ebay), [Adobe](https://leetcode.com/company/adobe), [Google](https://leetcode.com/company/google), [Walmart Labs](https://leetcode.com/company/walmart-labs)

**Related Topics**:  
[Linked List](https://leetcode.com/tag/linked-list/), [Recursion](https://leetcode.com/tag/recursion/)

**Similar Questions**:
* [Swap Nodes in Pairs (Medium)](https://leetcode.com/problems/swap-nodes-in-pairs/)
* [Swapping Nodes in a Linked List (Medium)](https://leetcode.com/problems/swapping-nodes-in-a-linked-list/)

## Solution 1.

```python
Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

        # reverse a linked list:
        # pre = None
        # cur = root
        # nxt = root.next
        # for _ in range(length_of_linkedList):
        #     cur.next = pre
        #     pre = cur
        #     cur = nxt
        #     if nxt:
        #       nxt = nxt.next
        # return pre

class Solution:
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:

#         count how many full reverse, add the rest
#         one thing should be noticed is that each reverse's tail need connect to next reverse's tail, 
#         need maintail head_node and tail_node, previous head_node will connect to cur tail_node, connect after each full reverse


        if not head:
            return head
        length = 0
        node = head
        while node:
            length += 1
            node = node.next
        pre = None
        cur = head
        nxt = head.next
        for i in range(length // k):
            if i == 0:
                list_head = cur
            else:
                pre_list_head = list_head
                list_head = cur
            for _ in range(k):
                cur.next = pre
                pre  = cur
                cur = nxt
                if nxt:
                    nxt = nxt.next
            if i == 0:
                return_head = pre
            else:
                pre_list_head.next = pre
            print('list_head',list_head.val,'return head',return_head.val)
            list_head.next = cur
                    
        return return_head
```

## Solution 2.
``` py
class Solution:
    
    def reverseLinkedList(self, head, k):
        
        # Reverse k nodes of the given linked list.
        # This function assumes that the list contains 
        # atleast k nodes.
        new_head, ptr = None, head
        while k:
            
            # Keep track of the next node to process in the
            # original list
            next_node = ptr.next
            
            # Insert the node pointed to by "ptr"
            # at the beginning of the reversed list
            ptr.next = new_head
            new_head = ptr
            
            # Move on to the next node
            ptr = next_node
            
            # Decrement the count of nodes to be reversed by 1
            k -= 1
        
        # Return the head of the reversed list
        return new_head
                
    
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
        
        count = 0
        ptr = head
        
        # First, see if there are atleast k nodes
        # left in the linked list.
        while count < k and ptr:
            ptr = ptr.next
            count += 1
        
        # If we have k nodes, then we reverse them
        if count == k: 
            
            # Reverse the first k nodes of the list and
            # get the reversed list's head.
            reversedHead = self.reverseLinkedList(head, k)
            
            # Now recurse on the remaining linked list. Since
            # our recursion returns the head of the overall processed
            # list, we use that and the "original" head of the "k" nodes
            # to re-wire the connections.
            head.next = self.reverseKGroup(ptr, k)
            return reversedHead
        return head
```