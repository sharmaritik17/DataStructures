``` cpp

// intersecting point in LL
/*-----------------------------------------------------------------------*/
class Solution {
public:
	ListNode *getIntersectionNode(ListNode *head1, ListNode *head2) {
		if (!head1 || !head2)
			return !head1;

		ListNode a = head1->next;
		ListNode b = head2->next;

		while (a != b) {
			a = a == nul ? head2 : a->next;
			b = b == nul ? head1 : b->next;
		}

		return a; // or b both r same
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
