https://leetcode.com/problems/132-pattern/

https://leetcode.com/problems/132-pattern/discuss/94071/Single-pass-C%2B%2B-O(n)-space-and-time-solution-(8-lines)-with-detailed-explanation.

https://leetcode.com/problems/132-pattern/discuss/166953/Easy-and-concise-C%2B%2B-solution-using-a-stack-with-explanation-VERY-EASY-to-understand
``` cpp
class Solution {
public:
    bool find132pattern(vector<int>& nums) {
        stack<int> s;
        int prev = INT_MIN;
        
        for (auto it = nums.rbegin(); it != nums.rend(); it++) {
            while (!s.empty() && s.top() < *it) {
                if (prev > s.top())
                    return true;
                prev = s.top();
                s.pop();
            }
            
            s.push(*it);
        }
        
        return !s.empty() && prev > s.top();
    }
};
