https://leetcode.com/problems/check-completeness-of-a-binary-tree/


https://leetcode.com/problems/check-completeness-of-a-binary-tree/discuss/1179275/Pure-BFS-or-Runtime%3A-4-ms-faster-than-80.07-or-C%2B%2B


https://www.geeksforgeeks.org/check-whether-binary-tree-complete-not-set-2-recursive-solution/#:~:text=If%20the%20current%20node%20under,Return%20false.
``` cpp
class Solution {
	int countNodes(TreeNode *root){
		if(!root)
			return 0;
		return 1+ countNodes(root->left) + countNodes(root->right);
	}
	bool isCompleteTree(TreeNode* root,int totalNodes,int index) {
		if(!root)
			return 1;

		if(index>=totalNodes)
			return 0;

		return isCompleteTree(root->left,totalNodes,2*index+1) && isCompleteTree(root->right,totalNodes,2*index+2);
	}
public:
    bool isCompleteTree(TreeNode* root) {
    	int totalNodes = countNodes(root);
    	return isCompleteTree(root,totalNodes,0);
    }
};
