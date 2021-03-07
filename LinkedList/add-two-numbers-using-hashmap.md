``` cpp
## 445 leetcode
by using hashmap
/* -----------------------------------------------------------------------*/
class linkedlistExtended {
public:
	unordered_map<ListNode*, ListNode*> _prev;
	ListNode *_tail=NULL;
	linkedlistExtended(ListNode *head) const {
		while (head != nul) {
			_prev[head] = _tail;
			_tail = head;
			head = head->next;
		}
	}

	ListNode get_prev(ListNode *curr) const {
		return _prev[curr];
	}

	ListNode get_value(ListNode *curr) const {
		return curr ? curr->val : 0;

	}

	ListNode get_tail(ListNode *curr) const {
		return _tail;
	}

};

class Solution {
public:
	ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
		linkedlistExtended A(l1), B(l2);

		ListNode *f = A.get_tail();
		ListNode *s = B.get_tail();

		int carry = 0;
		int digit = 0;
		ListNode *res = NULL;

		while (f || s) {
			digit  = A.get_value(f) + B.get_value(s) + carry;
			carry = digit / 10;
			digit = digit % 10;

			ListNode *nextDigit = new ListNode(digit);
			nextDigit->next = res;
			res = nextDigit;

			f = A.get_prev(f);
			s = B.get_prev(s);
		}

		if (carry) {
			ListNode *nextDigit = new ListNode(1);
			nextDigit->next = res;
			res = nextDigit;
		}
		return res;
	}
};
