``` cpp

https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/

https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/discuss/960995/Straight-Forward-or-Maths-Only-or-Intuitive

class Solution {
private:
	TreeNode* buildTreeHelp(vector<int>& preorder, vector<int>& inorder, int inS, int inE, int preS, int preE) {
		if (preE < preS || inE < inS)
			return NULL;

		int rootData = preorder[preS];
		int rootIndex = -1;
		for (int i = inS; i <= inE; i++) {
			if (rootData == inorder[i]) {
				rootIndex = i;
				break;
			}
		}
        //USE MATHEMATICS ONLY
		int LinS = inS; 
		int LinE = rootIndex - 1;
		int LpreS = preS + 1;
		int LpreE = LinE - LinS + LpreS;
		int RpreS = LpreE + 1;
		int RpreE = preE;
		int RinS = rootIndex + 1;
		int RinE = inE;


		TreeNode *root = new TreeNode(rootData);
		root->left = buildTreeHelp(preorder, inorder, LinS, LinE, LpreS, LpreE);
		root->right = buildTreeHelp(preorder, inorder, RinS, RinE, RpreS, RpreE);

		return root;
	}

public:
	TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
		int n = preorder.size();
		if (n != inorder.size())
			return NULL;

		return buildTreeHelp(preorder, inorder, 0, n - 1, 0, n - 1);
	}
};

//iterative
class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        int m = inorder.size();
        int n = preorder.size();
        if(!m || m!=n){
            return NULL;
        }
        unordered_map<int, int> mp;
        for(int i = 0;i<m;i++){
            mp[inorder[i]] = i;
        }
        TreeNode *root = new TreeNode(preorder[0]);
        stack<TreeNode *> st;
        st.push(root);
        for(int i = 1; i<n; i++){
            TreeNode *node = new TreeNode(preorder[i]);
            if(st.size() && mp[node->val] < mp[st.top()->val]){
                st.top()->left = node;
            }
            else{
                TreeNode *parent;
                while(st.size() && mp[st.top()->val] < mp[node->val]){
                    parent = st.top();
                    st.pop();
                }
                if(parent){
                    parent->right = node;
                }
            }
            st.push(node);
        }
        return root;
    }
};
