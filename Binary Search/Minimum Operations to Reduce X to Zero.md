``` cpp
// https://leetcode.com/problems/minimum-operations-to-reduce-x-to-zero/

// https://leetcode.com/problems/minimum-operations-to-reduce-x-to-zero/discuss/940444/faster-than-98.80-of-C%2B%2B-easy-buzzy-Sliding-Window

// efiicient TC O(N) SC O(1)
class Solution {
public:
	int minOperations(vector<int> &nums, int x) {
		if (!nums.size())
			return -1;

		int sum = accumulate(nums.begin(), nums.end(), 0) - x;

		if (sum < 0)
			return -1;

		if (sum == 0)
			return nums.size();

		int curr = 0;
		int start = 0;
		int res = INT_MIN;

		for (int end = 0; end < nums.size(); end++) {
			if (curr < sum)
				curr += nums[end];

			while (curr >= sum) {
				if (curr == sum) {
					res = max(res, end - start + 1);
				}
				curr -= nums[start++];
			}
		}

		return res != INT_MIN ? nums.size() - res : -1;
	}
};
 
 // TC O(N) SC O(N)
class Solution {
public:
	int minOperations(vector<int>& nums, int x) {
		int target = -x;
		for (auto it : nums)
			target += it;

		if (target == 0)
			return nums.size();

		unordered_map<int, int>map;
                 map[0]=-1;
        
		int res = -1;
		int sum = 0;

		for (int i = 0; i<nums.size(); i++) {

			sum += nums[i];

			if (map.find(sum - target) != map.end()) {
				res = max(res, i - map[sum - target]);
			}

			map[sum] = i;
		}
		return res != -1 ? nums.size() - res : res;
	}
}; 
```
