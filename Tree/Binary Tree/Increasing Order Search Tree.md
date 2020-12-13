``` cpp

https://leetcode.com/problems/increasing-order-search-tree/ 

class Solution {
public:
	TreeNode* increasingBST(TreeNode* root) {
		if (!root)
			return root;

		stack<TreeNode*> pendingNodes;
		TreeNode *saveReturn = new TreeNode(0);
		TreeNode *pre = saveReturn;

		while (root || pendingNodes.size()) {
			while (root) {
				pendingNodes.push(root);
				root = root->left;
			}

			TreeNode *top = pendingNodes.top();
			pendingNodes.pop();

			pre->right = top;
			pre = pre->right;
			top->left = NULL;
			root = top->right;
		}
		return saveReturn->right;
	}
};
