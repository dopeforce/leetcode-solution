# [**16. 3Sum Closest**](https://leetcode.com/problems/3sum-closest)

<p>Given an integer array <code>nums</code> of length <code>n</code> and an integer <code>target</code>, find three integers in <code>nums</code> such that the sum is closest to <code>target</code>.</p>
<p>Return <em>the sum of the three integers</em>.</p>
<p>You may assume that each input would have exactly one solution.</p>
<pre>
<h3><strong class="example">Example 1:</strong></h3>
<strong>Input:</strong> nums = [-1,2,1,-4], target = 1
<strong>Output:</strong> 2
<strong>Explanation:</strong> The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
</pre>
<pre>
<h3><strong class="example">Example 2:</strong></h3>
<strong>Input:</strong> nums = [0,0,0], target = 1
<strong>Output:</strong> 0
<strong>Explanation:</strong> The sum that is closest to the target is 0. (0 + 0 + 0 = 0).
</pre>
<h3><strong>Constraints:</strong></h3>
<ul>
	<li><code>3 &lt;= nums.length &lt;= 500</code></li>
	<li><code>-1000 &lt;= nums[i] &lt;= 1000</code></li>
	<li><code>-10<sup>4</sup> &lt;= target &lt;= 10<sup>4</sup></code></li>
</ul>
<p>&nbsp;</p>

# **Solutions**

### **Python3**
```python
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        nums.sort()
        n = len(nums)
        ans = inf
        for i, v in enumerate(nums):
            j, k = i + 1, n - 1
            while j < k:
                t = v + nums[j] + nums[k]
                if t == target:
                    return t
                if abs(t - target) < abs(ans - target):
                    ans = t
                if t > target:
                    k -= 1
                else:
                    j += 1
        return ans
```

### **Java**
```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int ans = 1 << 30;
        int n = nums.length;
        for (int i = 0; i < n; ++i) {
            int j = i + 1, k = n - 1;
            while (j < k) {
                int t = nums[i] + nums[j] + nums[k];
                if (t == target) {
                    return t;
                }
                if (Math.abs(t - target) < Math.abs(ans - target)) {
                    ans = t;
                }
                if (t > target) {
                    --k;
                } else {
                    ++j;
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
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());
        int ans = 1 << 30;
        int n = nums.size();
        for (int i = 0; i < n; ++i) {
            int j = i + 1, k = n - 1;
            while (j < k) {
                int t = nums[i] + nums[j] + nums[k];
                if (t == target) return t;
                if (abs(t - target) < abs(ans - target)) ans = t;
                if (t > target)
                    --k;
                else
                    ++j;
            }
        }
        return ans;
    }
};
```

### **Go**
```go
func threeSumClosest(nums []int, target int) int {
	sort.Ints(nums)
	ans := 1 << 30
	n := len(nums)
	for i, v := range nums {
		j, k := i+1, n-1
		for j < k {
			t := v + nums[j] + nums[k]
			if t == target {
				return t
			}
			if abs(t-target) < abs(ans-target) {
				ans = t
			}
			if t > target {
				k--
			} else {
				j++
			}
		}
	}
	return ans
}

func abs(x int) int {
	if x < 0 {
		return -x
	}
	return x
}
```

### **TypeScript**
```ts
function threeSumClosest(nums: number[], target: number): number {
    nums.sort((a, b) => a - b);
    let ans: number = 1 << 30;
    const n = nums.length;
    for (let i = 0; i < n; ++i) {
        let j = i + 1;
        let k = n - 1;
        while (j < k) {
            const t: number = nums[i] + nums[j] + nums[k];
            if (t === target) {
                return t;
            }
            if (Math.abs(t - target) < Math.abs(ans - target)) {
                ans = t;
            }
            if (t > target) {
                --k;
            } else {
                ++j;
            }
        }
    }
    return ans;
}
```

### **JavaScript**
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var threeSumClosest = function (nums, target) {
    nums.sort((a, b) => a - b);
    let ans = 1 << 30;
    const n = nums.length;
    for (let i = 0; i < n; ++i) {
        let j = i + 1;
        let k = n - 1;
        while (j < k) {
            const t = nums[i] + nums[j] + nums[k];
            if (t === target) {
                return t;
            }
            if (Math.abs(t - target) < Math.abs(ans - target)) {
                ans = t;
            }
            if (t > target) {
                --k;
            } else {
                ++j;
            }
        }
    }
    return ans;
};
```

### **PHP**
```php
class Solution {
    /**
     * @param int[] $nums
     * @param int $target
     * @return int
     */

    function threeSumClosest($nums, $target) {
        $n = count($nums);
        $closestSum = $nums[0] + $nums[1] + $nums[2];
        $minDiff = abs($closestSum - $target);

        sort($nums);

        for ($i = 0; $i < $n - 2; $i++) {
            $left = $i + 1;
            $right = $n - 1;

            while ($left < $right) {
                $sum = $nums[$i] + $nums[$left] + $nums[$right];
                $diff = abs($sum - $target);

                if ($diff < $minDiff) {
                    $minDiff = $diff;
                    $closestSum = $sum;
                } elseif ($sum < $target) {
                    $left++;
                } elseif ($sum > $target) {
                    $right--;
                } else {
                    return $sum;
                }
            }
        }

        return $closestSum;
    }
}
```