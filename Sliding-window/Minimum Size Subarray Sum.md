``` cpp
https://leetcode.com/problems/minimum-size-subarray-sum/

/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/


https://leetcode.com/problems/minimum-size-subarray-sum/discuss/913642/Sol-With-picture-%2B-Explanation-Sliding-Window-Easy-understanding

/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/


//bruteforce
class Solution {
public:
    int minSubArrayLen(int S, vector<int>& arr) {
        int n = arr.size();
        if (!n) {
            return 0;
        }

        int final_ans = INT_MAX;
        vector<int> prefix(n + 1);
        prefix[0] = arr[0];

        for (int i = 1; i < n; i++) {
            prefix[i] = prefix[i - 1] + arr[i];
        }
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                int temp_sum = prefix[j] - prefix[i] + arr[i];
                if (temp_sum >= S) {
                    final_ans = min(final_ans, j - i + 1);
                    break;
                }
            }
        }
        return (final_ans != INT_MAX) ? final_ans : 0;
    }
};
/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/

//brute force + optimisation
class Solution {
public:
    int minSubArrayLen(int s, vector<int>& nums)
    {
        int n = nums.size();
        if (n == 0)
            return 0;
        int ans = INT_MAX;
        vector<int> sums(n);
        sums[0] = nums[0];
        for (int i = 1; i < n; i++)
            sums[i] = sums[i - 1] + nums[i];
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                int sum = sums[j] - sums[i] + nums[i];
                if (sum >= s) {
                    ans = min(ans, (j - i + 1));
                    break; //Found the smallest subarray with sum>=s starting with index i, hence move to next index
                }
            }
        }
        return (ans != INT_MAX) ? ans : 0;
    }
};
/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/

//binary search
class Solution {
public:
    int minSubArrayLen(int s, vector<int>& nums)
    {
        int n = nums.size();
        if (n == 0)
            return 0;
        int ans = INT_MAX;
        vector<int> sums(n + 1, 0); //size = n+1 for easier calculations
        //sums[0]=0 : Meaning that it is the sum of first 0 elements
        //sums[1]=A[0] : Sum of first 1 elements
        //ans so on...
        for (int i = 1; i <= n; i++)
            sums[i] = sums[i - 1] + nums[i - 1];
        for (int i = 1; i <= n; i++) {
            int to_find = s + sums[i - 1];
            auto bound = lower_bound(sums.begin(), sums.end(), to_find);
            if (bound != sums.end()) {
                cout << *bound << endl;
                ans = min(ans, static_cast<int>(bound - (sums.begin() + i - 1)));
            }
        }
        return (ans != INT_MAX) ? ans : 0;
    }
};
/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/

//sliding window
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
        return minLength == INT_MAX ? -1 : minLength;
    }
};
