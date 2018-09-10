### 114 Flatten Binary Tree to LinkedList

	Given a binary tree, flatten it to a linked list in-place.
	
	For example, given the following tree:
	
	    1
	   / \
	  2   5
	 / \   \
	3   4   6
	The flattened tree should look like:
	
	1
	 \
	  2
	   \
	    3
	     \
	      4
	       \
	        5
	         \
	          6


### Idea 根据要求的 order 你会发现
* 这tm就是道 preOrder的题目！！！ 顺序而已


### Recursion 思路 (1.0)
* recursion的思路是 preOrder traversal 
	* `node`, `v(left)`, `v(right)`
	* 所以example的顺序是 `1, 2, 3, 4, 5, 6`
* 那如果我想`反着`过来的话
	* 顺序应该为 `6, 5, 4, 3, 2, 1`
	* (其实recursion就像 `Bottom Up 这个感觉`)
	* 可以通过 `v(right)`, `v(left)`, `node` 这个recursion来实现
	* `glboal prev` 来keep track
	 
### Solution Recursion (1.0) + Bottom Up 这种
	   // 用一个global的prev来存每一次recursion的信息
		private TreeNode prev = null; 
		public void flatten(TreeNode root){
			if (root == null) return;
			flatten(root.right);		
			flatten(root.left);
			
			//这里做一个link 
			root.right = prev;
			// 左边的指向null 因为上一步 flattern已经 (root.left) 了
			root.left = null;
			prev = root;
		}  
	
### Iterative 思路 （2.0）
* 这tm就是道 preOrder的题目！！！ 顺序而已
* 所以可以 `preOrder` + `prev` 就可以解开了

### Solution Iterative (2.0)
    public void flatten(TreeNode root) {
        // preOrder the iterative
        Stack<TreeNode> stack = new Stack<>();
        TreeNode prev = new TreeNode(0);
        TreeNode cur = null;
        if (root != null) {
            stack.push(root);
        } 
        
        while(!stack.isEmpty()) {
            cur = stack.pop();
            // update prev.right and prev correspondingly
            prev.right = cur;
            prev = prev.right;
            
            if (cur.right != null) {
                stack.push(cur.right);
            }
            
            if (cur.left != null) {                
                stack.push(cur.left);
                // update cur.left
                cur.left = null;                
            }            

        }
        
    }	          