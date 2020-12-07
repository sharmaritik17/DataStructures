``` cpp

#define data val
#define ll long long
class Solution {
    public:
    
 bool isValidBST(TreeNode *root) {
        // use long min and long max if the value in tree is int
        return isValidBSTRec(root, LONG_MIN, LONG_MAX);
    }
    
    bool isValidBSTRec(TreeNode* root, long min, long max) {
        if (root == NULL) {
            return true;
        }
        
        if (root->val <= min || root->val >= max) {
            return false;
        }
        
        bool left = isValidBSTRec(root->left, min, root->val);
        if (left == true) {
            return isValidBSTRec(root->right, root->val, max);
        }
        return false;
    }
};

//ITERATIVE 
class Solution {
public:
	bool isValidBST(TreeNode *root) {
		if (!root)
			return 0;

		TreeNode *pre = NULL;
		stack<TreeNode*> pendingNodes;

		while (root || pendingNodes.size()) {
			while (root) {
				pendingNodes.push(root);
				root = root->left;
			}

			TreeNode *front = pendingNodes.top();
			pendingNodes.pop();

			if (pre != NULL && front->data <= pre->data)
				return false;

			pre = front;
			root = front->right;
		}
        
        return true;
	}

};
