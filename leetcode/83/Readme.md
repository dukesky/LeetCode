# [621. Task Scheduler (Medium)](https://leetcode.com/problems/task-scheduler/)

<p>Given a characters array <code>tasks</code>, representing the tasks a CPU needs to do, where each letter represents a different task. Tasks could be done in any order. Each task is done in one unit of time. For each unit of time, the CPU could complete either one task or just be idle.</p>

<p>However, there is a non-negative integer&nbsp;<code>n</code> that represents the cooldown period between&nbsp;two <b>same tasks</b>&nbsp;(the same letter in the array), that is that there must be at least <code>n</code> units of time between any two same tasks.</p>

<p>Return <em>the least number of units of times that the CPU will take to finish all the given tasks</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> tasks = ["A","A","A","B","B","B"], n = 2
<strong>Output:</strong> 8
<strong>Explanation:</strong> 
A -&gt; B -&gt; idle -&gt; A -&gt; B -&gt; idle -&gt; A -&gt; B
There is at least 2 units of time between any two same tasks.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> tasks = ["A","A","A","B","B","B"], n = 0
<strong>Output:</strong> 6
<strong>Explanation:</strong> On this case any permutation of size 6 would work since n = 0.
["A","A","A","B","B","B"]
["A","B","A","B","A","B"]
["B","B","B","A","A","A"]
...
And so on.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> tasks = ["A","A","A","A","A","A","B","C","D","E","F","G"], n = 2
<strong>Output:</strong> 16
<strong>Explanation:</strong> 
One possible solution is
A -&gt; B -&gt; C -&gt; A -&gt; D -&gt; E -&gt; A -&gt; F -&gt; G -&gt; A -&gt; idle -&gt; idle -&gt; A -&gt; idle -&gt; idle -&gt; A
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= task.length &lt;= 10<sup>4</sup></code></li>
	<li><code>tasks[i]</code> is upper-case English letter.</li>
	<li>The integer <code>n</code> is in the range <code>[0, 100]</code>.</li>
</ul>


**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Microsoft](https://leetcode.com/company/microsoft), [Uber](https://leetcode.com/company/uber), [Amazon](https://leetcode.com/company/amazon), [Rubrik](https://leetcode.com/company/rubrik), [Bloomberg](https://leetcode.com/company/bloomberg), [Salesforce](https://leetcode.com/company/salesforce)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Greedy](https://leetcode.com/tag/greedy/), [Sorting](https://leetcode.com/tag/sorting/), [Heap (Priority Queue)](https://leetcode.com/tag/heap-priority-queue/), [Counting](https://leetcode.com/tag/counting/)

**Similar Questions**:
* [Rearrange String k Distance Apart (Hard)](https://leetcode.com/problems/rearrange-string-k-distance-apart/)
* [Reorganize String (Medium)](https://leetcode.com/problems/reorganize-string/)
* [Maximum Number of Weeks for Which You Can Work (Medium)](https://leetcode.com/problems/maximum-number-of-weeks-for-which-you-can-work/)

## Solution 1.

```py 
class Solution:
    def leastInterval(self, tasks: List[str], n: int) -> int:
        
        ## find the longest same number, if has m, then the least length is (m-1)(n+1)+1,
        ## if have multiple same legnth numbers, has p numbers all has length m, then the least length is (m-1)(n+1)+p
        
        count = collections.defaultdict(int)
        for task in tasks:
            count[task] += 1
        
        max_count = float('-inf')
        nums = 0
        
        for task in count:
            if count[task] > max_count:
                max_count = count[task]
                nums = 1
            elif count[task] == max_count:
                nums += 1
        
        return max(len(tasks),(max_count-1)*(n+1)+nums)

```