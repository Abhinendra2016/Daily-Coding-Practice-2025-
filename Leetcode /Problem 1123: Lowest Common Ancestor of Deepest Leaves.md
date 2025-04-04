# Problem 1123: Lowest Common Ancestor of Deepest Leaves

Given the root of a binary tree, return the lowest common ancestor of its deepest leaves.

Recall that:
- The node of a binary tree is a leaf if and only if it has no children.
- The depth of the root of the tree is 0. If the depth of a node is d, the depth of each of its children is d + 1.
- The lowest common ancestor (LCA) of a set `S` of nodes is the node `A` with the largest depth such that every node in `S` is in the subtree rooted at `A`.

## Examples

**Example 1:**
Input: root = [3,5,1,6,2,0,8,null,null,7,4] Output: [2,7,4] Explanation: The LCA is the node with value 2. The deepest nodes are 7 and 4, both with depth 3.


**Example 2:**


Input: root = [1] Output: [1] Explanation: The root itself is the only and deepest node.

**Example 3:**

Input: root = [0,1,3,null,2] Output: [2] Explanation: The deepest node is 2, and its LCA is itself.


## Constraints

- The number of nodes in the tree is in the range [1, 1000].
- `0 <= Node.val <= 1000`
- All node values are unique.

## Solution

```python
from typing import Optional

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def lcaDeepestLeaves(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        def dfs(node):
            if not node:
                return 0, None
            
            left_depth, left_lca = dfs(node.left)
            right_depth, right_lca = dfs(node.right)
            
            if left_depth > right_depth:
                return left_depth + 1, left_lca
            elif left_depth < right_depth:
                return right_depth + 1, right_lca
            else:
                return left_depth + 1, node
        
        return dfs(root)[1]
```
<h2>Time Complexity</h2> O(n) — Every node in the binary tree is visited once using DFS.<br>
 <h2>Space Complexity</h2> O(h) — Where h is the height of the binary tree due to recursive stack space. <br>
 <h2>Explanation</h2> We perform a post-order DFS traversal to compute: - the depth of the left and right subtrees, and - the LCA of deepest leaves in both subtrees.<br>
If the left and right subtrees are of equal depth, the current node is the LCA. Otherwise, we propagate the deeper subtree's LCA up the recursion.<br>


