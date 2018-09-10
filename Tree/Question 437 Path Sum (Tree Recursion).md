

## Question 437 Path Sum III
Available @ <https://leetcode.com/problems/path-sum-iii/description/>

	You are given a binary tree in which each node contains an integer value.
	
	Find the number of paths that sum to a given value.
	
	The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).
	
	The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.
	
	Example:
	
	root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8
	
	      10
	     /  \
	    5   -3
	   / \    \
	  3   2   11
	 / \   \
	3  -2   1
	
	Return 3. The paths that sum to 8 are:
	
	1.  5 -> 3
	2.  5 -> 2 -> 1
	3. -3 -> 11
	

### **Idea**
* **USE** `Recursion` with very subtle but impacting **huge differences**!!!
 	* `pathSum`: **defines** the total number of paths **EXCLUSING current node** == (`pathSum(left node)` + `pathSum(right node)` ) + **INCLUDING current node** `pathSumFrom(node)`
	
	* `pathSumFrom`: **defines** the total number of paths **INCLUDING** this node **ONLY**



	
### Solution 1.0 `Recursion + very subtle handling`
	    public int pathSum(TreeNode root, int sum) {
	        if (root == null) return 0;
	        //!!!! note pathSum(root.left, sum)!!!!!! INSTEAD OF helper!!!!!!!!
	        return pathSumFrom(root, sum) + pathSum(root.left, sum) + pathSum(root.right, sum);
	    }
	
	    // return # of path up to this node
	    private int pathSumFrom(TreeNode node, int remain) {
	        // base case
	        if (node == null) return 0;
	        // whether this node is the one we look for
	        int c = remain == node.val? 1: 0;
	        int left = pathSumFrom(node.left, remain - node.val);
	        int right = pathSumFrom(node.right, remain - node.val);
	
	        return c + left + right;
	    }
	
	      


