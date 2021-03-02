``` cpp
https://leetcode.com/problems/linked-list-in-binary-tree/

approach 1:-

#define data val
class Solution {
    bool checkIfPathExists(ListNode *head, TreeNode* root) {
        if (!head)
            return 1;
        if (!root) {
            return 0;
        }
        if (head->data != root->data) {
            return false;
        }
        if (!(checkIfPathExists(head->next, root->left)) && !(checkIfPathExists(head->next, root->right))) {
            return false;
        }
        return true;
    }
public:
    bool isSubPath(ListNode* head, TreeNode* root) {
        if (!head)
            return 1;
        if (!root) {
            return 0;
        }  

        bool finalAns = checkIfPathExists(head, root) || isSubPath(head, root->left) || isSubPath(head, root->right);

        return finalAns;
    }
};

approach 2:-
by using KMP ----- IMPORTANT 
https://leetcode.com/problems/linked-list-in-binary-tree/discuss/535370/Java-KMP-Search-O(m%2Bn)-Clean-code
