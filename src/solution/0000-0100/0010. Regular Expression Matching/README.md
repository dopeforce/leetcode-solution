# [**10. Regular Exression Matching**](https://leetcode.com/problems/regular-expression-matching)

<p>Given an input string <code>s</code>&nbsp;and a pattern <code>p</code>, implement regular expression matching with support for <code>&#39;.&#39;</code> and <code>&#39;*&#39;</code> where:</p>
<ul>
	<li><code>&#39;.&#39;</code> Matches any single character.​​​​</li>
	<li><code>&#39;*&#39;</code> Matches zero or more of the preceding element.</li>
</ul>
<p>The matching should cover the <strong>entire</strong> input string (not partial).</p>
<h3><strong class="example">Example 1:</strong></h3>
<pre>
<strong>Input:</strong> s = &quot;aa&quot;, p = &quot;a&quot;
<strong>Output:</strong> false
<strong>Explanation:</strong> &quot;a&quot; does not match the entire string &quot;aa&quot;.
</pre>
<h3><strong class="example">Example 2:</strong></h3>
<pre>
<strong>Input:</strong> s = &quot;aa&quot;, p = &quot;a*&quot;
<strong>Output:</strong> true
<strong>Explanation:</strong> &#39;*&#39; means zero or more of the preceding element, &#39;a&#39;. Therefore, by repeating &#39;a&#39; once, it becomes &quot;aa&quot;.
</pre>
<h3><strong class="example">Example 3:</strong></h3>
<pre>
<strong>Input:</strong> s = &quot;ab&quot;, p = &quot;.*&quot;
<strong>Output:</strong> true
<strong>Explanation:</strong> &quot;.*&quot; means &quot;zero or more (*) of any character (.)&quot;.
</pre>
<h3><strong>Constraints:</strong></h3>
<ul>
	<li><code>1 &lt;= s.length&nbsp;&lt;= 20</code></li>
	<li><code>1 &lt;= p.length&nbsp;&lt;= 20</code></li>
	<li><code>s</code> contains only lowercase English letters.</li>
	<li><code>p</code> contains only lowercase English letters, <code>&#39;.&#39;</code>, and&nbsp;<code>&#39;*&#39;</code>.</li>
	<li>It is guaranteed for each appearance of the character <code>&#39;*&#39;</code>, there will be a previous valid character to match.</li>
</ul>

<p>&nbsp;</p>

# **Solutions**

### **Python3**
```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        @cache
        def dfs(i, j):
            if j >= n:
                return i == m
            if j + 1 < n and p[j + 1] == '*':
                return dfs(i, j + 2) or (
                    i < m and (s[i] == p[j] or p[j] == '.') and dfs(i + 1, j)
                )
            return i < m and (s[i] == p[j] or p[j] == '.') and dfs(i + 1, j + 1)

        m, n = len(s), len(p)
        return dfs(0, 0)
```

### **Java**
```java
class Solution {
    private Boolean[][] f;
    private String s;
    private String p;
    private int m;
    private int n;

    public boolean isMatch(String s, String p) {
        m = s.length();
        n = p.length();
        f = new Boolean[m + 1][n + 1];
        this.s = s;
        this.p = p;
        return dfs(0, 0);
    }

    private boolean dfs(int i, int j) {
        if (j >= n) {
            return i == m;
        }
        if (f[i][j] != null) {
            return f[i][j];
        }
        boolean res = false;
        if (j + 1 < n && p.charAt(j + 1) == '*') {
            res = dfs(i, j + 2)
                || (i < m && (s.charAt(i) == p.charAt(j) || p.charAt(j) == '.') && dfs(i + 1, j));
        } else {
            res = i < m && (s.charAt(i) == p.charAt(j) || p.charAt(j) == '.') && dfs(i + 1, j + 1);
        }
        return f[i][j] = res;
    }
}
```

### **C++**
```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.size(), n = p.size();
        int f[m + 1][n + 1];
        memset(f, 0, sizeof f);
        function<bool(int, int)> dfs = [&](int i, int j) -> bool {
            if (j >= n) {
                return i == m;
            }
            if (f[i][j]) {
                return f[i][j] == 1;
            }
            int res = -1;
            if (j + 1 < n && p[j + 1] == '*') {
                if (dfs(i, j + 2) or (i < m and (s[i] == p[j] or p[j] == '.') and dfs(i + 1, j))) {
                    res = 1;
                }
            } else if (i < m and (s[i] == p[j] or p[j] == '.') and dfs(i + 1, j + 1)) {
                res = 1;
            }
            f[i][j] = res;
            return res == 1;
        };
        return dfs(0, 0);
    }
};
```

### **Go**
```go
func isMatch(s string, p string) bool {
	m, n := len(s), len(p)
	f := make([][]int, m+1)
	for i := range f {
		f[i] = make([]int, n+1)
	}
	var dfs func(i, j int) bool
	dfs = func(i, j int) bool {
		if j >= n {
			return i == m
		}
		if f[i][j] != 0 {
			return f[i][j] == 1
		}
		res := -1
		if j+1 < n && p[j+1] == '*' {
			if dfs(i, j+2) || (i < m && (s[i] == p[j] || p[j] == '.') && dfs(i+1, j)) {
				res = 1
			}
		} else if i < m && (s[i] == p[j] || p[j] == '.') && dfs(i+1, j+1) {
			res = 1
		}
		f[i][j] = res
		return res == 1
	}
	return dfs(0, 0)
}
```

### **Rust**
```rust
impl Solution {
    pub fn is_match(s: String, p: String) -> bool {
        let (m, n) = (s.len(), p.len());
        let mut f = vec![vec![0; n + 1]; m + 1];

        fn dfs(
            s: &Vec<char>,
            p: &Vec<char>,
            f: &mut Vec<Vec<i32>>,
            i: usize,
            j: usize,
            m: usize,
            n: usize,
        ) -> bool {
            if j >= n {
                return i == m;
            }
            if f[i][j] != 0 {
                return f[i][j] == 1;
            }
            let mut res = -1;
            if j + 1 < n && p[j + 1] == '*' {
                if dfs(s, p, f, i, j + 2, m, n)
                    || (i < m && (s[i] == p[j] || p[j] == '.') && dfs(s, p, f, i + 1, j, m, n))
                {
                    res = 1;
                }
            } else if i < m && (s[i] == p[j] || p[j] == '.') && dfs(s, p, f, i + 1, j + 1, m, n) {
                res = 1;
            }
            f[i][j] = res;
            res == 1
        }

        dfs(
            &s.chars().collect(),
            &p.chars().collect(),
            &mut f,
            0,
            0,
            m,
            n,
        )
    }
}
```

### **JavaScript**
```js
/**
 * @param {string} s
 * @param {string} p
 * @return {boolean}
 */
var isMatch = function (s, p) {
    const m = s.length;
    const n = p.length;
    const f = Array.from({ length: m + 1 }, () => Array(n + 1).fill(0));
    const dfs = (i, j) => {
        if (j >= n) {
            return i === m;
        }
        if (f[i][j]) {
            return f[i][j] === 1;
        }
        let res = -1;
        if (j + 1 < n && p[j + 1] === '*') {
            if (dfs(i, j + 2) || (i < m && (s[i] === p[j] || p[j] === '.') && dfs(i + 1, j))) {
                res = 1;
            }
        } else if (i < m && (s[i] === p[j] || p[j] === '.') && dfs(i + 1, j + 1)) {
            res = 1;
        }
        f[i][j] = res;
        return res === 1;
    };
    return dfs(0, 0);
};
```

### **C#**
```cs
public class Solution {
    private string s;
    private string p;
    private int m;
    private int n;
    private int[,] f;

    public bool IsMatch(string s, string p) {
        m = s.Length;
        n = p.Length;
        f = new int[m + 1, n + 1];
        this.s = s;
        this.p = p;
        return dfs(0, 0);
    }

    private bool dfs(int i, int j) {
        if (j >= n) {
            return i == m;
        }
        if (f[i, j] != 0) {
            return f[i, j] == 1;
        }
        int res = -1;
        if (j + 1 < n && p[j + 1] == '*') {
            if (dfs(i, j + 2) || (i < m && (s[i] == p[j] || p[j] == '.') && dfs(i + 1, j))) {
                res = 1;
            }
        } else if (i < m && (s[i] == p[j] || p[j] == '.') && dfs(i + 1, j + 1)) {
            res = 1;
        }
        f[i, j] = res;
        return res == 1;
    }
}
```