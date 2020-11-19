``` cpp
https://leetcode.com/problems/minimum-size-subarray-sum/

class Solution {
public:
    int minSubArrayLen(int s, vector<int>& vec)
    {
        int size = vec.size();

        if (!size)
            return 0;

        int windowStart = 0;
        int currWindowSum = 0;
        int minLength = INT_MAX;

        for (int windowEnd = 0; windowEnd < size; windowEnd++) {
            currWindowSum += vec[windowEnd];

            while (currWindowSum >= s) {
                minLength = min(minLength, windowEnd - windowStart + 1);
                currWindowSum -= vec[windowStart];
                windowStart++;
            }
            
        }
        return minLength != INT_MAX ? minLength : 0;
    }
};
