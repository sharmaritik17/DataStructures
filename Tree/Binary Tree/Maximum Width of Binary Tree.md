https://leetcode.com/problems/maximum-width-of-binary-tree/

https://leetcode.com/problems/maximum-width-of-binary-tree/discuss/1184525/C%2B%2B-BFS-or-With-INT-Only


//overflow
``` cpp
class Solution {
private:
    int maxVal = 0;
    unordered_map<int,int> levelLeft;
public:
    int widthOfBinaryTree(TreeNode* root) {
        dfs(root, 0, 0);
        return maxVal;
    }

    void dfs(TreeNode* root, int depth, int pos) 
    {
        if (root == NULL) 
            return;
        
        if (levelLeft.find(depth)==levelLeft.end())
           levelLeft[depth]=pos;
        
        maxVal = max(maxVal, pos - levelLeft[depth] + 1);
        
        dfs(root->left, depth + 1, 2 * pos + 1); //make sure all left explored first using dfs
        dfs(root->right, depth + 1, 2 * pos + 2);
    }
};
