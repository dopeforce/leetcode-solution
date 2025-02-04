# [**201. Bitwise AND of Numbers Range**](https://leetcode.com/problems/bitwise-and-of-numbers-range)

<p>Given two integers <code>left</code> and <code>right</code> that represent the range <code>[left, right]</code>, return <em>the bitwise AND of all numbers in this range, inclusive</em>.</p>
<h3><strong class="example">Example 1:</strong></h3>
<pre>
<strong>Input:</strong> left = 5, right = 7
<strong>Output:</strong> 4
</pre>
<h3><strong class="example">Example 2:</strong></h3>
<pre>
<strong>Input:</strong> left = 0, right = 0
<strong>Output:</strong> 0
</pre>
<h3><strong class="example">Example 3:</strong></h3>
<pre>
<strong>Input:</strong> left = 1, right = 2147483647
<strong>Output:</strong> 0
</pre>
<h3><strong>Constraints:</strong></h3>
<ul>
	<li><code>0 &lt;= left &lt;= right &lt;= 2<sup>31</sup> - 1</code></li>
</ul>
<p>&nbsp;</p>

# **Solutions**

### **Python3**
```python
class Solution:
    def rangeBitwiseAnd(self, left: int, right: int) -> int:
        while left < right:
            right &= right - 1
        return right
```

### **Java**
```java
class Solution {
    public int rangeBitwiseAnd(int left, int right) {
        while (left < right) {
            right &= (right - 1);
        }
        return right;
    }
}
```

### **C++**
```cpp
class Solution {
public:
    int rangeBitwiseAnd(int left, int right) {
        while (left < right) {
            right &= (right - 1);
        }
        return right;
    }
};
```

### **Go**
```go
func rangeBitwiseAnd(left int, right int) int {
	for left < right {
		right &= (right - 1)
	}
	return right
}
```

### **JavaScript**
```js
/**
 * @param {number} left
 * @param {number} right
 * @return {number}
 */
var rangeBitwiseAnd = function (left, right) {
    while (left < right) {
        right &= right - 1;
    }
    return right;
};
```

### **C#**
```cs
public class Solution {
    public int RangeBitwiseAnd(int left, int right) {
        while (left < right) {
            right &= (right - 1);
        }
        return right;
    }
}
```