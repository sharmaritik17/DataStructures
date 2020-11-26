``` cpp
https://leetcode.com/problems/make-sum-divisible-by-p/

class Solution {
public:
	int minSubarray(vector<int>& nums, int p) {
		int n = nums.size();
		int need = 0, curr = 0, res = INT_MAX;
		for (auto it : nums) {
			need = (need + it) % p; 
		}
        
		unordered_map<int, int> map;
		map[0] = -1;
		for (int i = 0; i < n; i++) {
			curr = (curr + nums[i]) % p;
			map[curr] = i;
			int want = (curr - need + p) % p;
			if (map.find(want) != map.end()) {
				res = min(res, i-map[want]);
			}
		}
		return res < n ? res : -1;
	}
};
