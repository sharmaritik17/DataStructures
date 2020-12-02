```cpp
https://leetcode.com/problems/subsets/
class Solution {
public:
	vector<vector<int>> subsets(vector<int>& nums) {
		vector<vector<int>> subs = {{}};

		for (auto it : nums) {
			int n = subs.size();
			for (int i = 0; i < n; i++) {
				subs.push_back(subs[i]);
				subs.back().push_back(it);
			}
		}

		return subs;
	}
};

class Solution {
public:
	vector<vector<int>> subsets(vector<int>& nums) {
		int n = nums.size();
		int size = 1 << n;
		vector<vector<int>> subs(size);

		for (int i = 0; i < size; i++) {
			for (int j = 0; j < n; j++) {
				if ((i >> j) & 1) {
					subs[i].push_back(nums[j]);
				}
			}
		}
		return subs;
	}
};
