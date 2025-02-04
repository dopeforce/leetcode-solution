# [**18. 4Sum**](https://leetcode.com/problems/4sum)

<p>Given an array <code>nums</code> of <code>n</code> integers, return <em>an array of all the <strong>unique</strong> quadruplets</em> <code>[nums[a], nums[b], nums[c], nums[d]]</code> such that:</p>
<ul>
	<li><code>0 &lt;= a, b, c, d&nbsp;&lt; n</code></li>
	<li><code>a</code>, <code>b</code>, <code>c</code>, and <code>d</code> are <strong>distinct</strong>.</li>
	<li><code>nums[a] + nums[b] + nums[c] + nums[d] == target</code></li>
</ul>
<p>You may return the answer in <strong>any order</strong>.</p>
<h3><strong class="example">Example 1:</strong></h3>
<pre>
<strong>Input:</strong> nums = [1,0,-1,0,-2,2], target = 0
<strong>Output:</strong> [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
</pre>
<h3><strong class="example">Example 2:</strong></h3>
<pre>
<strong>Input:</strong> nums = [2,2,2,2,2], target = 8
<strong>Output:</strong> [[2,2,2,2]]
</pre>
<h3><strong>Constraints:</strong></h3>
<ul>
	<li><code>1 &lt;= nums.length &lt;= 200</code></li>
	<li><code>-10<sup>9</sup> &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= target &lt;= 10<sup>9</sup></code></li>
</ul>
<p>&nbsp;</p>

# **Solutions**

### **Python3**
```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        n = len(nums)
        ans = []
        if n < 4:
            return ans
        nums.sort()
        for i in range(n - 3):
            if i and nums[i] == nums[i - 1]:
                continue
            for j in range(i + 1, n - 2):
                if j > i + 1 and nums[j] == nums[j - 1]:
                    continue
                k, l = j + 1, n - 1
                while k < l:
                    x = nums[i] + nums[j] + nums[k] + nums[l]
                    if x < target:
                        k += 1
                    elif x > target:
                        l -= 1
                    else:
                        ans.append([nums[i], nums[j], nums[k], nums[l]])
                        k, l = k + 1, l - 1
                        while k < l and nums[k] == nums[k - 1]:
                            k += 1
                        while k < l and nums[l] == nums[l + 1]:
                            l -= 1
        return ans
```

### **Java**
```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        int n = nums.length;
        List<List<Integer>> ans = new ArrayList<>();
        if (n < 4) {
            return ans;
        }
        Arrays.sort(nums);
        for (int i = 0; i < n - 3; ++i) {
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            for (int j = i + 1; j < n - 2; ++j) {
                if (j > i + 1 && nums[j] == nums[j - 1]) {
                    continue;
                }
                int k = j + 1, l = n - 1;
                while (k < l) {
                    long x = (long) nums[i] + nums[j] + nums[k] + nums[l];
                    if (x < target) {
                        ++k;
                    } else if (x > target) {
                        --l;
                    } else {
                        ans.add(List.of(nums[i], nums[j], nums[k++], nums[l--]));
                        while (k < l && nums[k] == nums[k - 1]) {
                            ++k;
                        }
                        while (k < l && nums[l] == nums[l + 1]) {
                            --l;
                        }
                    }
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
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        int n = nums.size();
        vector<vector<int>> ans;
        if (n < 4) {
            return ans;
        }
        sort(nums.begin(), nums.end());
        for (int i = 0; i < n - 3; ++i) {
            if (i && nums[i] == nums[i - 1]) {
                continue;
            }
            for (int j = i + 1; j < n - 2; ++j) {
                if (j > i + 1 && nums[j] == nums[j - 1]) {
                    continue;
                }
                int k = j + 1, l = n - 1;
                while (k < l) {
                    long long x = (long long) nums[i] + nums[j] + nums[k] + nums[l];
                    if (x < target) {
                        ++k;
                    } else if (x > target) {
                        --l;
                    } else {
                        ans.push_back({nums[i], nums[j], nums[k++], nums[l--]});
                        while (k < l && nums[k] == nums[k - 1]) {
                            ++k;
                        }
                        while (k < l && nums[l] == nums[l + 1]) {
                            --l;
                        }
                    }
                }
            }
        }
        return ans;
    }
};
```

### **Go**
```go
func fourSum(nums []int, target int) (ans [][]int) {
	n := len(nums)
	if n < 4 {
		return
	}
	sort.Ints(nums)
	for i := 0; i < n-3; i++ {
		if i > 0 && nums[i] == nums[i-1] {
			continue
		}
		for j := i + 1; j < n-2; j++ {
			if j > i+1 && nums[j] == nums[j-1] {
				continue
			}
			k, l := j+1, n-1
			for k < l {
				x := nums[i] + nums[j] + nums[k] + nums[l]
				if x < target {
					k++
				} else if x > target {
					l--
				} else {
					ans = append(ans, []int{nums[i], nums[j], nums[k], nums[l]})
					k++
					l--
					for k < l && nums[k] == nums[k-1] {
						k++
					}
					for k < l && nums[l] == nums[l+1] {
						l--
					}
				}
			}
		}
	}
	return
}
```

### **TypeScript**
```ts
function fourSum(nums: number[], target: number): number[][] {
    const n = nums.length;
    const ans: number[][] = [];
    if (n < 4) {
        return ans;
    }
    nums.sort((a, b) => a - b);
    for (let i = 0; i < n - 3; ++i) {
        if (i > 0 && nums[i] === nums[i - 1]) {
            continue;
        }
        for (let j = i + 1; j < n - 2; ++j) {
            if (j > i + 1 && nums[j] === nums[j - 1]) {
                continue;
            }
            let [k, l] = [j + 1, n - 1];
            while (k < l) {
                const x = nums[i] + nums[j] + nums[k] + nums[l];
                if (x < target) {
                    ++k;
                } else if (x > target) {
                    --l;
                } else {
                    ans.push([nums[i], nums[j], nums[k++], nums[l--]]);
                    while (k < l && nums[k] === nums[k - 1]) {
                        ++k;
                    }
                    while (k < l && nums[l] === nums[l + 1]) {
                        --l;
                    }
                }
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
 * @return {number[][]}
 */
var fourSum = function (nums, target) {
    const n = nums.length;
    const ans = [];
    if (n < 4) {
        return ans;
    }
    nums.sort((a, b) => a - b);
    for (let i = 0; i < n - 3; ++i) {
        if (i > 0 && nums[i] === nums[i - 1]) {
            continue;
        }
        for (let j = i + 1; j < n - 2; ++j) {
            if (j > i + 1 && nums[j] === nums[j - 1]) {
                continue;
            }
            let [k, l] = [j + 1, n - 1];
            while (k < l) {
                const x = nums[i] + nums[j] + nums[k] + nums[l];
                if (x < target) {
                    ++k;
                } else if (x > target) {
                    --l;
                } else {
                    ans.push([nums[i], nums[j], nums[k++], nums[l--]]);
                    while (k < l && nums[k] === nums[k - 1]) {
                        ++k;
                    }
                    while (k < l && nums[l] === nums[l + 1]) {
                        --l;
                    }
                }
            }
        }
    }
    return ans;
};
```

### **C#**
```cs
public class Solution {
    public IList<IList<int>> FourSum(int[] nums, int target) {
        int n = nums.Length;
        var ans = new List<IList<int>>();
        if (n < 4) {
            return ans;
        }
        Array.Sort(nums);
        for (int i = 0; i < n - 3; ++i) {
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            for (int j = i + 1; j < n - 2; ++j) {
                if (j > i + 1 && nums[j] == nums[j - 1]) {
                    continue;
                }
                int k = j + 1, l = n - 1;
                while (k < l) {
                    long x = (long) nums[i] + nums[j] + nums[k] + nums[l];
                    if (x < target) {
                        ++k;
                    } else if (x > target) {
                        --l;
                    } else {
                        ans.Add(new List<int> {nums[i], nums[j], nums[k++], nums[l--]});
                        while (k < l && nums[k] == nums[k - 1]) {
                            ++k;
                        }
                        while (k < l && nums[l] == nums[l + 1]) {
                            --l;
                        }
                    }
                }
            }
        }
        return ans;
    }
}
```

### **PHP**
```php
class Solution {
    /**
     * @param int[] $nums
     * @param int $target
     * @return int[][]
     */

    function fourSum($nums, $target) {
        $result = [];
        $n = count($nums);

        sort($nums);

        for ($i = 0; $i < $n - 3; $i++) {
            if ($i > 0 && $nums[$i] === $nums[$i - 1]) {
                continue;
            }

            for ($j = $i + 1; $j < $n - 2; $j++) {
                if ($j > $i + 1 && $nums[$j] === $nums[$j - 1]) {
                    continue;
                }

                $left = $j + 1;
                $right = $n - 1;

                while ($left < $right) {
                    $sum = $nums[$i] + $nums[$j] + $nums[$left] + $nums[$right];

                    if ($sum === $target) {
                        $result[] = [$nums[$i], $nums[$j], $nums[$left], $nums[$right]];

                        while ($left < $right && $nums[$left] === $nums[$left + 1]) {
                            $left++;
                        }

                        while ($left < $right && $nums[$right] === $nums[$right - 1]) {
                            $right--;
                        }

                        $left++;
                        $right--;
                    } elseif ($sum < $target) {
                        $left++;
                    } else {
                        $right--;
                    }
                }
            }
        }
        return $result;
    }
}
```