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