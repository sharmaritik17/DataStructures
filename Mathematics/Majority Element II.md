``` cpp
https://leetcode.com/problems/majority-element-ii/
 
TC-- O(N) SC-- O(1)

class Solution {
public:
	vector<int> majorityElement(vector<int>& nums) {
		int n = nums.size();
		int count1 = 0, count2 = 0, num1 = 0, num2 = 0;
		for (int i = 0; i < n; i++) {
			if (num1 == nums[i]) {
				count1++;
			}
			else if (num2 == nums[i]) {
				count2++;
			}
			else if (count1 == 0) {
				count1++;
				num1 = nums[i];
			}
			else if (count2 == 0) {
				count2++;
				num2 = nums[i];
			}
			else {
				count1--;
				count2--;
			}
		}

		int countHere1 = 0;
		int counthere2 = 0;
		for (auto it : nums) {
			if (num1 == it)
				countHere1++;
			else if (num2 == it)
				counthere2++;
		}
        
		vector<int> result;
		if (countHere1 > n / 3)
			result.push_back(num1);
		if (counthere2 > n / 3)
			result.push_back(num2);

		return result;
	}
};
