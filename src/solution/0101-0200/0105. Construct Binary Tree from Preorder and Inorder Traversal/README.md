# [**105. Construct Binary Tree from Preorder and Inorder Traversal**](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal)

<p>Given two integer arrays <code>preorder</code> and <code>inorder</code> where <code>preorder</code> is the preorder traversal of a binary tree and <code>inorder</code> is the inorder traversal of the same tree, construct and return <em>the binary tree</em>.</p>
<img alt="" src="https://fastly.jsdelivr.net/gh/doocs/leetcode@main/solution/0100-0199/0105.Construct%20Binary%20Tree%20from%20Preorder%20and%20Inorder%20Traversal/images/tree.jpg" style="width: 1200px; height: 600px;" />
<h3><strong class="example">Example 1:</strong></h3>
<pre>
<strong>Input:</strong> preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
<strong>Output:</strong> [3,9,20,null,null,15,7]
</pre>
<h3><strong class="example">Example 2:</strong></h3>
<pre>
<strong>Input:</strong> preorder = [-1], inorder = [-1]
<strong>Output:</strong> [-1]
</pre>
<h3><strong>Constraints:</strong></h3>
<ul>
	<li><code>1 &lt;= preorder.length &lt;= 3000</code></li>
	<li><code>inorder.length == preorder.length</code></li>
	<li><code>-3000 &lt;= preorder[i], inorder[i] &lt;= 3000</code></li>
	<li><code>preorder</code> and <code>inorder</code> consist of <strong>unique</strong> values.</li>
	<li>Each value of <code>inorder</code> also appears in <code>preorder</code>.</li>
	<li><code>preorder</code> is <strong>guaranteed</strong> to be the preorder traversal of the tree.</li>
	<li><code>inorder</code> is <strong>guaranteed</strong> to be the inorder traversal of the tree.</li>
</ul>
<p>&nbsp;</p>

# **Solutions**

### **Python3**
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        def dfs(i: int, j: int, n: int) -> Optional[TreeNode]:
            if n <= 0:
                return None
            v = preorder[i]
            k = d[v]
            l = dfs(i + 1, j, k - j)
            r = dfs(i + 1 + k - j, k + 1, n - k + j - 1)
            return TreeNode(v, l, r)

        d = {v: i for i, v in enumerate(inorder)}
        return dfs(0, 0, len(preorder))
```

### **Java**
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    private int[] preorder;
    private Map<Integer, Integer> d = new HashMap<>();

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        int n = preorder.length;
        this.preorder = preorder;
        for (int i = 0; i < n; ++i) {
            d.put(inorder[i], i);
        }
        return dfs(0, 0, n);
    }

    private TreeNode dfs(int i, int j, int n) {
        if (n <= 0) {
            return null;
        }
        int v = preorder[i];
        int k = d.get(v);
        TreeNode l = dfs(i + 1, j, k - j);
        TreeNode r = dfs(i + 1 + k - j, k + 1, n - 1 - (k - j));
        return new TreeNode(v, l, r);
    }
}
```

### **C++**
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        int n = preorder.size();
        unordered_map<int, int> d;
        for (int i = 0; i < n; ++i) {
            d[inorder[i]] = i;
        }
        function<TreeNode*(int, int, int)> dfs = [&](int i, int j, int n) -> TreeNode* {
            if (n <= 0) {
                return nullptr;
            }
            int v = preorder[i];
            int k = d[v];
            TreeNode* l = dfs(i + 1, j, k - j);
            TreeNode* r = dfs(i + 1 + k - j, k + 1, n - 1 - (k - j));
            return new TreeNode(v, l, r);
        };
        return dfs(0, 0, n);
    }
};
```

### **Go**
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func buildTree(preorder []int, inorder []int) *TreeNode {
	d := map[int]int{}
	for i, x := range inorder {
		d[x] = i
	}
	var dfs func(i, j, n int) *TreeNode
	dfs = func(i, j, n int) *TreeNode {
		if n <= 0 {
			return nil
		}
		v := preorder[i]
		k := d[v]
		l := dfs(i+1, j, k-j)
		r := dfs(i+1+k-j, k+1, n-1-(k-j))
		return &TreeNode{v, l, r}
	}
	return dfs(0, 0, len(preorder))
}
```

### **TypeScript**

```ts
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function buildTree(preorder: number[], inorder: number[]): TreeNode | null {
    const d: Map<number, number> = new Map();
    const n = inorder.length;
    for (let i = 0; i < n; ++i) {
        d.set(inorder[i], i);
    }
    const dfs = (i: number, j: number, n: number): TreeNode | null => {
        if (n <= 0) {
            return null;
        }
        const v = preorder[i];
        const k = d.get(v)!;
        const l = dfs(i + 1, j, k - j);
        const r = dfs(i + 1 + k - j, k + 1, n - 1 - (k - j));
        return new TreeNode(v, l, r);
    };
    return dfs(0, 0, n);
}
```

### **Rust**

```rust
// Definition for a binary tree node.
// #[derive(Debug, PartialEq, Eq)]
// pub struct TreeNode {
//   pub val: i32,
//   pub left: Option<Rc<RefCell<TreeNode>>>,
//   pub right: Option<Rc<RefCell<TreeNode>>>,
// }
//
// impl TreeNode {
//   #[inline]
//   pub fn new(val: i32) -> Self {
//     TreeNode {
//       val,
//       left: None,
//       right: None
//     }
//   }
// }
use std::cell::RefCell;
use std::collections::HashMap;
use std::rc::Rc;
impl Solution {
    pub fn build_tree(preorder: Vec<i32>, inorder: Vec<i32>) -> Option<Rc<RefCell<TreeNode>>> {
        let mut d = HashMap::new();
        for (i, &x) in inorder.iter().enumerate() {
            d.insert(x, i);
        }
        Self::dfs(&preorder, &d, 0, 0, preorder.len())
    }

    pub fn dfs(
        preorder: &Vec<i32>,
        d: &HashMap<i32, usize>,
        i: usize,
        j: usize,
        n: usize,
    ) -> Option<Rc<RefCell<TreeNode>>> {
        if n <= 0 {
            return None;
        }
        let v = preorder[i];
        let k = d[&v];
        let mut root = TreeNode::new(v);
        root.left = Self::dfs(preorder, d, i + 1, j, k - j);
        root.right = Self::dfs(preorder, d, i + k - j + 1, k + 1, n - k + j - 1);
        Some(Rc::new(RefCell::new(root)))
    }
}
```

### **JavaScript**
```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {number[]} preorder
 * @param {number[]} inorder
 * @return {TreeNode}
 */
var buildTree = function (preorder, inorder) {
    const d = new Map();
    const n = inorder.length;
    for (let i = 0; i < n; ++i) {
        d.set(inorder[i], i);
    }
    const dfs = (i, j, n) => {
        if (n <= 0) {
            return null;
        }
        const v = preorder[i];
        const k = d.get(v);
        const l = dfs(i + 1, j, k - j);
        const r = dfs(i + 1 + k - j, k + 1, n - 1 - (k - j));
        return new TreeNode(v, l, r);
    };
    return dfs(0, 0, n);
};
```