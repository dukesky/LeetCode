# [838. Push Dominoes (Medium)](https://leetcode.com/problems/push-dominoes/)

<p>There are <code>n</code> dominoes in a line, and we place each domino vertically upright. In the beginning, we simultaneously push some of the dominoes either to the left or to the right.</p>

<p>After each second, each domino that is falling to the left pushes the adjacent domino on the left. Similarly, the dominoes falling to the right push their adjacent dominoes standing on the right.</p>

<p>When a vertical domino has dominoes falling on it from both sides, it stays still due to the balance of the forces.</p>

<p>For the purposes of this question, we will consider that a falling domino expends no additional force to a falling or already fallen domino.</p>

<p>You are given a string <code>dominoes</code> representing the initial state where:</p>

<ul>
	<li><code>dominoes[i] = 'L'</code>, if the <code>i<sup>th</sup></code> domino has been pushed to the left,</li>
	<li><code>dominoes[i] = 'R'</code>, if the <code>i<sup>th</sup></code> domino has been pushed to the right, and</li>
	<li><code>dominoes[i] = '.'</code>, if the <code>i<sup>th</sup></code> domino has not been pushed.</li>
</ul>

<p>Return <em>a string representing the final state</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> dominoes = "RR.L"
<strong>Output:</strong> "RR.L"
<strong>Explanation:</strong> The first domino expends no additional force on the second domino.
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/05/18/domino.png" style="height: 196px; width: 512px;">
<pre><strong>Input:</strong> dominoes = ".L.R...LR..L.."
<strong>Output:</strong> "LL.RR.LLRRLL.."
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == dominoes.length</code></li>
	<li><code>1 &lt;= n &lt;= 10<sup>5</sup></code></li>
	<li><code>dominoes[i]</code> is either <code>'L'</code>, <code>'R'</code>, or <code>'.'</code>.</li>
</ul>


**Companies**:  
[Bloomberg](https://leetcode.com/company/bloomberg)

**Related Topics**:  
[Two Pointers](https://leetcode.com/tag/two-pointers/), [String](https://leetcode.com/tag/string/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

## Solution 1.

```py
class Solution:
    def pushDominoes(self, dominoes: str) -> str:
        
        ## O(n) 
        ## iterate from left, count distance of left push
        ## then iterate from right, compare left, right push to decide status
        left = []
        right_push = False
        dist = float('inf')
        for status in dominoes:
            dist += 1
            if status == 'R':
                right_push = True
                dist = 0
                left.append('R')
            elif status == 'L':
                right_push = False
                dist = 0
                left.append('L')
            else:
                if right_push:
                    left.append(dist)
                else:
                    left.append(float('inf'))

        left_push = False
        dist = float('inf')
        for i in range(len(dominoes)-1,-1,-1):
            dist += 1
            status = dominoes[i]
            if status == 'R':
                left_push = False
                dist = float('inf')
            elif status == 'L':
                left_push = True
                dist = 0
            else:
                if left_push:
                    if dist < left[i]:
                        left[i] = 'L'
                    elif dist > left[i]:
                        left[i] = 'R'
                    else:
                        left[i] = '.'
                elif left[i] != float('inf'):
                    left[i] = 'R'
                else:
                    left[i] = '.'
                    
        return ''.join(left)
            
                
        
```