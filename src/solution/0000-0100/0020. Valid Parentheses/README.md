# [**20. Valid Parentheses**](https://leetcode.com/problems/valid-parentheses)

<p>Given a string <code>s</code> containing just the characters <code>&#39;(&#39;</code>, <code>&#39;)&#39;</code>, <code>&#39;{&#39;</code>, <code>&#39;}&#39;</code>, <code>&#39;[&#39;</code> and <code>&#39;]&#39;</code>, determine if the input string is valid.</p>
<p>An input string is valid if:</p>
<ol>
	<li>Open brackets must be closed by the same type of brackets.</li>
	<li>Open brackets must be closed in the correct order.</li>
	<li>Every close bracket has a corresponding open bracket of the same type.</li>
</ol>
<h3><strong class="example">Example 1:</strong></h3>
<pre>
<strong>Input:</strong> <span class="example-io">s = &quot;()&quot;</span>
<strong>Output:</strong> <span class="example-io">true</span>
</pre>
<h3><strong class="example">Example 2:</strong></h3>
<pre>
<strong>Input:</strong> <span class="example-io">s = &quot;()[]{}&quot;</span>
<strong>Output:</strong> <span class="example-io">true</span>
</pre>
<h3><strong class="example">Example 3:</strong></h3>
<pre>
<strong>Input:</strong> <span class="example-io">s = &quot;(]&quot;</span>
<strong>Output:</strong> <span class="example-io">false</span>
</pre>
<h3><strong class="example">Example 4:</strong></h3>
<pre>
<strong>Input:</strong> <span class="example-io">s = &quot;([])&quot;</span>
<strong>Output:</strong> <span class="example-io">true</span>
</pre>
<h3><strong>Constraints:</strong></h3>
<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>4</sup></code></li>
	<li><code>s</code> consists of parentheses only <code>&#39;()[]{}&#39;</code>.</li>
</ul>
<p>&nbsp;</p>

# **Solutions**

### **Python3**
```python
class Solution:
    def isValid(self, s: str) -> bool:
        stk = []
        d = {'()', '[]', '{}'}
        for c in s:
            if c in '({[':
                stk.append(c)
            elif not stk or stk.pop() + c not in d:
                return False
        return not stk
```

### **Java**
```java
class Solution {
    public boolean isValid(String s) {
        Deque<Character> stk = new ArrayDeque<>();
        for (char c : s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[') {
                stk.push(c);
            } else if (stk.isEmpty() || !match(stk.pop(), c)) {
                return false;
            }
        }
        return stk.isEmpty();
    }

    private boolean match(char l, char r) {
        return (l == '(' && r == ')') || (l == '{' && r == '}') || (l == '[' && r == ']');
    }
}
```

### **C++**
```cpp
class Solution {
public:
    bool isValid(string s) {
        string stk;
        for (char c : s) {
            if (c == '(' || c == '{' || c == '[')
                stk.push_back(c);
            else if (stk.empty() || !match(stk.back(), c))
                return false;
            else
                stk.pop_back();
        }
        return stk.empty();
    }

    bool match(char l, char r) {
        return (l == '(' && r == ')') || (l == '[' && r == ']') || (l == '{' && r == '}');
    }
};
```

### **Go**
```go
func isValid(s string) bool {
	stk := []rune{}
	for _, c := range s {
		if c == '(' || c == '{' || c == '[' {
			stk = append(stk, c)
		} else if len(stk) == 0 || !match(stk[len(stk)-1], c) {
			return false
		} else {
			stk = stk[:len(stk)-1]
		}
	}
	return len(stk) == 0
}

func match(l, r rune) bool {
	return (l == '(' && r == ')') || (l == '[' && r == ']') || (l == '{' && r == '}')
}
```

### **TypeScript**
```ts
const map = new Map([
    ['(', ')'],
    ['[', ']'],
    ['{', '}'],
]);

function isValid(s: string): boolean {
    const stack = [];
    for (const c of s) {
        if (map.has(c)) {
            stack.push(map.get(c));
        } else if (stack.pop() !== c) {
            return false;
        }
    }
    return stack.length === 0;
}
```

### **Rust**
```rust
use std::collections::HashMap;

impl Solution {
    pub fn is_valid(s: String) -> bool {
        let mut map = HashMap::new();
        map.insert('(', ')');
        map.insert('[', ']');
        map.insert('{', '}');
        let mut stack = vec![];
        for c in s.chars() {
            if map.contains_key(&c) {
                stack.push(map[&c]);
            } else if stack.pop().unwrap_or(' ') != c {
                return false;
            }
        }
        stack.len() == 0
    }
}
```

### **JavaScript**
```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function (s) {
    let stk = [];
    for (const c of s) {
        if (c == '(' || c == '{' || c == '[') {
            stk.push(c);
        } else if (stk.length == 0 || !match(stk[stk.length - 1], c)) {
            return false;
        } else {
            stk.pop();
        }
    }
    return stk.length == 0;
};

function match(l, r) {
    return (l == '(' && r == ')') || (l == '[' && r == ']') || (l == '{' && r == '}');
}
```

### **C#**
```cs
public class Solution {
    public bool IsValid(string s) {
        Stack<char> stk = new Stack<char>();
        foreach (var c in s.ToCharArray()) {
            if (c == '(') {
                stk.Push(')');
            } else if (c == '[') {
                stk.Push(']');
            } else if (c == '{') {
                stk.Push('}');
            } else if (stk.Count == 0 || stk.Pop() != c) {
                return false;
            }
        }
        return stk.Count == 0;
    }
}
```

### **Ruby**
```rb
# @param {String} s
# @return {Boolean}
def is_valid(s)
  stack = ''
  s.split('').each do |c|
    if ['{', '[', '('].include?(c)
      stack += c
    else
      if c == '}' && stack[stack.length - 1] == '{'

        stack = stack.length > 1 ? stack[0..stack.length - 2] : ""
      elsif c == ']' && stack[stack.length - 1] == '['
        stack = stack.length > 1 ? stack[0..stack.length - 2] : ""
      elsif c == ')' && stack[stack.length - 1] == '('
        stack = stack.length > 1 ? stack[0..stack.length - 2] : ""
      else
        return false
      end
    end
  end
  stack == ''
end
```

### **PHP**
```php
class Solution {
    /**
     * @param string $s
     * @return boolean
     */

    function isValid($s) {
        $stack = [];
        $brackets = [
            ')' => '(',
            '}' => '{',
            ']' => '[',
        ];

        for ($i = 0; $i < strlen($s); $i++) {
            $char = $s[$i];
            if (array_key_exists($char, $brackets)) {
                if (empty($stack) || $stack[count($stack) - 1] !== $brackets[$char]) {
                    return false;
                }
                array_pop($stack);
            } else {
                array_push($stack, $char);
            }
        }
        return empty($stack);
    }
}
```