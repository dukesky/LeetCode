# [721. Accounts Merge (Medium)](https://leetcode.com/problems/accounts-merge/)

<p>Given a list of <code>accounts</code> where each element <code>accounts[i]</code> is a list of strings, where the first element <code>accounts[i][0]</code> is a name, and the rest of the elements are <strong>emails</strong> representing emails of the account.</p>

<p>Now, we would like to merge these accounts. Two accounts definitely belong to the same person if there is some common email to both accounts. Note that even if two accounts have the same name, they may belong to different people as people could have the same name. A person can have any number of accounts initially, but all of their accounts definitely have the same name.</p>

<p>After merging the accounts, return the accounts in the following format: the first element of each account is the name, and the rest of the elements are emails <strong>in sorted order</strong>. The accounts themselves can be returned in <strong>any order</strong>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> accounts = [["John","johnsmith@mail.com","john_newyork@mail.com"],["John","johnsmith@mail.com","john00@mail.com"],["Mary","mary@mail.com"],["John","johnnybravo@mail.com"]]
<strong>Output:</strong> [["John","john00@mail.com","john_newyork@mail.com","johnsmith@mail.com"],["Mary","mary@mail.com"],["John","johnnybravo@mail.com"]]
<strong>Explanation:</strong>
The first and second John's are the same person as they have the common email "johnsmith@mail.com".
The third John and Mary are different people as none of their email addresses are used by other accounts.
We could return these lists in any order, for example the answer [['Mary', 'mary@mail.com'], ['John', 'johnnybravo@mail.com'], 
['John', 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com']] would still be accepted.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> accounts = [["Gabe","Gabe0@m.co","Gabe3@m.co","Gabe1@m.co"],["Kevin","Kevin3@m.co","Kevin5@m.co","Kevin0@m.co"],["Ethan","Ethan5@m.co","Ethan4@m.co","Ethan0@m.co"],["Hanzo","Hanzo3@m.co","Hanzo1@m.co","Hanzo0@m.co"],["Fern","Fern5@m.co","Fern1@m.co","Fern0@m.co"]]
<strong>Output:</strong> [["Ethan","Ethan0@m.co","Ethan4@m.co","Ethan5@m.co"],["Gabe","Gabe0@m.co","Gabe1@m.co","Gabe3@m.co"],["Hanzo","Hanzo0@m.co","Hanzo1@m.co","Hanzo3@m.co"],["Kevin","Kevin0@m.co","Kevin3@m.co","Kevin5@m.co"],["Fern","Fern0@m.co","Fern1@m.co","Fern5@m.co"]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= accounts.length &lt;= 1000</code></li>
	<li><code>2 &lt;= accounts[i].length &lt;= 10</code></li>
	<li><code>1 &lt;= accounts[i][j] &lt;= 30</code></li>
	<li><code>accounts[i][0]</code> consists of English letters.</li>
	<li><code>accounts[i][j] (for j &gt; 0)</code> is a valid email.</li>
</ul>


**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [String](https://leetcode.com/tag/string/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Union Find](https://leetcode.com/tag/union-find/)

**Similar Questions**:
* [Redundant Connection (Medium)](https://leetcode.com/problems/redundant-connection/)
* [Sentence Similarity (Easy)](https://leetcode.com/problems/sentence-similarity/)
* [Sentence Similarity II (Medium)](https://leetcode.com/problems/sentence-similarity-ii/)

## Solution 1.

```py

from collections import defaultdict

class Solution:
    def accountsMerge(self, accounts: List[List[str]]) -> List[List[str]]:
        ## use set to store email address for each account
        ## it is a merge problem? union find?
        
        def unionmerge(set_list):
            set_dict = defaultdict(int)
            for i in range(len(set_list)):
                set_dict[i] = set_list[i]
            set_nums = [i for i in range(len(set_list))]
            union_pairs = []
            for i in range(len(set_list)-1):
                for j in range(i+1,len(set_list)):
                    for ele in set_list[i]:
                        if ele in set_list[j]:
                            union_pairs.append((i,j))
            for union_i,union_j in union_pairs:
                root_i,root_j = union_i,union_j
                ## find root if union_i or union_j not the root
                while set_nums[root_i] != root_i:
                    root_i = set_nums[root_i]
                while set_nums[root_j] != root_j:
                        root_j = set_nums[root_j]
                set_nums[max(root_i,root_j)] = min(root_i,root_j)
                
            res_dict = defaultdict(set)
            for i in range(len(set_nums)):
                root = i
                while root != set_nums[root]:
                    root = set_nums[root]
                set_nums[i] = root
                for ele in set_list[i]:
                    res_dict[root].add(ele)
            
            return [list(item) for key,item in res_dict.items()]
        
        account_dict = defaultdict(list)
        for account in accounts:
            name = account[0]
            emails = set(account[1:])
            account_dict[name].append(emails)
        for name in account_dict:
            account_dict[name] = unionmerge(account_dict[name])
        
        res = []
        for name in account_dict:
            # print(name,account_dict[name])
            res += [[name]+sorted(email_list) for email_list in account_dict[name]]
            
        return res
            
```