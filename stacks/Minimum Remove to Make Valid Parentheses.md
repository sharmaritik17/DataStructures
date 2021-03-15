https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/

``` cpp
class Solution {
public:
  string minRemoveToMakeValid(string s) {
    int count = 0;

    for (int i = 0; s[i]!='\0'; i++) {
      if (s[i] == '(') {
        count++;
      }
      else if (s[i] == ')') {
        if (count == 0) {
          s[i] = '*';
        }
        else {
          count--;
        }
      }
    }

    count = 0;
    for (int i = s.length() - 1; i >= 0; i--) {
      if (s[i] == ')') {
        count++;
      }
      else if (s[i] == '(') {
        if (count == 0) {
          s[i] = '*';
        }
        else {
          count--;
        }
      }
    }

    string res = "";
    for (auto curr : s) {
      if (curr != '*') {
        res.push_back(curr);
      }
    }

    return res;
  }
};
