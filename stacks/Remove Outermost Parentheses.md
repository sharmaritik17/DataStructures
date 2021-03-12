``` cpp
When we meet outermost '(', the count will be 0, so we post increment the count to ignore that '('.
When we meet outermost ')', the count will be 1, so we pre decrement the count to ignore that ')'.


class Solution {
public:

  string removeOuterParentheses(string S) {
    int st = 0;
    string ans;
    for (auto a : S)
    {
      if (a == '(')
      {
        if (st > 0)
        {
          ans += '(';
        }
        st++;
      }
      else
      {
        if (st > 1)
        {
          ans += ')';
        }
        st--;
      }
    }
    return ans;
  }
};


class Solution {
public:
  string removeOuterParentheses(string S) {
    string res = ""; stack<char> stack;

    for (char curr : S) {

      if (curr == '(') {
        if (stack.size() > 0) {
          res += curr;
        }
        stack.push(curr);
      }
      else {
        if (stack.size() > 1) {
          res += curr;
        }
        stack.pop();
      }
      
    }
    return res;
  }
};
