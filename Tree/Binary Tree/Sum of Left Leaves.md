
https://leetcode.com/problems/sum-of-left-leaves/

#define data val
class Solution {
public:
	int sumOfLeftLeaves(TreeNode* root, bool isLeft = false) { //default argument
		if (!root)
			return 0;

		if (!root->left && !root->right) {
			return isLeft ? root->data : 0;
		}

		return sumOfLeftLeaves(root->left, 1) + sumOfLeftLeaves(root->right, 0);
	}
};

#define data val
class Solution {
	void sumOfLeftLeavesHelper(TreeNode *root, int &sum) {
		if (!root)
			return;

		if (root->left && !root->left->left && !root->left->right) {
			sum += root->left->data;
		}

		sumOfLeftLeavesHelper(root->left, sum);
		sumOfLeftLeavesHelper(root->right, sum);
	}
public:
	int sumOfLeftLeaves(TreeNode* root) {
		int sum = 0;
		sumOfLeftLeavesHelper(root, sum);
		return sum;
	}
};

#define data val
class Solution {
public:
	int sumOfLeftLeaves(TreeNode* root) {
		if (!root)
			return 0;
		int sum = 0;
		if (root->left) {
			if (!root->left->left && !root->left->right) {
				sum += root->left->data;
			}
			else {
				sum += sumOfLeftLeaves(root->left);
			}
		}

		sum += sumOfLeftLeaves(root->right);

		return sum;
	}
};
