https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/
``` cpp
#define data val
class Solution {
public:
    TreeNode* bstFromPreorder(vector<int>& preorder) {
    	TreeNode *root = new TreeNode(preorder[0]);
    	TreeNode *parent = root;
    	int size = preorder.size();

    	for(int i=1;i<size;i++){
    		TreeNode *child = new TreeNode(preorder[i]);
    		if(parent->data > child->data){
    			parent->left = child;
    			child->right = parent; //morris link to parent
    		}
    		else{
    			while(parent->right && parent->right->data < child->data){
    				auto temp = parent;
    				parent = parent->right; //uplift to upper parent
    				temp->right = NULL; // breaking morris parent-child link
    			}
    			child->right = parent->right; //morris link to parent where it's parent previously pointing to.
    			parent->right = child;  //child linked here to it's parent to right
    		}
    		parent = child;
    	}

    	while(parent->right){
    		auto temp = parent->right;
    		parent->right = NULL; // unlink parent-child morris link that we did unusually.
    		parent = temp;
    	}

    	return root;
    }
};
```

``` cpp
class Solution {
public:
    TreeNode* bstFromPreorder(vector<int>& preorder) {
        TreeNode dummy_root(INT_MAX);
        stack<TreeNode *> s({&dummy_root});
        for (int x : preorder) {
            auto n = new TreeNode(x);
            TreeNode *p = nullptr;
            while (s.top()->val < x) {
                p = s.top();
                s.pop();
            }
            if (p) {
                p->right = n;
            } else {
                s.top()->left = n;
            }
            s.push(n);
        }
        return dummy_root.left;
    }
};
```
