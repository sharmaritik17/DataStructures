https://leetcode.com/problems/longest-well-performing-interval/


``` cpp
class Solution {
public:
    int longestWPI(vector<int>& hours) {
        int res = 0, score = 0, n = hours.size();
        unordered_map<int, int> seen;
        for (int i = 0; i < n; ++i) {
            score += hours[i] > 8 ? 1 : -1;
            if (score > 0) {
                res = i + 1;
            } else {
                
                if (seen.find(score) == seen.end()){
                    seen[score] = i;
                }
                // seen[score-1] is the leftmost idx with smaller score,
                // because for i from 1 to some positive k,
                // seen[score-i] is a strickly increasing sequence
                if (seen.find(score - 1) != seen.end()){
                    res = max(res, i - seen[score - 1]);
                }
            }
        }
        return res;
    }
};
