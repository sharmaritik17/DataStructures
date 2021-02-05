``` cpp
https://leetcode.com/problems/palindrome-linked-list/

#define data val
class Solution {
public:
    ListNode* reverseList(ListNode *head) {
        if (head == NULL || head->next == NULL) return head;
        ListNode *ptr = reverseList(head->next);
        head->next->next = head;
        head->next = NULL;
        return ptr;
    }

    bool isPalindrome(ListNode* head) {
        ListNode *slow = head, *fast = head;
        while (fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
        }
        slow = reverseList(slow);
        while (slow != NULL) {
            if (slow->val != head->val) return false;
            slow = slow->next;
            head = head->next;
        }
        return true;
    }
};
