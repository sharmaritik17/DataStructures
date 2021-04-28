https://leetcode.com/problems/house-robber-iii/



https://leetcode.com/problems/house-robber-iii/discuss/1180579/Runtime%3A-8-ms-faster-than-96.18-or-C%2B%2B

``` cpp
//recursion
class Solution {
public:
    int rob(TreeNode* root) {
        if(!root)
        	return 0;

        int sum =0;
        if(root->left){
        	sum += rob(root->left->left) + rob(root->left->right);
        }
        if(root->right){
        	sum += rob(root->right->left) + rob(root->right->right);
        }

        return max((root->val + sum),rob(root->left) + rob(root->right));
    }
};

// memoization
class Solution {
unordered_map<TreeNode *,int> map;
public:
    int rob(TreeNode* root) 
    {
        if(!root)
            return 0;
        if(map.count(root))
            return map[root];
        int total=0;
        if(root->left)
            total+= rob(root->left->left)+rob(root->left->right);
        if(root->right)
            total+=rob(root->right->left)+rob(root->right->right);
        
        return map[root]=max(root->val+total,rob(root->left)+rob(root->right));
        
    }
};
