https://leetcode.com/problems/minimum-distance-between-bst-nodes/

``` cpp

#define data val
class Solution {
	void minDiffInBSTHelper(TreeNode *root, TreeNode *&pre, int &res) {
		if (!root)
			return;
		minDiffInBSTHelper(root->left, pre, res);
		if (pre) {
			res = min(res, root->data - pre->data);
		}
		pre = root;
		minDiffInBSTHelper(root->right, pre, res)
	}
public:
	int minDiffInBST(TreeNode* root) {
		int res = INT_MAX;
		TreeNode *pre = NULL;
		minDiffInBSTHelper(root, pre, res);
		return res;
	}
};

// iterative
#define data val
class Solution {
public:
	int minDiffInBST(TreeNode* root) {
		int finalMinDiff = INT_MAX;
		TreeNode *pre = NULL;
		stack<TreeNode*> pendingNodes;

		while (pendingNodes.size() || root) {
			while (root) {
				pendingNodes.push(root);
				root = root->left;
			}

			if (pre) {
				finalMinDiff = min(finalMinDiff, abs(pre->data - pendingNodes.top()->data));
			}
			pre = pendingNodes.top();
			pendingNodes.pop();

			root = pre->right;
		}
		return finalMinDiff;
	}
};
