# [677. Map Sum Pairs (Medium)](https://leetcode.com/problems/map-sum-pairs/)

<p>Implement the <code>MapSum</code> class:</p>

<ul>
	<li><code>MapSum()</code> Initializes the&nbsp;<code>MapSum</code> object.</li>
	<li><code>void insert(String key, int val)</code> Inserts the <code>key-val</code> pair into the map. If the <code>key</code> already existed, the original <code>key-value</code> pair will be overridden to the new one.</li>
	<li><code>int sum(string prefix)</code> Returns&nbsp;the sum of all the pairs' value whose <code>key</code> starts with the <code>prefix</code>.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input</strong>
["MapSum", "insert", "sum", "insert", "sum"]
[[], ["apple", 3], ["ap"], ["app", 2], ["ap"]]
<strong>Output</strong>
[null, null, 3, null, 5]

<strong>Explanation</strong>
MapSum mapSum = new MapSum();
mapSum.insert("apple", 3);  
mapSum.sum("ap");           // return 3 (<u>ap</u>ple = 3)
mapSum.insert("app", 2);    
mapSum.sum("ap");           // return 5 (<u>ap</u>ple + <u>ap</u>p = 3 + 2 = 5)
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= key.length, prefix.length &lt;= 50</code></li>
	<li><code>key</code> and <code>prefix</code> consist of only lowercase English letters.</li>
	<li><code>1 &lt;= val &lt;= 1000</code></li>
	<li>At most <code>50</code> calls will be made to <code>insert</code> and <code>sum</code>.</li>
</ul>


**Companies**:  
[Akuna Capital](https://leetcode.com/company/akuna-capital)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Design](https://leetcode.com/tag/design/), [Trie](https://leetcode.com/tag/trie/)

## Solution 1.

```py
## solutoin1 use 2 directionary store key-val and prefix-val, update each time
# O(mn) m- num-words  n- num-letters-each-word
class MapSum:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.prefix = dict()
        self.num = dict()

    def insert(self, key: str, val: int) -> None:
        pre_key = ''
        ## check if key already exist
        if key in self.num:
            change_val = val - self.num[key]
            self.num[key] = val
        else:
            change_val = val
            self.num[key] = val
        for char in key:
            pre_key += char
            if pre_key not in self.prefix:
                self.prefix[pre_key] = change_val
            else:
                self.prefix[pre_key] += change_val
        print(self.prefix)
        

    def sum(self, prefix: str) -> int:
        if prefix not in self.prefix:
            return 0
        return self.prefix[prefix]
    
    
## solution2 user trie and dictionary to store key-value


# Your MapSum object will be instantiated and called as such:
# obj = MapSum()
# obj.insert(key,val)
# param_2 = obj.sum(prefix)

```