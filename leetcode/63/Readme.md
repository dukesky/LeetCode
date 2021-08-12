# [954. Array of Doubled Pairs (Medium)](https://leetcode.com/problems/array-of-doubled-pairs/)

<p>Given an integer array of even length <code>arr</code>, return <code>true</code><em> if it is possible to reorder </em><code>arr</code><em> such that </em><code>arr[2 * i + 1] = 2 * arr[2 * i]</code><em> for every </em><code>0 &lt;= i &lt; len(arr) / 2</code><em>, or </em><code>false</code><em> otherwise</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> arr = [3,1,3,6]
<strong>Output:</strong> false
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> arr = [2,1,2,6]
<strong>Output:</strong> false
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> arr = [4,-2,2,-4]
<strong>Output:</strong> true
<strong>Explanation:</strong> We can take two groups, [-2,-4] and [2,4] to form [-2,-4,2,4] or [2,4,-2,-4].
</pre>

<p><strong>Example 4:</strong></p>

<pre><strong>Input:</strong> arr = [1,2,4,16,8,4]
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= arr.length &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>arr.length</code> is even.</li>
	<li><code>-10<sup>5</sup> &lt;= arr[i] &lt;= 10<sup>5</sup></code></li>
</ul>


**Companies**:  
[Google](https://leetcode.com/company/google)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Greedy](https://leetcode.com/tag/greedy/), [Sorting](https://leetcode.com/tag/sorting/)

## Solution 1.

```py
class Solution:
    def canReorderDoubled(self, arr: List[int]) -> bool:
        
        ## example [1,4,2,8,16,32]
        ## O(NlogN)
        ##  split data into pos and neg and sorted, 
        pos_dict = dict()
        neg_dict = dict()
        zero = 0
        for num in arr:
            if num == 0:
                zero += 1
            elif num > 0:
                if num not in pos_dict:
                    pos_dict[num] = 1
                else:
                    pos_dict[num] += 1
            else:
                if num not in neg_dict:
                    neg_dict[num] = 1
                else:
                    neg_dict[num] += 1
            
        ## check zero
        if zero%2 == 1: return False
        ## check pos
        pos_nums = sorted(pos_dict.keys(),reverse=True)
        for num in pos_nums:
            while num in pos_dict:
                if num%2==0 and num//2 in pos_dict:
                    pos_dict[num] -= 1
                    if pos_dict[num] == 0:
                        del pos_dict[num]
                    pos_dict[num//2] -= 1
                    if pos_dict[num//2] == 0:
                        del pos_dict[num//2]
                else:
                    return False
        print(pos_dict)
        if pos_dict:
            return False
        
        
        ## check neg
        neg_nums = sorted(neg_dict.keys())
        for num in neg_nums:
            while num in neg_dict:
                if num%2==0 and num//2 in neg_dict:
                    neg_dict[num] -= 1
                    if neg_dict[num] == 0:
                        del neg_dict[num]
                    neg_dict[num//2] -= 1
                    if neg_dict[num//2] == 0:
                        del neg_dict[num//2]
                else:
                    return False
        print(neg_dict)
        if neg_dict:
            return False
        return True

```