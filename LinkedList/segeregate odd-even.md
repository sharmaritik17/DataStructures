``` cpp
https://leetcode.com/problems/odd-even-linked-list/
/*------------------------------------------------------------------------------------------------------------------------------------------------------------------------------*/
#define nul     NULL
Node *reverse(Node *head) {
	if (!head)
		return head;

	Node *nextNode = nul;
	Node *prev = nul;
	Node *curr = head;

	while (curr) {
		nextNode = curr->next;
		curr->next = prev;
		prev = curr;
		curr = nextNode;
	}

	return prev;
}
void rearrange(struct Node *head)
{
	if (!head)
		return head;

	Node *odd = head;
	Node *even = head->next;
	Node *evenHead = even;

	while (even && even->next) {
		odd->next = even->next;
		odd = odd->next;

		even->next = odd->next;
		even = even->next;
	}

	evenHead = reverse(evenHead);

	odd->next = evenHead;

}




LEETCODE PROBLEM --- SOLUTION

class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        if (!head || !head->next)
            return head;

        ListNode *odd = head, *even = head->next , *evenHead = even;

        while (even && even->next) {
            odd->next = odd->next->next;
            even->next = even->next->next;    // THIS WILL PUT AUTOMATICALLY NULL(WHEN LENGTH OF LL IS ODD)
            odd = odd->next;
            even = even->next;
        }
        odd->next = evenHead;

        return head;
    }
};
