https://leetcode.com/problems/make-the-string-great/

https://leetcode.com/problems/make-the-string-great/discuss/1107250/Simplicity-Without-Stack-or-Intuitive-or-Easy-Understanding-or-C%2B%2B
``` cpp
class Solution {
public:
  string makeGood(string s) {
    if (s.empty())
      return "";

    int n = s.length();
    int ptr = -1;
    int  i = 0;
    while (i < n) {
      if (ptr == -1 || abs(s[ptr] - s[i]) != 32) {
        ptr++;
        s[ptr] = s[i];
        i++;
      }
      else {
        while (i < n && ptr > -1 && abs(s[ptr] - s[i]) == 32) {
          ptr--;
          i++;
        }
      }
    }

    return s.substr(0, ptr + 1);
  }
};
