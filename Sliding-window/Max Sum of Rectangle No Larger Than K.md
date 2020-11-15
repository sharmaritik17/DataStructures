https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/


/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/

``` cpp
class Solution {
public:
    int maxSumSubmatrix(vector<vector<int>>& matrix, int k) {
        if (matrix.empty()) return 0;
        int row = matrix.size(), col = matrix[0].size(), res = INT_MIN;
        for (int l = 0; l < col; ++l) {
            vector<int> sums(row, 0);
            for (int r = l; r < col; ++r) {
                for (int i = 0; i < row; ++i) {
                    sums[i] += matrix[i][r];
                }

                // Find the max subarray no more than K
                set<int> accuSet;
                accuSet.insert(0);
                int curSum = 0, curMax = INT_MIN;
                for (auto sum : sums) {
                    curSum += sum;
                    auto it = accuSet.lower_bound(curSum - k); // returns a iterator
                    if (it != accuSet.end()) {
                        curMax = max(curMax, curSum - *it);
                    }
                    accuSet.insert(curSum);

                }
                res = max(res, curMax);
            }
        }
        return res;
    }
};
```
