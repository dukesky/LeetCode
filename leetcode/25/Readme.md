# [1338. Reduce Array Size to The Half (Medium)](https://leetcode.com/problems/reduce-array-size-to-the-half/)

<p>Given an array <code>arr</code>.&nbsp; You can choose a set of integers and remove all the occurrences of these integers in the array.</p>

<p>Return <em>the minimum size of the set</em> so that <strong>at least</strong> half of the integers of the array are removed.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> arr = [3,3,3,3,5,5,5,2,2,7]
<strong>Output:</strong> 2
<strong>Explanation:</strong> Choosing {3,7} will make the new array [5,5,5,2,2] which has size 5 (i.e equal to half of the size of the old array).
Possible sets of size 2 are {3,5},{3,2},{5,2}.
Choosing set {2,7} is not possible as it will make the new array [3,3,3,3,5,5,5] which has size greater than half of the size of the old array.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> arr = [7,7,7,7,7,7]
<strong>Output:</strong> 1
<strong>Explanation:</strong> The only possible set you can choose is {7}. This will make the new array empty.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> arr = [1,9]
<strong>Output:</strong> 1
</pre>

<p><strong>Example 4:</strong></p>

<pre><strong>Input:</strong> arr = [1000,1000,3,7]
<strong>Output:</strong> 1
</pre>

<p><strong>Example 5:</strong></p>

<pre><strong>Input:</strong> arr = [1,2,3,4,5,6,7,8,9,10]
<strong>Output:</strong> 5
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= arr.length &lt;= 10^5</code></li>
	<li><code>arr.length</code> is even.</li>
	<li><code>1 &lt;= arr[i] &lt;= 10^5</code></li>
</ul>

**Companies**:  
[Akuna Capital](https://leetcode.com/company/akuna-capital)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Greedy](https://leetcode.com/tag/greedy/), [Sorting](https://leetcode.com/tag/sorting/), [Heap (Priority Queue)](https://leetcode.com/tag/heap-priority-queue/)

## Solution 1.

```python

class Solution:
    def minSetSize(self, arr: List[int]) -> int:
        
        ## count number of occurance of each number and sorted based on occurance, delete number from high to low untill remain less than half
        ## time O(n + klogk)   n is the length of arr, k is the number of unique values in array
        full_length = len(arr)
        at_most_remain = full_length //2
        arr_dict = dict()
        for num in arr:
            if num not in arr_dict:
                arr_dict[num] = 1
            else:
                arr_dict[num] += 1
        occurance_list =sorted(arr_dict.values(), reverse=True)
        # print(occurance_list)
        remain = full_length
        pt = 0
        while remain > at_most_remain:
            remain -= occurance_list[pt]
            pt += 1
            
        return pt 

```