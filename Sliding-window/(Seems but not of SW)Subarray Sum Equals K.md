``` cpp

https://leetcode.com/problems/subarray-sum-equals-k/

class Solution {
public:
	int subarraySum(vector<int>& nums, int k) {
		unordered_map<int, int> map;

		map[0] = 1;
		int sum = 0;
		int count = 0;
		for (int i = 0; i < nums.size(); i++) {
			sum += nums[i];

			if (map.find(sum - k) != map.end()) {
				count += map[sum-k];  
                // case [1,-1,0] //right o/p 3 if not included this then o/p 2(wrng)
			}
             // if sum existed then ++ otherwise =1  
			map[sum]++;
		}

		return count;
	}
};
