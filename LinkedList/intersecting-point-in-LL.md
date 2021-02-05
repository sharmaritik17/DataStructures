``` cpp
https://leetcode.com/problems/intersection-of-two-linked-lists/
// intersecting point in LL
/*-----------------------------------------------------------------------*/
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *p1, ListNode *p2) {
        if (!p1 || !p2)
            return {};

        ListNode *a = p1, *b = p2;

        while (a != b) {
            a = a ? a->next : p2 ;
            b = b ? b->next : p1 ;
        }
        return a;
    }
};


class Solution {
public:
    ListNode *getIntersectionNode(ListNode *p1, ListNode *p2) {
        ListNode *headA = p1, *headB = p2;
        if (!headA || !headB)
            return {};

        int lenA = 0;
        int lenB = 0;
        while (headA || headB) {
            if (headA) {
                lenA++;
                headA = headA->next;
            }
            if (headB) {
                lenB++;
                headB = headB->next;
            }
        }

        headA = p1, headB = p2;
        
        if (lenA < lenB) {
            int diff = lenB - lenA;
            for (int i = 0; i < diff; i++) {
                headB = headB->next;
            }
        }
        else {
            int diff = lenA - lenB;
            for (int i = 0; i < diff; i++) {
                headA = headA->next;
            }
        }

        while (headB != headA) {
            headB = headB->next;
            headA = headA->next;
        }

        return headB;
    }
};
