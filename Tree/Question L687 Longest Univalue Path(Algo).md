

## Question L687 Longest Univalue Path(Algo)


Available @ <https://leetcode.com/problems/longest-univalue-path/description/>

	Given a binary tree, find the length of the longest path where each node in the path has the same value. This path may or may not pass through the root.
	
	Note: The length of path between two nodes is represented by the number of edges between them.
	
	Example 1:
	
	Input:
	
	              5
	             / \
	            4   5
	           / \   \
	          1   1   5
	Output:
	
	2
	Example 2:
	
	Input:
	
	              1
	             / \
	            4   5
	           / \   \
	          4   4   5
	Output:

	2


### **Idea**

* **USE** `Recursion` !! 
* **NOTE** Think of the subproblem and how you define this problem!!!!

	
	
### Solution 1.0 (Recursion + Many Case Conditions)
	class Solution {
		 /*
		 用gMax是因为这个recursion每一次都需要比较很多次！
		 */
	    private int gMax = 0;	    
	    // return the longest length up to root
	    public int longestUnivaluePath(TreeNode root) {
	        if (root == null) return 0;   
	        longestPathFromNode(root);
	        return gMax;
	    }
	    
	    /*
	    0. Return the longest path including this node
	    1. Define this recursion --> you must include this node 
	    */	             
	    private int longestPathFromNode(TreeNode node) {
	    	// base case
	        if (node == null) return 0;
	        // the max length so far including this node -> default to 0
	        int count = 0;
	        
	        // left: the longest path length including node.left
	        int left = longestPathFromNode(node.left);
	        int right = longestPathFromNode(node.right);
	        
	        // Now the case 1: when node.val = node.left.val, then
	        // we must increment left by 1 -> include this node
	        if (node.left != null && node.val == node.left.val) {
	            left += 1;
	            // update count for this level
	            count = left;
	        }
	        // case 2: similar to the left condition
	        if (node.right != null && node.val == node.right.val) {
	            right += 1;
	            // update count for this level 
	            count = Math.max(count, right);
	        }
	                
	        // case 3: a bridge condition!!!
	        if (node.left != null && node.val == node.left.val &&
	            node.right != null && node.left.val == node.right.val) {
	            gMax = Math.max(gMax, left + right);            
	        }
	        
			 // case 4: we need to update the gMax!!! in case 
			 //			  case 3 is not reached
	        gMax = Math.max(count, gMax);
	        
	        // This is important! We return count!!
	        return count;
	    }
	}




### Solution 2.0 (Recursion But Different Function Definition) 
	class Solution {    
	    private int gMax = 0;
	    
	    // return the longest length up to root
	    public int longestUnivaluePath(TreeNode root) {
	        if (root == null) return 0;  
	        
	        // initially --> make sure the root.val is not found 
	        longestPathFromNode(root, root.val - 1);
	        return gMax;
	    }
	    
	    // this recursion 
	    // 1.--> you must include this node 
	    // 2.--> you ONLY increment IFF prevValue equals to this node's value
	    private int longestPathFromNode(TreeNode node, int preValue) {
	        if (node == null) return 0;
	        // Check this out: you now put the node.val to the next recursion!!!!
	        int left = longestPathFromNode(node.left, node.val);
	        int right = longestPathFromNode(node.right, node.val);
	        int count = 0;
	        
	        // NOTE: left means that the longestPath with values equals to current node.val
	        //       similarly for right 
	        // so gMax can be safely derived this way
	        gMax = Math.max(gMax, left + right);
	        
	        // Trick for returning the value!!! 
	        // WE ONLY RETURN 1 PATH to AVOID Y shape!
	        if (node.val == preValue) {
	            count = 1 + Math.max(left, right);
	        }
	        
	        // No Need -> because the previous comparison: gMax = Math.max(gMax, left +right); 
	        // So -> gMax = Math.max( c, gMax); is not required ANY MORE!!!!!!!!
	        return count;
	    }
	}
