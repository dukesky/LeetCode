# [927. Three Equal Parts (Hard)](https://leetcode.com/problems/three-equal-parts/)

<p>You are given an array <code>arr</code> which consists of only zeros and ones, divide the array into <strong>three non-empty parts</strong> such that all of these parts represent the same binary value.</p>

<p>If it is possible, return any <code>[i, j]</code> with <code>i + 1 &lt; j</code>, such that:</p>

<ul>
	<li><code>arr[0], arr[1], ..., arr[i]</code> is the first part,</li>
	<li><code>arr[i + 1], arr[i + 2], ..., arr[j - 1]</code> is the second part, and</li>
	<li><code>arr[j], arr[j + 1], ..., arr[arr.length - 1]</code> is the third part.</li>
	<li>All three parts have equal binary values.</li>
</ul>

<p>If it is not possible, return <code>[-1, -1]</code>.</p>

<p>Note that the entire part is used when considering what binary value it represents. For example, <code>[1,1,0]</code> represents <code>6</code> in decimal, not <code>3</code>. Also, leading zeros <strong>are allowed</strong>, so <code>[0,1,1]</code> and <code>[1,1]</code> represent the same value.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> arr = [1,0,1,0,1]
<strong>Output:</strong> [0,3]
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> arr = [1,1,0,1,1]
<strong>Output:</strong> [-1,-1]
</pre><p><strong>Example 3:</strong></p>
<pre><strong>Input:</strong> arr = [1,1,0,0,1]
<strong>Output:</strong> [0,2]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>3 &lt;= arr.length &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>arr[i]</code> is <code>0</code> or <code>1</code></li>
</ul>


**Companies**:  
[Hotstar](https://leetcode.com/company/hotstar)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Math](https://leetcode.com/tag/math/)

## Solution 1.

```python
class Solution:
    def threeEqualParts(self, arr: List[int]) -> List[int]:
        
        ## brute force two for loop  O(N^3) -> O(N^2)
        
        ## two pointer  O(N)
        # left,right = 0,2
        # num1 = arr[:left+1]
        # num2 = arr[left+1:right]
        
        ## total 1's should divided by 3, the seperate between each group of 1's
        ## the last number's value is fixed, get this number and track the first two value
        total_ones = sum(arr)
        if total_ones % 3 != 0:
            return [-1,-1]
        else:
            each_ones = total_ones //3
            if each_ones == 0:
                return [0,2]
            right = len(arr) - 1
            end_zeros = 0
            while arr[right] == 0:
                end_zeros += 1
                right -= 1
        left = 0
        count_zero = 0
        count_one = 0
        while count_one < each_ones:
            if arr[left] == 1:
                count_one += 1
            left += 1
        while count_zero < end_zeros:
            if arr[left] == 0:
                count_zero += 1
            if arr[left] == 1:
                return [-1,-1]
            left += 1
        right = left
        left -= 1
        count_zero = 0
        count_one = 0
        while count_one < each_ones:
            if arr[right] == 1:
                count_one += 1
            right += 1
        while count_zero < end_zeros:
            if arr[right] == 0:
                count_zero += 1
            if arr[right] == 1:
                return [-1,-1]
            right += 1
        num1 = int(''.join([str(i) for i in arr[:left+1]]),2)
        num2 = int(''.join([str(i) for i in arr[left+1:right]]),2)
        num3 = int(''.join([str(i) for i in arr[right:]]),2)
        print(num1,num2,num3)
        if num1==num2 and num2==num3:
            return [left,right]
        else:
            return [-1,-1]
        
        

```