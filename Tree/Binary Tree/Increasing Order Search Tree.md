``` cpp

https://leetcode.com/problems/increasing-order-search-tree/ 

//recursive
class Solution {
	void increasingBSTHelper(TreeNode *root, TreeNode *&curr) {
		if (!root)
			return;

		increasingBSTHelper(root->left, curr);
		root->left = NULL;
		curr->right = root;
		curr = root;
		increasingBSTHelper(root->right, curr);
	}
public:
	TreeNode* increasingBST(TreeNode* root) {
		if (!root)
			return root;

		TreeNode *dummy = new TreeNode(0);
		TreeNode *curr = dummy;
		increasingBSTHelper(root, curr);
		return dummy->right;
	}
};


//iterative
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
