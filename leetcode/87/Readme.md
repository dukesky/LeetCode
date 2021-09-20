# [1275. Find Winner on a Tic Tac Toe Game (Easy)](https://leetcode.com/problems/find-winner-on-a-tic-tac-toe-game/solution/)

<p>Tic-tac-toe is played&nbsp;by&nbsp;two players <em>A</em> and <em>B</em> on a&nbsp;<i>3</i>&nbsp;x&nbsp;<i>3</i>&nbsp;grid.</p>

<p>Here are the rules of Tic-Tac-Toe:</p>

<ul>
	<li>Players take turns placing characters into empty squares (" ").</li>
	<li>The first player <em>A</em> always places "X" characters, while the second player <em>B</em>&nbsp;always places "O" characters.</li>
	<li>"X" and "O" characters are always placed into empty squares, never on filled ones.</li>
	<li>The game ends when there are 3 of the same (non-empty) character filling any row, column, or diagonal.</li>
	<li>The game also ends if all squares are non-empty.</li>
	<li>No more moves can be played if the game is over.</li>
</ul>

<p>Given an array <code>moves</code> where each element&nbsp;is another array of size 2 corresponding to the row and column of the grid where they mark their respective character in the order in which <em>A</em> and <em>B</em> play.</p>

<p>Return the winner of the game if it exists (<em>A</em> or <em>B</em>), in case the game ends in a draw return "Draw", if there are still movements to play return "Pending".</p>

<p>You can assume that&nbsp;<code>moves</code> is&nbsp;<strong>valid</strong> (It follows the rules of Tic-Tac-Toe),&nbsp;the grid is initially empty and <em>A</em> will play <strong>first</strong>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> moves = [[0,0],[2,0],[1,1],[2,1],[2,2]]
<strong>Output:</strong> "A"
<strong>Explanation:</strong> "A" wins, he always plays first.
"X  "    "X  "    "X  "    "X  "    "<strong>X</strong>  "
"   " -&gt; "   " -&gt; " X " -&gt; " X " -&gt; " <strong>X</strong> "
"   "    "O  "    "O  "    "OO "    "OO<strong>X</strong>"
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> moves = [[0,0],[1,1],[0,1],[0,2],[1,0],[2,0]]
<strong>Output:</strong> "B"
<strong>Explanation:</strong> "B" wins.
"X  "    "X  "    "XX "    "XXO"    "XXO"    "XX<strong>O</strong>"
"   " -&gt; " O " -&gt; " O " -&gt; " O " -&gt; "XO " -&gt; "X<strong>O</strong> " 
"   "    "   "    "   "    "   "    "   "    "<strong>O</strong>  "
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> moves = [[0,0],[1,1],[2,0],[1,0],[1,2],[2,1],[0,1],[0,2],[2,2]]
<strong>Output:</strong> "Draw"
<strong>Explanation:</strong> The game ends in a draw since there are no moves to make.
"XXO"
"OOX"
"XOX"
</pre>

<p><strong>Example 4:</strong></p>

<pre><strong>Input:</strong> moves = [[0,0],[1,1]]
<strong>Output:</strong> "Pending"
<strong>Explanation:</strong> The game has not finished yet.
"X  "
" O "
"   "
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= moves.length &lt;= 9</code></li>
	<li><code>moves[i].length == 2</code></li>
	<li><code>0 &lt;= moves[i][j] &lt;= 2</code></li>
	<li>There are no repeated elements on <code>moves</code>.</li>
	<li><code>moves</code> follow the rules of tic tac toe.</li>
</ul>

**Companies**:  
[Microsoft](https://leetcode.com/company/microsoft), [Amazon](https://leetcode.com/company/amazon), [Facebook](https://leetcode.com/company/facebook), [Apple](https://leetcode.com/company/apple)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Matrix](https://leetcode.com/tag/matrix/), [Simulation](https://leetcode.com/tag/simulation/)

## Solution 1.

```py
class Solution:
    def tictactoe(self, moves: List[List[int]]) -> str:
        
        ## constance space and time
        ## for each move, check each row(3),col(3), dignal(2)
        def check_win(player_set):
            # check row
            for i in range(3):
                nums = 0
                for j in range(0,3):
                    if (i,j) in player_set:
                        nums += 1
                if nums == 3:
                    return True
                else:
                    nums = 0
            # check col
            for i in range(3):
                nums = 0
                for j in range(0,3):
                    if (j,i) in player_set:
                        nums += 1
                if nums == 3:
                    return True
                else:
                    nums = 0            
            # check dignal
            nums = 0
            for i in range(0,3):
                if (i,i) in player_set:
                    nums += 1
            if nums == 3:
                return True
            else:
                nums = 0               
            for i in range(0,3):
                if (2-i,i) in player_set:
                    nums += 1
            if nums == 3:
                return True
                    
            return False
            
            
        A = set()
        B = set()
        for i,move in enumerate(moves):
            if i%2==0:
                A.add(tuple(move))
                if check_win(A):
                    return 'A'
            else:
                B.add(tuple(move))
                if check_win(B):
                    return 'B'
        if i == 8:
            return 'Draw'
        else:
            return 'Pending'

```