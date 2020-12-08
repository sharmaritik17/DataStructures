``` cpp
#define data val
#define rl root->left
#define rr root->right
#define pd p->data
#define qd q->data
#define rd root->data

class Solution {
public:
	TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
		if (!root || !p || !q || rd == pd || rd == qd)
			return root;

		if (rd > pd && rd > qd)
			return lowestCommonAncestor(rl, p, q);
		else if (rd < pd && rd < qd)
			return lowestCommonAncestor(rr, p, q);

		TreeNode *leftAns = lowestCommonAncestor(rl, p, q);
		TreeNode *rightAns = lowestCommonAncestor(rr, p, q);

		if (leftAns && rightAns)
			return root;
		else if (leftAns)
			return leftAns;
		else
			return rightAns;
	}
};


#define data val
#define rl root->left
#define rr root->right
#define pd p->data
#define qd q->data
#define rd root->data

class Solution {
public:
	TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
		if (!root || !p || !q || rd == pd || rd == qd)
			return root;

		if (rd > pd && rd > qd)
			return lowestCommonAncestor(rl, p, q);
		else if (rd < pd && rd < qd)
			return lowestCommonAncestor(rr, p, q);
		else
			return root;
	}
};

// iteratively

#define data val
#define rl root->left
#define rr root->right
#define pd p->data
#define qd q->data
#define rd root->data

class Solution {
public:
	TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
		TreeNode *curr = root;
		while (1) {
			if (rd > pd && rd > qd)
				curr = curr->left;
			else if (rd < pd && rd < qd)
				curr = curr->right;
			else
				break;
		}

		return curr;
	}
};
