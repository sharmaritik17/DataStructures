

https://leetcode.com/problems/range-sum-of-bst/

``` cpp

#define data val
class Solution {
public:
	int rangeSumBST(TreeNode* root, int L, int R) {
		if (!root)
			return 0;

		int sum = 0;
		if (root->data >= L && root->data <= R) {
			sum += root->data;
		}
		else if (root->data < L)
			return rangeSumBST(root->right, L, R);
		else if (root->data > R)
			return rangeSumBST(root->left, L, R);

		sum += rangeSumBST(root->left, L, R);
		sum += rangeSumBST(root->right, L, R);

		return sum;
	}
};

#define data val
#include<stack>
class Solution {
public:
	int rangeSumBST(TreeNode* root, int L, int R) {
		if (!root)
			return 0;

		int sum = 0;
		stack<TreeNode*> pendingNodes;
		pendingNodes.push(root);
		while (pendingNodes.size()) {
			TreeNode *top = pendingNodes.top();
			pendingNodes.pop();

			if (!top)
				continue;

			if (top->data >= L && top->data <= R) {
				sum += top->data;
			}
			if (top->data > L) {
				pendingNodes.push(top->left);
			}
			if (top->data < R) {
				pendingNodes.push(top->right);
			}
		}
		return sum;
	}
};
