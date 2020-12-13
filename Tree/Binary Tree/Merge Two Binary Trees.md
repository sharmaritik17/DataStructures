``` cpp

https://leetcode.com/problems/merge-two-binary-trees/

#define getPair pair<TreeNode*,TreeNode*>
#define  f  first
#define  s  second
#define data val
class Solution {
public:
	TreeNode* mergeTrees(TreeNode* t1, TreeNode* t2) {
		if (!t1)
			return t2;
		if (!t2)
			return t1;

		stack<getPair> pendingNodes;
		pendingNodes.push(make_pair(t1,t2));

		while (pendingNodes.size()) {
			getPair top = pendingNodes.top();
			pendingNodes.pop();

			TreeNode *first = top.f;
			TreeNode *second = top.s;

			if (!second) {
				continue;
			}
			first->data += second->data;
			if (!first->left) {
				first->left = second->left;
			}
			else {
				pendingNodes.push(make_pair(first->left, second->left));
			}

			if (!first->right) {
				first->right = second->right;
			}
			else {
				pendingNodes.push(make_pair(first->right, second->right));
			}
		}

		return t1;
	}
};
