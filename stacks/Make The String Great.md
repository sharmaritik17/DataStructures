https://leetcode.com/problems/make-the-string-great/

https://leetcode.com/problems/make-the-string-great/discuss/1107250/Simplicity-Without-Stack-or-Intuitive-or-Easy-Understanding-or-C%2B%2B

https://leetcode.com/problems/make-the-string-great/discuss/780897/C%2B%2B-Brute-Force-%2B-Two-Pointers
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



string makeGood(string s, int p = 0) {
    for (int i = 0; i < s.size(); ++i) {
        if (p > 0 && abs(s[i] - s[p - 1]) == 32)
            --p;
        else
            s[p++] = s[i];
    }
    return s.substr(0, p);
}
