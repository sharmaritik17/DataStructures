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



Node *reverseLinkedListRec(Node *head) {
    // Write your code here
    if(!head || !head->next){
        return head;
    }


    Node *smallAns = reverseLinkedListRec(head->next);

    head->next->next = head;
    head->next = NULL;
    
    /*
    Node *tail = head->next;
    tail->next = head;
    
    head->next = NULL;
    */

    return smallAns;
}



Node *reverseLinkedList(Node *head) {
    // Write your code here
    if(!head)
        return head;
    
    Node *curr = head;
    Node *prev = NULL;
    Node *nextNode = NULL;
    
    while(curr){
        nextNode = curr->next;
        curr->next = prev;
        prev = curr;
        curr = nextNode;
    }
    return prev;
}
