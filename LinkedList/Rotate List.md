``` cpp
https://leetcode.com/problems/rotate-list/


https://leetcode.com/problems/rotate-list/discuss/1050591/Two-Pointer-or-Easy-Buzzy-or-Intuitive

APPROACH :-Maintain two pointers FAST and SLOW

TC -- O(Length of List)
SC -- O(1)

#define nul     NULL
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        if (!head || k == 0) {
            return head;
        }

        ListNode* orgHead = nul, *slow = head, *fast = head;
        int count = 0;
        int len = 0;
        while (count < k) {
            if (fast) {
                fast = fast->next;
                len++;
                count++;
            }
            else {
                count = 0;
                fast = head;
                k = k % len;
            }
        }

        if(!fast){
            return head;
        }

        while (slow && fast->next) {
            slow = slow->next;
            fast = fast->next;
        }
        fast->next = head;
        orgHead = slow->next;
        slow->next = nul;

        return orgHead;
    }
};
