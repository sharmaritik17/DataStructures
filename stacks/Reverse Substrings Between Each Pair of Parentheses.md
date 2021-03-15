https://leetcode.com/problems/reverse-substrings-between-each-pair-of-parentheses/

https://leetcode.com/problems/reverse-substrings-between-each-pair-of-parentheses/discuss/1111319/Simplicity-or-Stack-or-C%2B%2B-or-Intuitive


``` cpp

class Solution {
  void reverse(string &s, int i, int j) {
    while (i < j) {
      swap(s[i++], s[j--]);
    }
  }
public:
  string reverseParentheses(string s) {
    stack<int> stack;
    string res;
    for (int i = 0; s[i] != '\0'; i++) {
      if (s[i] == '(') {
        stack.push(res.length());
      }
      else if (s[i] == ')') {
        reverse(res, stack.top(), res.length()-1);
        stack.pop();
      }
      else {
        res += s[i];
      }
    }

    return res;
  }
};
