``` cpp
add two numbers   
https://practice.geeksforgeeks.org/problems/add-two-numbers-represented-by-linked-lists/1
/* ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------*/
#define nul     NULL
class Solution {
public:
	ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
		int digit = 0;
		int carry = 0;
		ListNode *tail = nul;
		ListNode *newhead = nul;
		int l1_val = 0;
		int l2_val = 0;
		while (l1 || l2) {
			l1_val = l1 != nul ? l1->val : 0;
			l2_val = l2 != nul ? l2->val : 0;
			digit = l1_val + l2_val + carry;
			carry = digit / 10;
			digit = digit % 10;
			if (!tail) {
				ListNode *nextDigit = new ListNode(digit);
				nextDigit->next = tail;
				tail = nextDigit;
				newhead = nextDigit;
			}
			else {
				ListNode *nextDigit = new ListNode(digit);
				tail->next = nextDigit;
				tail = nextDigit;
			}
			if (l1)
				l1 = l1->next;
			if (l2)
				l2 = l2->next;
		}
		if (carry) {
			ListNode *nextDigit = new ListNode(carry);
			tail->next = nextDigit;
			tail = nextDigit;
		}
		return newhead;
	}
};
