``` cpp
https://leetcode.com/problems/next-greater-node-in-linked-list/



#define data val
class Solution {
public:
    vector<int> nextLargerNodes(ListNode* head) {
        vector<int> res;
        stack<pair<int, int>> st;

        for (int i = 0; head; head = head->next) {

            while (st.size() && st.top().first < head->data) {
                int index = st.top().second;
                res[index] = head->data;
                st.pop();
            }

            st.push({head->data, i++});

            res.push_back(0);
        }
        return res;
    }
};


#define data val
class Solution {
public:
  vector<int> nextLargerNodes(ListNode* head) {
    vector<int> res;
    stack<int> stack;  // save indexes

    for (int i = 0; head; head = head->next) {

      while (stack.size() && res[stack.top()] < head->data) {
        res[stack.top()] = head->data;
        stack.pop();
      }

      stack.push(i++);

      res.push_back(head->data);
    }

    while (stack.size()) {
      res[stack.top()] = 0;
      stack.pop();
    }

    return res;
  }
};
