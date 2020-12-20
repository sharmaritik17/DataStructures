https://leetcode.com/problems/pseudo-palindromic-paths-in-a-binary-tree/



``` cpp
#define data val
class Solution {
public:
	int pseudoPalindromicPaths (TreeNode* root, int count = 0) {
		if (!root)
			return 0;

		count ^= (1 << (root->data));
		int res = pseudoPalindromicPaths(root->left, count) + pseudoPalindromicPaths(root->right, count);
		if (!root->left && !root->right && (count & (count - 1)) == 0) // (count & (count - 1)) == 0 to check if count is exact power of 2 or not(so that it ahving only 1 bit up)
			res++;
        
		return res;
	}
};
