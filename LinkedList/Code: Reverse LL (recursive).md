``` cpp

#define nul     NULL
class Pair {
public:
    Node *head = nul;
    Node *tail = nul;
};

Pair reverseLinkedList_helper(Node *head) {
    if (!head || !head->next) {
        Pair ans;
        ans.head = head;
        ans.tail = head;
        return ans;
    }

    Pair smallAns = reverseLinkedList_helper(head->next);
    smallAns.tail->next = head;
    head->next = nul;

    Pair ans;
    ans.head = smallAns.head;
    ans.tail = head;

    return ans;
}
Node *reverseLinkedList(Node *head) {
    // Write your code here
    reverseLinkedList_helper(head).head;
}
