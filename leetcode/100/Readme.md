# [79. Word Search (Medium)](https://leetcode.com/problems/word-search/)

<p>Given an <code>m x n</code> grid of characters <code>board</code> and a string <code>word</code>, return <code>true</code> <em>if</em> <code>word</code> <em>exists in the grid</em>.</p>

<p>The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/04/word2.jpg" style="width: 322px; height: 242px;">
<pre><strong>Input:</strong> board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
<strong>Output:</strong> true
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg" style="width: 322px; height: 242px;">
<pre><strong>Input:</strong> board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
<strong>Output:</strong> true
</pre>

<p><strong>Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/15/word3.jpg" style="width: 322px; height: 242px;">
<pre><strong>Input:</strong> board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == board.length</code></li>
	<li><code>n = board[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 6</code></li>
	<li><code>1 &lt;= word.length &lt;= 15</code></li>
	<li><code>board</code> and <code>word</code> consists of only lowercase and uppercase English letters.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Could you use search pruning to make your solution faster with a larger <code>board</code>?</p>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Snapchat](https://leetcode.com/company/snapchat), [Bloomberg](https://leetcode.com/company/bloomberg), [Twitter](https://leetcode.com/company/twitter), [Facebook](https://leetcode.com/company/facebook), [Apple](https://leetcode.com/company/apple), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [Cisco](https://leetcode.com/company/cisco), [Google](https://leetcode.com/company/google), [Adobe](https://leetcode.com/company/adobe), [VMware](https://leetcode.com/company/vmware), [Cruise Automation](https://leetcode.com/company/cruise-automation), [ByteDance](https://leetcode.com/company/bytedance), [Bolt](https://leetcode.com/company/bolt)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Backtracking](https://leetcode.com/tag/backtracking/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:
* [Word Search II (Hard)](https://leetcode.com/problems/word-search-ii/)

## Solution 1.

``py
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        
        ## DFS
        add_ons = [(0,-1),(0,1),(-1,0),(1,0)]
        def helper(word, next_char_idx, cur_pos, visited):
            # print(next_char_idx, cur_pos, visited)
            if next_char_idx == len(word):
                return True
            result = False
            for (add_row, add_col) in add_ons:
                next_row, next_col = cur_pos[0] + add_row,cur_pos[1] + add_col
                if 0<= next_row < len(board) and 0 <= next_col < len(board[0]) and (next_row,next_col) not in visited and board[next_row][next_col] == word[next_char_idx]:
                    visited.add((next_row,next_col))
                    result = result or helper(word,next_char_idx+1, (next_row,next_col),visited)
                    visited.remove((next_row,next_col))
            return result
        
        ## find begin char
        begin_pos = []
        for i in range(0,len(board)):
            for j in range(0,len(board[0])):
                if board[i][j] == word[0]:
                    begin_pos.append((i,j))
            
        result = False
        for begin in begin_pos:
            if helper(word,1,begin,set({begin})):
                return True
        return False
```