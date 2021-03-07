https://leetcode.com/problems/swapping-nodes-in-a-linked-list/
``` cpp
class Solution {
public:
    ListNode* swapNodes(ListNode* head, int n) {
        if(!head){
            return {};
        }

        ListNode *slow =head,*fast=head,*save=NULL;
        
        for(int i=1;i<n;i++){
            fast = fast->next;
        }

        save = fast;

        while(fast->next){
            slow =slow->next;
            fast = fast->next;
        }

        swap(save->val,slow->val);

        return head;
    }
};

```
