### Validate Binary Search Tree

	Given a binary tree, determine if it is a valid binary search tree (BST).
	
	Assume a BST is defined as follows:
	
	The left subtree of a node contains only nodes with keys less than the node's key.
	The right subtree of a node contains only nodes with keys greater than the node's key.
	Both the left and right subtrees must also be binary search trees.
	Example 1:
	
	Input:
	    2
	   / \
	  1   3
	Output: true
	Example 2:
	
	    5
	   / \
	  1   4
	     / \
	    3   6
	Output: false
	Explanation: The input is: [5,1,4,null,null,3,6]. The root node's value
	             is 5 but its right child's value is 4.

### Idea 1.0 + 2.0
* `1.0` BST 一般就是inOrder了 朋友 正的序列	
* `2.0` Recursion 
	* 根据题目的要求 recursion 的顺序不同 `bottom up` vs `top down`
		* `bottom up` -> 考虑下`反着`的顺序 + `update `一些 `global variable` 
		* `top down` -> 考虑下 你要怎么`return`参数 


### Iterative 思路 （2.0）
* 这就是inOrder的顺序而已


### Solution Iterative (2.0)
    public boolean isValidBST(TreeNode root) {
       if (root == null) return true;
       Stack<TreeNode> stack = new Stack<>();
       TreeNode pre = null;
       while (root != null || !stack.isEmpty()) {
          while (root != null) {
             stack.push(root);
             root = root.left;
          }
          root = stack.pop();
          if(pre != null && root.val <= pre.val) return false;
          pre = root;
          root = root.right;
       }
       return true;
    }


### Recursion 思路 (1.0)
* recursion的思路是 preOrder traversal 
	* `node`, `v(left)`, `v(right)`
	* 所以example的顺序是 `1, 2, 3, 4, 5, 6`
* 那如果我想`反着`过来的话
	* 顺序应该为 `6, 5, 4, 3, 2, 1`
	* (其实recursion就像 `Bottom Up 这个感觉`)
	* 可以通过 `v(right)`, `v(left)`, `node` 这个recursion来实现
	* `glboal prev` 来keep track
	 
### Solution Recursion -> Return 的参数
    public boolean isValidBST(TreeNode root) {
        return helper(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }
    
    private boolean helper(TreeNode node, long min, long max) {
        if (node == null) return true;
        if (node.val < min || node.val > max) return false;
        
        return helper(node.left, min,(long) node.val - 1) &&
               helper(node.right, (long) node.val + 1, max);
    }
	

    