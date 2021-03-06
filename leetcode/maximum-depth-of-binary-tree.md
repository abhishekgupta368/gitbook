# 104. Maximum Depth of Binary Tree

* *Difficulty: Easy*

* *Topics: Tree, Depth-first Search*

* *Similar Questions:*

  * [Balanced Binary Tree](balanced-binary-tree.md)

  * [Minimum Depth of Binary Tree](minimum-depth-of-binary-tree.md)

  * [Maximum Depth of N-ary Tree](maximum-depth-of-n-ary-tree.md)

## Problem:

<p>Given a binary tree, find its maximum depth.</p>

<p>The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.</p>

<p><strong>Note:</strong>&nbsp;A leaf is a node with no children.</p>

<p><strong>Example:</strong></p>

<p>Given binary tree <code>[3,9,20,null,null,15,7]</code>,</p>

<pre>
    3
   / \
  9  20
    /  \
   15   7</pre>

<p>return its depth = 3.</p>

## Solutions:

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == NULL)   return 0;
        return 1 + std::max(maxDepth(root->left), maxDepth(root->right));
    }
};
```
