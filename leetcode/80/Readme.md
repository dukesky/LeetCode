# [224. Basic Calculator (Hard)](https://leetcode.com/problems/basic-calculator/)

<p>Given a string <code>s</code> representing a valid expression, implement a basic calculator to evaluate it, and return <em>the result of the evaluation</em>.</p>

<p><strong>Note:</strong> You are <strong>not</strong> allowed to use any built-in function which evaluates strings as mathematical expressions, such as <code>eval()</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "1 + 1"
<strong>Output:</strong> 2
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = " 2-1 + 2 "
<strong>Output:</strong> 3
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> s = "(1+(4+5+2)-3)+(6+8)"
<strong>Output:</strong> 23
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 3&nbsp;* 10<sup>5</sup></code></li>
	<li><code>s</code> consists of digits, <code>'+'</code>, <code>'-'</code>, <code>'('</code>, <code>')'</code>, and <code>' '</code>.</li>
	<li><code>s</code> represents a valid expression.</li>
	<li><code>'+'</code> is not used as a unary operation.</li>
	<li><code>'-'</code> could be used as a unary operation but it has to be inside parentheses.</li>
	<li>There will be no two consecutive operators in the input.</li>
	<li>Every number and running calculation will fit in a signed 32-bit integer.</li>
</ul>


**Companies**:  
[Microsoft](https://leetcode.com/company/microsoft), [Facebook](https://leetcode.com/company/facebook), [Karat](https://leetcode.com/company/karat), [Amazon](https://leetcode.com/company/amazon), [Roblox](https://leetcode.com/company/roblox), [Google](https://leetcode.com/company/google), [eBay](https://leetcode.com/company/ebay), [Apple](https://leetcode.com/company/apple), [ByteDance](https://leetcode.com/company/bytedance), [Bolt](https://leetcode.com/company/bolt), [Indeed](https://leetcode.com/company/indeed), [Yahoo](https://leetcode.com/company/yahoo), [Wish](https://leetcode.com/company/wish), [Shopee](https://leetcode.com/company/shopee)

**Related Topics**:  
[Math](https://leetcode.com/tag/math/), [String](https://leetcode.com/tag/string/), [Stack](https://leetcode.com/tag/stack/), [Recursion](https://leetcode.com/tag/recursion/)

**Similar Questions**:
* [Evaluate Reverse Polish Notation (Medium)](https://leetcode.com/problems/evaluate-reverse-polish-notation/)
* [Basic Calculator II (Medium)](https://leetcode.com/problems/basic-calculator-ii/)
* [Different Ways to Add Parentheses (Medium)](https://leetcode.com/problems/different-ways-to-add-parentheses/)
* [Expression Add Operators (Hard)](https://leetcode.com/problems/expression-add-operators/)
* [Basic Calculator III (Hard)](https://leetcode.com/problems/basic-calculator-iii/)

## Solution 1. Count sign of all number and get sum

```py
class Solution:
    def calculate(self, s: str) -> int:
        
        ## remove space
        ## count pos/neg sign each number in a list
        ## get sum
        ## exp (1+(4+5+2)-3)+(6+8) ==> [2,5,4,1,-3,6,8] / [1,4,5,2,-3,6,8] ==> [[1,[4,5,2],-3],[6,8]]
        ## exp -(1)+(2-3)-(4+5)-(6)+(7+8) ==> [1,2,-3,-4,-5,-6,7,8]
        ## exp -1+4+(2+3)   4-1-(-2+3) ==> [-1+4+2+3]  [4-1-2-3]
        ## exp -1+4+(2+3-(4+5+(6-(7-8+(9-19-(25+1)))))) ==> [-1+4+2+3-4-5-6+7-8+9-19-25-1]
        s = ''.join(s.split(' '))
        print(s)
        nums = []
        digits = set(['0','1','2','3','4','5','6','7','8','9'])
        signs = set(['+','-'])
        # use a stack to store all pareteness sign
        pare_sign = [1]
        sign = 1
        num = ''
        for i,char in enumerate(s):
            if char in digits:
                num += char
            else: 
                if num:
                    nums.append(sign*pare_sign[-1]*int(num))
                    num = ''
                    
                if  char in signs and s[i+1] in digits:
                    if char == '+':
                        sign = 1
                    else:
                        sign = -1     
                elif char in ['(',')']:
                    sign = 1
                    if char == '(':
                        if i>0 and s[i-1]=='-':
                            pare_sign.append(pare_sign[-1]*(-1))
                        else:
                            pare_sign.append(pare_sign[-1])
                    if char == ')':
                        pare_sign.pop()
                            
        if num:
            nums.append(sign*int(num))
                    
        return sum(nums)
```

## Solution 2. Use Stack to store and get sum by combute order

```py
class Solution:
    def calculate(self, s: str) -> int:

        stack = []
        operand = 0
        res = 0 # For the on-going result
        sign = 1 # 1 means positive, -1 means negative  

        for ch in s:
            if ch.isdigit():

                # Forming operand, since it could be more than one digit
                operand = (operand * 10) + int(ch)

            elif ch == '+':

                # Evaluate the expression to the left,
                # with result, sign, operand
                res += sign * operand

                # Save the recently encountered '+' sign
                sign = 1

                # Reset operand
                operand = 0

            elif ch == '-':

                res += sign * operand
                sign = -1
                operand = 0

            elif ch == '(':

                # Push the result and sign on to the stack, for later
                # We push the result first, then sign
                stack.append(res)
                stack.append(sign)

                # Reset operand and result, as if new evaluation begins for the new sub-expression
                sign = 1
                res = 0

            elif ch == ')':

                # Evaluate the expression to the left
                # with result, sign and operand
                res += sign * operand

                # ')' marks end of expression within a set of parenthesis
                # Its result is multiplied with sign on top of stack
                # as stack.pop() is the sign before the parenthesis
                res *= stack.pop() # stack pop 1, sign
```