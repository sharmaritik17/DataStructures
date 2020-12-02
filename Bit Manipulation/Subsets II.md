``` cpp

https://leetcode.com/problems/subsets-ii/

class Solution {
public:
	vector<vector<int>> subsetsWithDup(vector<int>& nums) {
		int  n = nums.size();
		vector<vector<int>> finalSet = {{}};

		sort(nums.begin(), nums.end());

		for (int i = 0; i < n;) {
			int count = 0;

			while (count + i < n && nums[count + i] == nums[i]) count++;

			int finalSetSize = finalSet.size();
			for (int j = 0; j < finalSetSize; j++) {

				vector<int> currSubset = finalSet[j];

				for (int k = 0; k<count; k++) {
					currSubset.push_back(nums[i]);
					finalSet.push_back(currSubset);
				}
			}
			i += count;
		}
		return finalSet;
	}
};
