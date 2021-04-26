https://leetcode.com/problems/longest-zigzag-path-in-a-binary-tree/

``` cpp
#define getPair pair<int,pair<int,int>>
#define maxLen first
#define forwardSlope second.first
#define backwardSlope second.second
class Solution {
	getPair helper(TreeNode *root){
		if(!root){
			getPair res;
			res.maxLen =-1;
			res.forwardSlope =-1;
			res.backwardSlope =-1;
			return res;
		}

		getPair leftAns = helper(root->left);
		getPair rightAns = helper(root->right);

		getPair res;
		res.maxLen = max(max(leftAns.maxLen,rightAns.maxLen),max(leftAns.backwardSlope,rightAns.forwardSlope)+1);
		res.forwardSlope = leftAns.backwardSlope+1;
		res.backwardSlope = rightAns.forwardSlope+1;

		return res;
	}
public:
    int longestZigZag(TreeNode* root) {
    	return helper(root).maxLen;
    }
};
