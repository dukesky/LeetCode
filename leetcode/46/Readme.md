
# [16. 3Sum Closest (Medium)](https://leetcode.com/problems/3sum-closest/)

<p>Given an array <code>nums</code> of <em>n</em> integers and an integer <code>target</code>, find three integers in <code>nums</code>&nbsp;such that the sum is closest to&nbsp;<code>target</code>. Return the sum of the three integers. You may assume that each input would have exactly one solution.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [-1,2,1,-4], target = 1
<strong>Output:</strong> 2
<strong>Explanation:</strong> The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>3 &lt;= nums.length &lt;= 10^3</code></li>
	<li><code>-10^3&nbsp;&lt;= nums[i]&nbsp;&lt;= 10^3</code></li>
	<li><code>-10^4&nbsp;&lt;= target&nbsp;&lt;= 10^4</code></li>
</ul>


**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Apple](https://leetcode.com/company/apple), [Adobe](https://leetcode.com/company/adobe), [Uber](https://leetcode.com/company/uber), [Google](https://leetcode.com/company/google), [Capital One](https://leetcode.com/company/capital-one)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Two Pointers](https://leetcode.com/tag/two-pointers/), [Sorting](https://leetcode.com/tag/sorting/)

**Similar Questions**:
* [3Sum (Medium)](https://leetcode.com/problems/3sum/)
* [3Sum Smaller (Medium)](https://leetcode.com/problems/3sum-smaller/)

## Solution 1.

```py

class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        
        ## solution1: three loop to find a combination(a1,a2,a3), compare (a1+a2+a3) with target and get the closest one  T:O(N^3)  S:O(1)
#         nums = sorted(nums)
#         res = float('inf')
#         for i in range(0,len(nums)-2):
#             if nums[i] > (target+2)//3:
#                 return min(res,nums[i]+nums[i+1]+nums[i+2])
#             for j in range(i+1,len(nums)):
#                 for p in range(j+1,len(nums)):
#                     if abs(nums[i] + nums[j] + nums[p] - target) < abs(res-target):
#                         res = nums[i] + nums[j] + nums[p]
                        
#         return res
    
```

## solution 2.
```py
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:

        ## solution2: use i,j to choose begin, end number, use binary search to find the middle number  T:O(N^2logN)
        nums = sorted(nums)
        res = float('inf')
        for i in range(0,len(nums)-2):
            if nums[i] > (target+2)//3:
                return min(res,nums[i]+nums[i+1]+nums[i+2])
            for j in range(i+2,len(nums)):
                new_target = target - nums[i] - nums[j]
                # select closest number to target between i+1 and j-1
                left = i+1
                right = j-1

                while left<right-1:
                    mid = (left+right)//2
                    if nums[mid] >new_target:
                        right = mid
                    else:
                        left = mid
                mid_num = left if abs(nums[left]-new_target)<abs(nums[right]-new_target) else right
                if abs(nums[i]+nums[j]+nums[mid_num]-target) <abs(res-target):
                    res = nums[i]+nums[j]+nums[mid_num]
                        
        return res        


```