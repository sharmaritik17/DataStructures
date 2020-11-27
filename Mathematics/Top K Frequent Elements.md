``` cpp

https://leetcode.com/problems/top-k-frequent-elements/


class Solution {
public:
	vector<int> topKFrequent(vector<int>& nums, int k) {
		unordered_map<int, int> map;

		for (auto &it : nums)
			++map[it];

		vector<vector<int>> buckets(nums.size() + 1);
		for (auto &it : map)
			buckets[it.second].push_back(it.first);

		reverse(buckets.begin(), buckets.end());

		vector<int> result;
		for (auto &bucket : buckets) {
			for (auto &it : bucket) {
				k--;
				result.push_back(it);
				if (!k) {
					return result;
				}
			}
		}
		return result;
	}
};
