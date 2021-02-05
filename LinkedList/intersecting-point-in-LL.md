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
