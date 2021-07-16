# [18. 4Sum (Medium)](https://leetcode.com/problems/4sum/)

<p>Given an array <code>nums</code> of <code>n</code> integers, return <em>an array of all the <strong>unique</strong> quadruplets</em> <code>[nums[a], nums[b], nums[c], nums[d]]</code> such that:</p>

<ul>
	<li><code>0 &lt;= a, b, c, d&nbsp;&lt; n</code></li>
	<li><code>a</code>, <code>b</code>, <code>c</code>, and <code>d</code> are <strong>distinct</strong>.</li>
	<li><code>nums[a] + nums[b] + nums[c] + nums[d] == target</code></li>
</ul>

<p>You may return the answer in <strong>any order</strong>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,0,-1,0,-2,2], target = 0
<strong>Output:</strong> [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [2,2,2,2,2], target = 8
<strong>Output:</strong> [[2,2,2,2]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 200</code></li>
	<li><code>-10<sup>9</sup> &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= target &lt;= 10<sup>9</sup></code></li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Bloomberg](https://leetcode.com/company/bloomberg), [Adobe](https://leetcode.com/company/adobe), [Yahoo](https://leetcode.com/company/yahoo), [Snapchat](https://leetcode.com/company/snapchat)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Two Pointers](https://leetcode.com/tag/two-pointers/), [Sorting](https://leetcode.com/tag/sorting/)

**Similar Questions**:
* [Two Sum (Easy)](https://leetcode.com/problems/two-sum/)
* [3Sum (Medium)](https://leetcode.com/problems/3sum/)
* [4Sum II (Medium)](https://leetcode.com/problems/4sum-ii/)

## Solution 1.

```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        
        ## 4 sum could be iterate two loop i,j, and a two sum for target_new = target - nums[i] - nums[j]    O(n^3) n -- number of elements
        nums = sorted(nums)
        result = []
        exist_pair = set()
        for i in range(0,len(nums)-3):
            for j in range(i+1,len(nums)-2):
                if nums[i] + nums[j] > target //2:
                    break
                if (nums[i],nums[j]) in exist_pair:
                    continue
                exist_pair.add((nums[i],nums[j]))
                res = target - nums[i] - nums[j]
                num_dict = collections.defaultdict(lambda:0)
                for num in nums[j+1:]:
                    num_dict[num] += 1
                    
                for num in nums[j+1:]:
                    if num in num_dict:
                        num_dict[num] -= 1
                        if res - num in num_dict and res - num != num:
                            result.append([nums[i],nums[j],num, res -num])
                            del num_dict[num]
                            del num_dict[res - num]
                        elif res - num in num_dict and res - num == num and num_dict[num] != 0:
                            result.append([nums[i],nums[j],num, res -num])
                            del num_dict[num]
        return result


```
## Solution 2.

``` python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        ## 4 sum could be a combination of two sum:
        ## two loop to check 2_sum and target - 2_sum exist
        ## 
        nums = sorted(nums)
        two_sum_target_dict = dict()
        two_sum_target_set = set()
        for i in range(0,len(nums)):
            for j in range(i+1,len(nums)):
                if nums[i] + nums[j] not in two_sum_target_set:
                    two_sum_target_set.add(nums[i]+nums[j])
                    two_sum_target_dict[nums[i]+nums[j]] = set([(nums[i],nums[j])])
                else:
                    if (nums[i],nums[j]) not in two_sum_target_dict[nums[i]+nums[j]]:
                        two_sum_target_dict[nums[i]+nums[j]].add((nums[i],nums[j]))
        
        result = []
        sum_list = list(two_sum_target_set)
        for sum_1 in sum_list:
            if sum_1 <= target //2:
                if target - sum_1 in two_sum_target_set:
                    if target - sum_1 != sum_1:
                        for tup_1 in two_sum_target_dict[sum_1]:
                            for tup_2 in two_sum_target_dict[target-sum_1]:
                                result.appned(list(tup_1)+list(tup_2))
                    else:
                        if len(two_sum_target_dict[sum_1])>1:
                            same_sum_list = list(two_sum_target_dict[sum_1])
                            for i in range(0,len(same_sum_list)):
                                for j in range(i+1,len(same_sum_list)):
                                    result.append(list(same_sum_list[i])+list(same_sum_list[j]))
                            
            else:
                break
                
        return result
                    
                    
        
        

```