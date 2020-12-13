``` cpp
   https://leetcode.com/problems/cousins-in-binary-tree/

#define data val
class Solution {
	int depth(TreeNode *root, int x) {
		if (!root)
			return -1;

		if (root->data == x) {
			return 0;
		}

		int leftAns = depth(root->left, x);
		if (leftAns != -1) {
			return leftAns + 1;
		}
		else {
			int rightAns = depth(root->right, x);
			if (rightAns != -1) {
				return rightAns + 1;
			}
			else {
				return -1;
			}
		}
	}
	bool isSibling(TreeNode *root, int x, int y) {
		if (!root)
			return 0;

		if (root->left && root->right) {
			if (root->left->data == x && root->right->data == y) {
				return true;
			}
			else if (root->right->data == x && root->left->data == y) {
				return true;
			}
			else {
				return isSibling(root->left, x, y) || isSibling(root->right, y, x);
			}
		}

		if (root->left) {
			return isSibling(root->left, x, y);
		}
		else
			return isSibling(root->right, y, x);
	}
public:
	bool isCousins(TreeNode* root, int x, int y) {
		if (!root)
			return 0;

		return (depth(root, x) == depth(root, y)) && (!isSibling(root, x, y));
	}
};
