``` cpp
https://leetcode.com/problems/sliding-window-maximum/

/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/



class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        int n = nums.size();

        if (!n)
            return {};

        vector<int> result;
        deque<int> dq;

        for (int i = 0; i < n; i++) {

            //indexes present in window size has been exhausted
            while (!dq.empty() && dq.front() < i - k + 1) {
                dq.pop_front();
            }

            // monotonic increasing dequeue
            while (!dq.empty() && nums[dq.back()] < nums[i]) {
                dq.pop_back();
            }

            //push every element
            dq.push_back(i);

            //take front element as this will be max from current particular window
            if (i >= k - 1)
                result.push_back(nums[dq.front()]);

        }
        return result;
    }
};

/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/ //prefix-suffix
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        int n = nums.size();

        if (!n)
            return {};

        int left_max[n];
        int right_max[n];

        vector<int> result;
        // according to question window size is given as 1 based indexing
        // but i'm taking it as zero based so wont be any problem
        for (int i = 0; i < n; i++) {
            if (i == 0 || i % k == 0)
                left_max[i] = nums[i];
            else
                left_max[i] = max(left_max[i - 1], nums[i]);
        }

        // thats why here we need to stop at (j+1)%k
        for (int j = n - 1; j >= 0; j--) {
            if (j == n - 1 || (j + 1) % k == 0)
                right_max[j] = nums[j];
            else
                right_max[j] = max(right_max[j + 1], nums[j]);
        }

        //left_max[i + k - 1] because at this point k size window will be completed
        for (int i = 0; i < n - k + 1; i++) {
            result.push_back(max(left_max[i + k - 1], right_max[i]));
        }

        return result;
    }
};

