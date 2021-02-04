``` cpp

https://leetcode.com/problems/sort-list/

TC --  O(nlogn) Sc -- O(1)
#define data val
#define j NULL
class Solution {
    ListNode* split(ListNode *head, int n) {
        for (int i = 1; i < n && head; i++) {
            head = head->next;
        }
        if (!head)
            return head;
        ListNode *sec = head->next;
        head->next = NULL;
        return sec;
    }

    ListNode* merge(ListNode* l1, ListNode*l2, ListNode* head) {
        ListNode *curr = head;
        while (l1 && l2) {
            if (l1->data < l2->data) {
                curr->next = l1;
                curr = l1;
                l1 = l1->next;
            }
            else {
                curr->next = l2;
                curr = l2;
                l2 = l2->next;
            }
        }
        curr->next = (l1 ? l1 : l2);
        while (curr->next) {
            curr = curr->next;
        }
        return curr;
    }
    int length(ListNode *head) {
        if (!head)
            return 0;
        return 1 + length(head->next);
    }
public:
    ListNode *sortList(ListNode *head) {
        if (!head || !head->next)
            return head;
        int len = length(head);

        ListNode *curr = head, *tail = j, *left = j, *right = j, dummy = 0;
        dummy.next = head;

        for (int step = 1; step < len; step *= 2) {
            curr = dummy.next;
            tail = &dummy;
            while (curr) {
                left = curr;
                right = split(left, step);
                curr = split(right, step);
                tail = merge(left, right, tail);
            }
        }
        return dummy.next;
    }
};
