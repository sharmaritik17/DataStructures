``` cpp
/*=======================================================================================================*/
class Node {
public:
    int data;
    Node *next;

    Node(int data): data(data) {
        //this->data = data;
        next = nul;
    }
};

/*=======================================================================================================*/
//delete node at particular postion in circular linked list
Node* deleteNode(Node *head, int pos) {
	if (!head)
		return nul;

	if (pos == 0) {
		Node *remove = head;
		Node *temp = head;
		Node *newhead = head->next;
		while (temp->next != head) {
			temp = temp->next;
		}
		temp->next = newhead;
		delete(remove);
		return newhead;
	}

	int count = 0;
	Node *temp = head;
	while (count < pos - 1 && temp->next != head) {
		count++;
		temp = temp->next;
	}

	if (temp != head && temp->next != head) {
		Node* remove = temp->next;
		temp->next = temp->next->next;
		delete(remove);
	}

	if (temp != head && temp->next == head) {
		Node* remove = temp;
		temp = head;
		delete(remove);
	}

	return head;
}
/* -----------------------------------------------------------------------*/
//insert node at particular postion in circular linked list
Node* insertNode(Node *head, int pos, int data) {
	if (!head)
		return nul;

	Node *newNode = new Node(data);

	if (pos == 0) {
		Node *temp = head->next;
		while (temp->next != head) {
			temp = temp->next;
		}
		temp->next = newNode;
		newNode->next = head;
		return newNode;
	}
	int count = 0;
	Node *temp = head->next;
	while (count < pos - 1 && temp != head) {
		count++;
		temp = temp->next;
	}

	if (temp != head) {
		newNode->next = temp->next;
		temp->next = newNode;
	}
	if (temp != head && temp->next == head) {
		temp->next = newNode;
		newNode->next = head; //temp->next;
	}
	return head;
}
/* -----------------------------------------------------------------------*/
//take input of circular linked list
Node* takeinput() {
	int data;
	cin >> data;

	Node *head = nul;
	Node *tail = nul;

	while (data != -1) {
		Node *newNode = new Node(data);
		if (head == nul) {
			head = newNode;
			newNode->next = head;
			tail = newNode;
		}
		else {
			tail->next = newNode;
			newNode->next = head;     //cirular linked list
			tail = newNode;
		}
		cin >> data;
	}
	return head;
}

/* -----------------------------------------------------------------------*/
void print(Node const  *head)   {
	if (!head)
		return;

	cout << head->data << " ";
	Node const *temp = head->next;
	while (temp != head) {
		cout << temp->data << " ";
		temp = temp->next;
	}
}
/* -----------------------------------------------------------------------*/
int main() {
	/*||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||*/
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
	/*||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||*/

	Node *head = takeinput();
	print(head);
	cout << "\n";
	int i, data;
	cin >> i;// >> data;
	head = deleteNode(head, i);
	print(head);

}
