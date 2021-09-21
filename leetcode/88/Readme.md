# [774. Minimize Max Distance to Gas Station (Hard)](https://leetcode.com/problems/minimize-max-distance-to-gas-station/)

<p>You are given an integer array <code>stations</code> that represents the positions of the gas stations on the <strong>x-axis</strong>. You are also given an integer <code>k</code>.</p>

<p>You should add <code>k</code> new gas stations. You can add the stations anywhere on the <strong>x-axis</strong>, and not necessarily on an integer position.</p>

<p>Let <code>penalty()</code> be the maximum distance between <strong>adjacent</strong> gas stations after adding the <code>k</code> new stations.</p>

<p>Return <em>the smallest possible value of</em> <code>penalty()</code>. Answers within <code>10<sup>-6</sup></code> of the actual answer will be accepted.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> stations = [1,2,3,4,5,6,7,8,9,10], k = 9
<strong>Output:</strong> 0.50000
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> stations = [23,24,36,39,46,56,57,65,84,98], k = 1
<strong>Output:</strong> 14.00000
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>10 &lt;= stations.length &lt;= 2000</code></li>
	<li><code>0 &lt;= stations[i] &lt;= 10<sup>8</sup></code></li>
	<li><code>stations</code> is sorted in a <strong>strictly increasing</strong> order.</li>
	<li><code>1 &lt;= k &lt;= 10<sup>6</sup></code></li>
</ul>


**Companies**:  
[Google](https://leetcode.com/company/google)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Binary Search](https://leetcode.com/tag/binary-search/)

**Similar Questions**:
* [Koko Eating Bananas (Medium)](https://leetcode.com/problems/koko-eating-bananas/)

## Solution 1.

```py
class Solution:
    def minmaxGasDist(self, stations: List[int], k: int) -> float:
        
        ## count distance betweeen each gas stations
        ## use a heap to store all distance, with number of add gas between these distance
        ## O(NlogN + klongN)
        diff = []
        for i in range(0,len(stations)-1):
            diff.append([-1*(stations[i+1]-stations[i]),0])
        heapq.heapify(diff)
        while k>0:
            longest,sep = heapq.heappop(diff)
            longest = round((longest*(sep+1))/(sep+2),6)
            heapq.heappush(diff,[longest,sep+1])
            k-=1
        
        return -1*heapq.heappop(diff)[0]
    
```

## Solution 2.

```py
class Solution(object):
    def minmaxGasDist(self, stations, K):
        def possible(D):
            return sum(int((stations[i+1] - stations[i]) / D)
                       for i in xrange(len(stations) - 1)) <= K

        lo, hi = 0, 10**8
        while hi - lo > 1e-6:
            mi = (lo + hi) / 2.0
            if possible(mi):
                hi = mi
            else:
                lo = mi
        return lo

```