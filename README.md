# Construct Binary Tree from Preorder and Inorder Traversal
# https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal

Given preorder and inorder traversal of a tree, construct the binary tree.

**Note : You may assume that duplicates do not exist in the tree.**
```
For example, given

preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
Return the following binary tree:

    3
   / \
  9  20
    /  \
   15   7
```

## Implementation 

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public static TreeNode buildTree(int[] preorder, int[] inorder) {
	      int preOrderStart = 0;
	      int preOrderEnd = preorder.length - 1;
	      int inOrderStart = 0;
	      int inOrderEnd = inorder.length - 1;
	      Map<Integer, Integer> map = new HashMap<>();
	      for(int i = 0; i < inorder.length; i++) {
	    	  map.put(inorder[i], i);
	      }
	      return construct(inorder, inOrderStart, inOrderEnd, preorder, preOrderStart, preOrderEnd, map);
	}
	
	private static TreeNode construct(int[] inorder, int inStart, int inEnd, 
									  int[] preorder, int preStart, int preEnd, Map<Integer, Integer> map)       {
		if(inStart > inEnd || preStart > preEnd)
			return null;
		
		TreeNode node = new TreeNode(preorder[preStart]);
		int rootIndex = map.get(preorder[preStart]);
		int sizeOfLeftSubtree = rootIndex - inStart;	
		node.left = construct(inorder, inStart, rootIndex - 1, 
                              preorder, preStart+1, preStart+sizeOfLeftSubtree, map);
		node.right = construct(inorder, rootIndex + 1, inEnd, 
                               preorder, preStart+sizeOfLeftSubtree+1, preEnd, map);
		return node;
	}
}
```
