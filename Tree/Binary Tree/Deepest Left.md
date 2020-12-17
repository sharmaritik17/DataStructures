https://www.geeksforgeeks.org/deepest-left-leaf-node-in-a-binary-tree/
``` cpp


https://leetcode.com/problems/find-bottom-left-tree-value/

#define data val
class Solution {
	void findBottomLeftValueHelper(TreeNode *root, int currLevel, int &preLevel, int &leftVal) {
		if (!root)
			return;

		if (currLevel > preLevel) {
			preLevel = currLevel;
			leftVal = root->data;
		}
		if (currLevel == preLevel) {   // for gfg ques to find max ele only in last level
			leftVal = max(leftVal, root->data);
		}

		findBottomLeftValueHelper(root->left, currLevel + 1, preLevel, leftVal);
		findBottomLeftValueHelper(root->right, currLevel + 1, preLevel, leftVal);
	}
public:
	int findBottomLeftValue(TreeNode* root) {
		if (!root)
			return 0;

		int preLevel = 0;
		int leftVal = root->data; //case where only one node is present
		findBottomLeftValueHelper(root, 0, preLevel, leftVal);
		return leftVal;
	}
};




// awkward approach
void helper(BinaryTreeNode<int>* root, bool isLeft, int &max_level, int currlevel, int &value) {
	if (!root)
		return;

	if (isLeft && !root->left && !root->right && currlevel >= max_level) {
		if (currlevel != max_level) {
			max_level = currlevel;
			value = root->data;
		}
		else
			value = max(value, root->data);
	}

	helper(root->left, true, max_level, currlevel + 1, value);
	helper(root->right, false, max_level, currlevel + 1, value);
}

int solve(BinaryTreeNode<int>* root) {
	int value = -1;
    int max_level = 0;
	helper(root, false, max_level, 0, value);

	return value;
}
