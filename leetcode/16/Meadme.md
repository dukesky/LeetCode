# [1004. Max Consecutive Ones III (Medium)](https://leetcode.com/problems/max-consecutive-ones-iii/)

<p>Given a binary array <code>nums</code> and an integer <code>k</code>, return <em>the maximum number of consecutive </em><code>1</code><em>'s in the array if you can flip at most</em> <code>k</code> <code>0</code>'s.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2
<strong>Output:</strong> 6
<strong>Explanation:</strong> [1,1,1,0,0,<u><strong>1</strong>,1,1,1,1,<strong>1</strong></u>]
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], k = 3
<strong>Output:</strong> 10
<strong>Explanation:</strong> [0,0,<u>1,1,<strong>1</strong>,<strong>1</strong>,1,1,1,<strong>1</strong>,1,1</u>,0,0,0,1,1,1,1]
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>nums[i]</code> is either <code>0</code> or <code>1</code>.</li>
	<li><code>0 &lt;= k &lt;= nums.length</code></li>
</ul>


**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Bloomberg](https://leetcode.com/company/bloomberg), [Zillow](https://leetcode.com/company/zillow), [HBO](https://leetcode.com/company/hbo)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Binary Search](https://leetcode.com/tag/binary-search/), [Sliding Window](https://leetcode.com/tag/sliding-window/), [Prefix Sum](https://leetcode.com/tag/prefix-sum/)

**Similar Questions**:
* [Longest Substring with At Most K Distinct Characters (Medium)](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)
* [Longest Repeating Character Replacement (Medium)](https://leetcode.com/problems/longest-repeating-character-replacement/)
* [Max Consecutive Ones (Easy)](https://leetcode.com/problems/max-consecutive-ones/)
* [Max Consecutive Ones II (Medium)](https://leetcode.com/problems/max-consecutive-ones-ii/)

## Solution 1.

```python
class Solution:
    def longestOnes(self, nums: List[int], k: int) -> int:
        
        ## Slicing window O(n) use left and right point count max length of 1s with k zero
        # length = 0
        # count = 0
        # left,right = 0,0
        # while right<len(nums):
        #     if nums[right]== 0 and count == k:
        #         ## move the right pointer pass a '0'
        #         while nums[left] != 0:
        #             left += 1
        #         left += 1
        #         count-= 1
        #         # print('pass all zero, than new',left,right)
        #     elif nums[right]== 0 and count <k:
        #         right += 1
        #         count += 1
        #         if right-left > length:
        #             length = right-left
        #     else:
        #         right += 1
        #         if right-left > length:
        #             length = right - left
        # if right-left > length:
        #             length = right - left
        # return length
    
    
        ## Optimized
        length = 0
        count = 0
        left,right = 0,0
        while right<len(nums):
            if nums[right]== 0 and count == k:
                ## move the leftt pointer pass a '0'
                while nums[left] != 0:
                    left += 1
                left += 1
                count-= 1

            else:
                if nums[right]== 0:
                    right += 1
                    count += 1
                else:
                    right += 1
                    
                if right-left > length:
                    length = right - left
                   
        ## final check after while loop
        if right-left > length:
            length = right - left
            
        return length        
            
                
        
```