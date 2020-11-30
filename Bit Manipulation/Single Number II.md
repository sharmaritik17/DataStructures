``` cpp

https://leetcode.com/problems/single-number-ii/

Hard to come up with this approach

class Solution {
public:
	int singleNumber(vector<int>& nums) {
		int ones = 0;
		int twos = 0;

		for (auto i : nums)
		{
			ones = (ones ^ i);
			ones = ones & (~twos);
                        twos = (twos^i); 
			twos = twos & (~ones);
		}
		return ones;
	}
};
