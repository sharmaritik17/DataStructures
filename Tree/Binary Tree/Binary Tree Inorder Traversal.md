
https://leetcode.com/problems/binary-tree-inorder-traversal/

``` cpp

class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        TreeNode *save = NULL;

        while(root){

        	if(root->left){
        		save = root->left;
        		while(save->right){
        			save = save->right;
        		}
        		save->right = root;
        		save = root->left;
        		root->left = NULL;
        		root = save;
        	}
        	else{
        		result.push_back(root->val);
        		root = root->right;
        	}
        	
        }
        return result;
    }
};
