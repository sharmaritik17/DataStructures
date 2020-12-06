``` cpp
https://leetcode.com/problems/diameter-of-binary-tree/

https://leetcode.com/problems/diameter-of-binary-tree/discuss/962035/DP-on-Trees-or-Interview-or-Explanation


class Solution {
private:
	int diameterOfBinaryTreehelper(TreeNode *root, int &diameterSoFar) {
		if (!root)
			return 0;

		int leftAns = diameterOfBinaryTreehelper(root->left, diameterSoFar);
		int rightAns = diameterOfBinaryTreehelper(root->right, diameterSoFar);

		diameterSoFar = max(diameterSoFar, leftAns + rightAns);

		return 1 + max(leftAns, rightAns);
	}
public:
	int diameterOfBinaryTree(TreeNode* root) {
		if (!root)
			return 0;

		int diameterSoFar = 0;
		diameterOfBinaryTreehelper(root, diameterSoFar);
		return diameterSoFar;
	}
};
