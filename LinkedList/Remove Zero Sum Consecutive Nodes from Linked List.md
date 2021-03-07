https://leetcode.com/problems/remove-zero-sum-consecutive-nodes-from-linked-list/

``` cpp

#define data val
class Solution {
public:
    ListNode* removeZeroSumSublists(ListNode* head) {
        ListNode *dummy = new ListNode(0);
        dummy->next = head;

        unordered_map<int, ListNode*> map;

        ListNode *curr = dummy;
        int prefix = 0;
        while (curr) {

            prefix += curr->data;

            if (map.find(prefix) != map.end()) { //found the match in map
                ListNode *save = map[prefix]->next;

                int buildUp = prefix + save->data;
                while (buildUp != prefix) {
                    map.erase(buildUp);
                    save = save->next;
                    buildUp += save->data;
                }

                map[prefix]->next = save->next;

            }
            else{
                map[prefix] = curr;
            }

            curr = curr->next;
        }

        return dummy->next;
    }
};



#define data val
class Solution {
public:
    ListNode* removeZeroSumSublists(ListNode* head) {
        ListNode *dummy = new ListNode(0);
        dummy->next = head;

        unordered_map<int, ListNode*> seen;

        int prefix = 0;
        for (ListNode* i = dummy; i; i = i->next) {
            prefix += i->data;
            seen[prefix] = i;
        }

        prefix = 0;
        for (ListNode *i = dummy; i; i = i->next) {
            prefix += i->data;
            i->next = seen[prefix]->next;
        }

        return dummy->next;
    }
};
