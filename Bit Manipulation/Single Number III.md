``` cpp

https://leetcode.com/problems/single-number-iii/
https://www.youtube.com/watch?v=u5-ss5kKy7g

class Solution {
public:
	vector<int> singleNumber(vector<int>& nums) {
		int allXOR = 0;
		for (auto it : nums) {
			allXOR ^= it;
		}

		
        allXOR &= -allXOR;  // to find lowest bit = 1 in allXOR
        int setBit = allXOR;
        //but not necessary in this problem to find that particular,you may find any kth set bit
        
		int a = 0, b = 0;
		for (auto it : nums) {
			if (setBit & it) {
				a ^= it;
			}
			else {
				b ^= it;
			}
		}
		return {a, b};
	}
};
