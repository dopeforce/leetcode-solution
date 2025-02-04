# [**204. Count Primes**](https://leetcode.com/problems/count-primes)

<p>Given an integer <code>n</code>, return <em>the number of prime numbers that are strictly less than</em> <code>n</code>.</p>
<h3><strong class="example">Example 1:</strong></h3>
<pre>
<strong>Input:</strong> n = 10
<strong>Output:</strong> 4
<strong>Explanation:</strong> There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
</pre>
<h3><strong class="example">Example 2:</strong></h3>
<pre>
<strong>Input:</strong> n = 0
<strong>Output:</strong> 0
</pre>
<h3><strong class="example">Example 3:</strong></h3>
<pre>
<strong>Input:</strong> n = 1
<strong>Output:</strong> 0
</pre>
<h3><strong>Constraints:</strong></h3>
<ul>
	<li><code>0 &lt;= n &lt;= 5 * 10<sup>6</sup></code></li>
</ul>
<p>&nbsp;</p>

# **Solutions**

### **Python3**
```python
class Solution:
    def countPrimes(self, n: int) -> int:
        primes = [True] * n
        ans = 0
        for i in range(2, n):
            if primes[i]:
                ans += 1
                for j in range(i + i, n, i):
                    primes[j] = False
        return ans
```

### **Java**
```java
class Solution {
    public int countPrimes(int n) {
        boolean[] primes = new boolean[n];
        Arrays.fill(primes, true);
        int ans = 0;
        for (int i = 2; i < n; ++i) {
            if (primes[i]) {
                ++ans;
                for (int j = i + i; j < n; j += i) {
                    primes[j] = false;
                }
            }
        }
        return ans;
    }
}
```

### **C++**
```cpp
class Solution {
public:
    int countPrimes(int n) {
        vector<bool> primes(n, true);
        int ans = 0;
        for (int i = 2; i < n; ++i) {
            if (primes[i]) {
                ++ans;
                for (int j = i; j < n; j += i) primes[j] = false;
            }
        }
        return ans;
    }
};
```

### **Go**
```go
func countPrimes(n int) int {
	primes := make([]bool, n)
	for i := range primes {
		primes[i] = true
	}
	ans := 0
	for i := 2; i < n; i++ {
		if primes[i] {
			ans++
			for j := i + i; j < n; j += i {
				primes[j] = false
			}
		}
	}
	return ans
}
```

### **JavaScript**
```js
/**
 * @param {number} n
 * @return {number}
 */
var countPrimes = function (n) {
    let primes = new Array(n).fill(true);
    let ans = 0;
    for (let i = 2; i < n; ++i) {
        if (primes[i]) {
            ++ans;
            for (let j = i + i; j < n; j += i) {
                primes[j] = false;
            }
        }
    }
    return ans;
};
```

### **C#**
```cs
public class Solution {
    public int CountPrimes(int n) {
        var notPrimes = new bool[n];
        int ans = 0;
        for (int i = 2; i < n; ++i)
        {
            if (!notPrimes[i])
            {
                ++ans;
                for (int j = i + i; j < n; j += i)
                {
                    notPrimes[j] = true;
                }
            }
        }
        return ans;
    }
}
```