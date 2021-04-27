https://leetcode.com/problems/even-odd-tree/

https://leetcode.com/problems/even-odd-tree/discuss/1179640/C%2B%2B-BFS-or-Level-Wise



``` cpp
#define data val
class Solution {
    	unordered_map<int,int> map;
    	
    	bool isEvenOddTree(TreeNode *root,int currLevel){
    		if(!root){
    			return 1;
    		}

    		if(currLevel & 1){
    			if(root->data & 1){
    				return 0;
    			}
    		}
    		else if(!(root->data & 1)) return 0;

    		if(map.count(currLevel)){
    			if(currLevel & 1){
    				if(map[currLevel]<=root->data) return 0;
    			}
    			else if(map[currLevel]>=root->data) return 0;
    		}

    		map[currLevel] = root->data;

    		return isEvenOddTree(root->left,currLevel+1) && isEvenOddTree(root->right,currLevel+1);
    	}

public:
    bool isEvenOddTree(TreeNode* root) {
    	return isEvenOddTree(root,0);
    }
};
