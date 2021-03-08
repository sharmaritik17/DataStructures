https://leetcode.com/problems/add-two-numbers-ii/
``` cpp
// can be done using stacks/hashmap/recursion/reversing only/iterative only(first finding length)

int llLen(ListNode* node) {
    int c = 0;
    while (node) {
        ++c;
        node = node->next;
    }
    return c;
}

int addTwoList(ListNode* longer, ListNode* shorter, int nDiff) {
    if (longer == nullptr)         // both should be at null simultaneously
        return 0;
    int _sum = 0;
    if (nDiff) {
        int ret = addTwoList(longer->next, shorter, nDiff - 1);
        _sum = longer->val + ret;
    }
    else {
        int ret = addTwoList(longer->next, shorter->next, nDiff);
        _sum = longer->val + shorter->val + ret;
    }
    longer->val = _sum % 10;
    return _sum / 10;
}

ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    int n1 = llLen(l1);
    int n2 = llLen(l2);

    ListNode* longer = n1 >= n2 ? l1 : l2;
    ListNode* shorter = n1 >= n2 ? l2 : l1;

    int ret = addTwoList(longer, shorter, abs(n1 - n2));
    if (ret) {
        ListNode* newHead = new ListNode(ret, longer);
        longer = newHead;
    }
    return longer;
}
