``` cpp
// add polynomials
Node* addPolynomial(Node *p1, Node *p2)
{
	//Your code here
	Node *head = new Node(0, 0);
	Node *tail = head;
	while (p1 && p2)
	{
		if (p1->pow > p2->pow)
		{
			tail->next = p1;
			tail = p1;
			p1 = p1->next;
		} else if (p1->pow < p2->pow)
		{
			tail->next = p2;
			tail = p2;
			p2 = p2->next;
		}
		else {
			p1->coeff += p2->coeff;
			tail->next = p1;
			tail = p1;
			p1 = p1->next;
			p2 = p2->next;
		}
	}
	while (p1)
	{
		tail->next = p1;
		tail = p1;
		p1 = p1->next;
	}
	while (p2)
	{
		tail->next = p2;
		tail = p2;
		p2 = p2->next;
	}

	return head->next;
}
