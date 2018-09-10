### L250 Count Univalue Subtrees
Available @ <https://leetcode.com/problems/count-univalue-subtrees/description/>

    Given a binary tree, count the number of uni-value subtrees.

    A Uni-value subtree means all nodes of the subtree have the same value.

    Example :

    Input:  root = [5,1,5,5,5,null,5]

                  5
                 / \
                1   5
               / \   \
              5   5   5

    Output: 4
    


### Idea
* **Define** a recursion function CAREFUL!
	* `Solution 1.0` defines **boolean** `checkUni(TreeNode node)`, whether that node is `Univalue Subtree`
	* **PLEASE** note the following cases!

	
### Types Diagram
	4 types:
	
		a             a             a              a
    null  null      null a        a  null        a   a
		
	     
### Solution 1.0
	class Solution {
	    int count;    
	    public int countUnivalSubtrees(TreeNode root) {
	        count = 0;
	        checkUni(root);
	        return count;
	    }
	    
	    // check whether node (including this one) is a subtree of univalue
	    private boolean checkUni(TreeNode node) {
	        // base case
	        if (node == null) return true;
	        boolean left = checkUni(node.left);
	        boolean right = checkUni(node.right);
	        // both left & right
	        if (left && right) {
	            // 4 types of cases together 
	            /* THESE ARE THE FOLLOWING!!!
	                   a             a             a              a
	               null  null      null a        a  null        a   a
	            */            
	            
	            if ( ((node.left == null) || (node.left.val == node.val)) &&
	                 (node.right == null || (node.right.val == node.val))
	               )
	            {
	                count ++;
	                return true;
	            }
	
	        }
	        
	        return false;
	    }    
	}


### Solution 2.0 (Similar ALTERNATIVE to Global Variable)
    public int countUnivalSubtrees(TreeNode root) {
        // defaults to 0
        int[] valSet = new int[1];
        getUni(root, valSet);
        
        return valSet[0];
    }
    
    // check whether node is uniTree, and increment valSet -> java by reference
    private boolean getUni(TreeNode node, int[] valSet) {
        // base case
        if (node == null) return true;
        
        boolean left = getUni(node.left, valSet);
        boolean right = getUni(node.right, valSet);
        
        // case 4 types
        if (left && right) {
            if ((node.left == null || node.left.val == node.val) &&
                (node.right == null || node.right.val == node.val)) {
                valSet[0] ++;
                return true;
            }                            
        }
        
        return false;
    }
    