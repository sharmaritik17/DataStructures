https://leetcode.com/problems/score-of-parentheses/

https://leetcode.com/problems/score-of-parentheses/discuss/141975/c%2B%2B-solution-using-stack-(5ms)-detail-explained

https://leetcode.com/problems/score-of-parentheses/discuss/141777/C%2B%2BJavaPython-O(1)-Space


``` cpp
    int scoreOfParentheses(string S) {
        int res = 0, l = 0;
        for (int i = 0; i < S.length(); ++i) {
            if (S[i] == '(') l++; else l--;
            if (S[i] == ')' && S[i - 1] == '(') res += 1 << l;
        }
        return res;
    }
