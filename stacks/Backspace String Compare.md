https://leetcode.com/problems/backspace-string-compare/

https://leetcode.com/problems/backspace-string-compare/solution/  

``` cpp
class Solution {
public:
  bool backspaceCompare(string s, string t) {
    int count = 0;
    int i = s.length() - 1, j = t.length() - 1;
    int skipS = 0, skipT = 0;
    while (i >= 0 || j >= 0) {
      while (i >= 0) {
        if (s[i] == '#') {
          skipS++; i--;
        }
        else if (skipS > 0) {
          skipS--; i--;
        }
        else {
          break;
        }
      }

      while (j >= 0) {
        if (t[j] == '#') {
          skipT++; j--;
        }
        else if (skipT > 0) {
          skipT--; j--;
        }
        else {
          break;
        }
      }

      if (((i >= 0 && j >= 0) && s[i] != t[j]) || ((i >= 0) != (j >= 0))) {
        return false;
      }
      i--;
      j--;
    }

    return true;
  }
};
