https://leetcode.com/problems/minimum-depth-of-binary-tree/
``` cpp


class Solution {
public:
	int minDepth(TreeNode* root) {
		if (!root)
			return 0;

		int leftAns = minDepth(root->left);
		int rightAns = minDepth(root->right);

		return 1 + (min(leftAns, rightAns) ? min(leftAns, rightAns) : max(leftAns, rightAns));

		// return 1 + (leftAns && rightAns ? min(leftAns, rightAns) : max(leftAns, rightAns));
	}
};

class Solution {
public:
	int minDepth(TreeNode* root) {
		if (!root)
			return 0;

		int height = 0;
		queue<TreeNode*> pendingNodes;
		pendingNodes.push(root);

		while (pendingNodes.size()) {
			height++;

			int size = pendingNodes.size();
			for (int i = 0; i < size; i++) {
                         TreeNode *front = pendingNodes.front();
				if (front->left) {
					pendingNodes.push(front->left);
				}
				if (front->right) {
					pendingNodes.push(front->right);
				}

				if (!front->left && !front->right)
					return height;

				pendingNodes.pop();
			}
		}
		return -1;
	}
};
