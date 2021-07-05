# [535. Encode and Decode TinyURL (Medium)](https://leetcode.com/problems/encode-and-decode-tinyurl/)

<blockquote>Note: This is a companion problem to the <a href="https://leetcode.com/discuss/interview-question/system-design/" target="_blank">System Design</a> problem: <a href="https://leetcode.com/discuss/interview-question/124658/Design-a-URL-Shortener-(-TinyURL-)-System/" target="_blank">Design TinyURL</a>.</blockquote>

<p>TinyURL is a URL shortening service where you enter a URL such as <code>https://leetcode.com/problems/design-tinyurl</code> and it returns a short URL such as <code>http://tinyurl.com/4e9iAk</code>. Design a class to encode a URL and decode a tiny URL.</p>

<p>There is no restriction on how your encode/decode algorithm should work. You just need to ensure that a URL can be encoded to a tiny URL and the tiny URL can be decoded to the original URL.</p>

<p>Implement the <code>Solution</code> class:</p>

<ul>
	<li><code>Solution()</code> Initializes the object of the system.</li>
	<li><code>String encode(String longUrl)</code> Returns a tiny URL for the given <code>longUrl</code>.</li>
	<li><code>String decode(String shortUrl)</code> Returns the original long URL for the given <code>shortUrl</code>. It is guaranteed that the given <code>shortUrl</code> was encoded by the same object.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> url = "https://leetcode.com/problems/design-tinyurl"
<strong>Output:</strong> "https://leetcode.com/problems/design-tinyurl"

<strong>Explanation:</strong>
Solution obj = new Solution();
string tiny = obj.encode(url); // returns the encoded tiny url.
string ans = obj.decode(tiny); // returns the original url after deconding it.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= url.length &lt;= 10<sup>4</sup></code></li>
	<li><code>url</code> is guranteed to be a valid URL.</li>
</ul>


**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Design](https://leetcode.com/tag/design/), [Hash Function](https://leetcode.com/tag/hash-function/)

## Solution 1.

```python
class Codec:

    ## Solution1 Count encoding, maintain a count i, each number appears,add i+1, save original url to position i
    
    def __init__(self):
        self.i = 0
        self.origin_url = []
        
    def encode(self, longUrl: str) -> str:
        """Encodes a URL to a shortened URL.
        """
        pre_url = 'https://tinyrul.com/'
        self.origin_url.append(longUrl)
        url = pre_url + str(self.i)
        self.i += 1
        return url
        

    def decode(self, shortUrl: str) -> str:
        """Decodes a shortened URL to its original URL.
        """
        count = int(shortUrl.split('/')[-1])
        return self.origin_url[count]

```

## Solution 2.

```python

    ## Solution2 Count encoding, transter count to a 62 scale number (0-9,a-z,A-Z), map each number to a original url
    
    def __init__(self):
        self.i = 0
        self.origin_url = dict()
        self.chars = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
    
    def encode(self, longUrl: str) -> str:
        """Encodes a URL to a shortened URL.
        """
        pre_url = 'https://tinyrul.com/'
        c = self.i
        sb = []
        while c>0:
            sb.append(self.chars[c%62])
            c /= 62
        sb = ''.join(sb)
        url = pre_url + sb
        self.origin_url[sb]=longUrl
        self.i += 1
        return url
        

    def decode(self, shortUrl: str) -> str:
        """Decodes a shortened URL to its original URL.
        """
        count = shortUrl.split('/')[-1]
        return self.origin_url[count]
        

```

## Solution 3.

```python
class Codec:

    ## Solution3 use hash function to encode string into a hash number and map the original url
    
    def __init__(self):

        self.origin_url = dict()

    
    def encode(self, longUrl: str) -> str:
        """Encodes a URL to a shortened URL.
        """
        pre_url = 'https://tinyrul.com/'
        hash_code = hash(longUrl)
        self.origin_url[str(hash_code)]=longUrl

        return pre_url + str(hash_code)
        

    def decode(self, shortUrl: str) -> str:
        """Decodes a shortened URL to its original URL.
        """
        count = shortUrl.split('/')[-1]
        return self.origin_url[count]
    


```