https://leetcode.com/problems/reorder-list/


``` cpp

#define nul     NULL
class Solution {
    ListNode* reverse(ListNode *head) {
        if (!head) {
            return {};
        }
        ListNode *nextNode = nul, *prev = nul, *curr = head;
        while (curr) {
            nextNode = curr->next;
            curr->next = prev;
            prev = curr;
            curr = nextNode;
        }
        return prev;
    }

public:
    void reorderList(ListNode* head) {
        if (!head) {
            return;
        }

        ListNode *slow = head, *fast = head->next;

        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
        }


        ListNode *newHead = reverse(slow->next);
        slow->next = nul;


        ListNode *t1 = nul, *t2 = nul;
        while (head && newHead) {
            t1 = head->next;
            t2 = newHead->next;
            newHead->next = head->next;
            head->next = newHead;
            head = t1;
            newHead = t2;
        }

    }
};





#define nul     NULL
class Solution {
public:
    void reorderList(ListNode* head) {
        if (!head) {
            return;
        }

        ListNode *slow = head, *fast = head, *curr = head, *prev = nul;

        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
        }

        stack<ListNode*> backup;

        while (slow) {
            backup.push(slow);
            slow = slow->next;
        }

        //now we need to make whole list

        while (!backup.empty()) {
            ListNode *top = backup.top();
            backup.pop();
            // this case would occur only for odd number of elements 
            if (curr == top) {
                break;
            }
            prev = curr->next;
            curr->next = top;
            top->next = prev;
            curr = prev;
        }
        curr->next = nul;

    }
};
