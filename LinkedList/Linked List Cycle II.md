https://leetcode.com/problems/linked-list-cycle/

https://leetcode.com/problems/linked-list-cycle-ii/

https://leetcode.com/problems/linked-list-cycle-ii/discuss/1101113/Different-Approach-than-Solution-or-Count-Nodes-in-Cycle

``` cpp
class Solution {
    ListNode *omitNodes(ListNode *slow, ListNode *fast , int count) {
        for (int i = 0; i < count; i++) {
            fast = fast->next;
        }

        while (fast != slow) {
            slow = slow->next;
            fast = fast->next;
        }
        return slow;
    }
    int countNodesInCycle(ListNode *head, ListNode *&save) {
        int count = 1;
        head = head->next;
        while (head != save) {
            head = head->next;
            count++;
        }
        return count;
    }
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode *slow = head;
        ListNode *fast = head;
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {
                int count = countNodesInCycle(slow, slow);
                return omitNodes(head, head, count);
            }
        }
        return {};
    }
};
