https://leetcode.com/problems/deepest-leaves-sum/

https://leetcode.com/problems/deepest-leaves-sum/discuss/1164807/O(1)-space-O(n)-time-Morris-traversal

``` cpp

#define data val
class Solution {
	void deepestLeavesSumHelper(TreeNode *root, int &sum, int level, int &prevLevel) {
		if (!root)
			return;

		if (level > prevLevel) {
			sum = 0;
			prevLevel = level;
		}

		if (level == prevLevel) {
			sum += root->data;
		}

		deepestLeavesSumHelper(root->left, sum, level + 1, prevLevel);
		deepestLeavesSumHelper(root->right, sum, level + 1, prevLevel);
	}
public:
	int deepestLeavesSum(TreeNode* root) {
		if (!root)
			return 0;

		int sum = 0;
		int prevLevel = 0;
		deepestLeavesSumHelper(root, sum, 0, prevLevel);
		return sum;
	}
};


//iteratively
#define data val
class Solution {
public:
	int deepestLeavesSum(TreeNode* root) {
		if (!root)
			return 0;

		int res = 0;
		queue<TreeNode*> pendingNodes;
		pendingNodes.push(root);
		while (pendingNodes.size()) {
			res = 0;
			for (int i = pendingNodes.size() - 1; i >= 0; i--) {
				TreeNode *front = pendingNodes.front();
				pendingNodes.pop();

				res += front->data;

				if (front->left)
					pendingNodes.push(front->left);
				if (front->right)
					pendingNodes.push(front->right);
			}
		}
		return res;
	}
};
