``` cpp

https://leetcode.com/problems/swap-nodes-in-pairs/



class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if(!head || !head->next)
            return head;

        ListNode *save = head->next;
        head->next = swapPairs(save->next);
        save->next = head;

        return save;
    }
};


class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* ohead = head;
        ListNode* last = NULL;
        while (head && head->next) {
            ListNode* tmp = head->next;
            head->next = tmp->next;
            tmp->next = head;

            if (last) {
                last->next = tmp;
            } else {
                ohead = tmp;
            }
            last = head;
            head = head->next;

        }

        return ohead;
    }
};
