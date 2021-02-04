``` cpp
#define nul     NULL
class Solution {
    int length(ListNode *head) {
        if (!head)
            return 0;

        return 1 + length(head->next);
    }
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        if (k == 0 || k == 1 || length(head) < k || !head) {
            return head;
        }

        int count = 0;
        ListNode *curr = head, *prev = nul;
        while (curr && count < k) {
            ListNode *nextNode = curr->next;
            curr->next = prev;
            prev = curr;
            curr = nextNode;
            count++;
        }

        if (curr) {
            head->next = reverseKGroup(curr, k);
        }

        return prev;
    }
};

/*-----------------------------------------------------------------------*/ leads to same/below solution 
Node* reverseKGroup(Node* head, int k) {
	if (!head || !k)
		return head;
	Node *dummy = new Node(0);
	dummy->next = head;
	int length = 0;
	Node *curr = head;
	while (curr) {
		curr = curr->next;
		length++;
	}

	curr = head;
	Node *prev = nul;
	Node *nextNode = nul;
	while (length >= k) {
		for (int i = 0; i < k - 1; i++) {
			nextNode = curr->next;
			curr->next = prev;
			prev = curr;
			curr = nextNode;
		}
		prev = curr;
		curr = curr->next;
		length -= k;
	}
	return dummy->next;
}
/*-----------------------------------------------------------------------*/   my-solution
class Solution {
public:
	ListNode* reverseKGroup(ListNode* head, int k) {
		if (!head)
			return head;
		if (k == 0 || k == 1)
			return head;

		ListNode *dummy = new ListNode(0);
		dummy->next = head;
		ListNode *pre = dummy;
		int len = 0;
		ListNode *let = head;
		while (let) {
			len++;
			let = let->next;
		}

		for (int i = 0; i < len / k; i++) {
			for (int j = 0; j < k - 1; j++) { // basically LL given is 1 based
				// and so we starting from 0 to =k-2 you may use 1 to =k-1
				ListNode *temp  = pre->next;
				pre->next = head->next;
				head->next = head->next->next;
				pre->next->next = temp;
			}
			pre = head;
			head = head->next;
		}
		ListNode *save = dummy->next;
		delete(dummy);
		return save;
	}
};
/*++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*/  author-solution
class Solution {
public:
	ListNode* reverseKGroup(ListNode* head, int k) {
		dummy -> next = head;
		int len = length(head);
		for (int i = 0; i < len / k; i++) {
			for (int j = 1; j < k; j++) {
				ListNode* temp = pre -> next;
				pre -> next = head -> next;
				head -> next = head -> next -> next;
				pre -> next -> next = temp;
			}
			pre = head;
			head = head -> next;
		}
		return dummy -> next;
	}
private:
	ListNode *dummy = new ListNode(0), *pre = dummy;
	int length(ListNode* head) {
		int len = 0;
		while (head) {
			len++;
			head = head -> next;
		}
		return len;
	}
};
