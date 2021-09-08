# [206. Reverse Linked List (Easy)](https://leetcode.com/problems/reverse-linked-list/solution/)

<p>Given the <code>head</code> of a singly linked list, reverse the list, and return <em>the reversed list</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg" style="width: 542px; height: 222px;">
<pre><strong>Input:</strong> head = [1,2,3,4,5]
<strong>Output:</strong> [5,4,3,2,1]
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg" style="width: 182px; height: 222px;">
<pre><strong>Input:</strong> head = [1,2]
<strong>Output:</strong> [2,1]
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> head = []
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is the range <code>[0, 5000]</code>.</li>
	<li><code>-5000 &lt;= Node.val &lt;= 5000</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> A linked list can be reversed either iteratively or recursively. Could you implement both?</p>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Apple](https://leetcode.com/company/apple), [Adobe](https://leetcode.com/company/adobe), [Cisco](https://leetcode.com/company/cisco), [Google](https://leetcode.com/company/google), [Yandex](https://leetcode.com/company/yandex), [Nvidia](https://leetcode.com/company/nvidia), [eBay](https://leetcode.com/company/ebay), [Uber](https://leetcode.com/company/uber), [VMware](https://leetcode.com/company/vmware), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [HBO](https://leetcode.com/company/hbo)

**Related Topics**:  
[Linked List](https://leetcode.com/tag/linked-list/), [Recursion](https://leetcode.com/tag/recursion/)

**Similar Questions**:
* [Reverse Linked List II (Medium)](https://leetcode.com/problems/reverse-linked-list-ii/)
* [Binary Tree Upside Down (Medium)](https://leetcode.com/problems/binary-tree-upside-down/)
* [Palindrome Linked List (Easy)](https://leetcode.com/problems/palindrome-linked-list/)

## Solution 1.

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
 
        ## solution1: straight forward
#         if not head:
#             return head
        
#         pre = None
#         cur = head

        
#         while cur:
#             next = cur.next
#             cur.next = pre
#             pre = cur
#             cur = next
            
        
#         return pre
    
        ## solution2: recursion: each function return a reverse from this root to end

        # baseline
        if not head or not head.next:
            return head

        
        res = self.reverseList(head.next)
        head.next.next = head
        head.next = None

        return res

```