``` cpp

https://leetcode.com/problems/majority-element/

https://www.geeksforgeeks.org/check-whether-k-th-bit-set-not/    /************************/ must check

//BOYRE'S MOORE VOTING ALGORTIHM
class Solution {
public:
	int majorityElement(vector<int>& nums) {
		int count = 0;
		int candidate = 0;


		for (int i = 0; i < nums.size(); i++) {
			if (count == 0) {
				candidate = nums[i];
			}

			if (candidate == nums[i])
				count++;
			else
				count--;
		}

		return candidate;
	}
};

//BIT MAGIC
class Solution {
public:
	int majorityElement(vector<int>& nums) {
		int candidate = 0;
		int n = nums.size();

		for (int i = 0; i < 32; i++) {
            int ones = 0;
			for (int j = 0; j < n; j++) {
				if (nums[j] & 1 << i) {
					ones++;
				}
				if ( 2*ones > n) {
					candidate |= 1 << i;
				}
			}
		}
		return candidate;
	}
};

//can be used as
class Solution {
public:
	int majorityElement(vector<int>& nums) {
		int candidate = 0;
		int n = nums.size();

		for (int i = 0; i < 32; i++) {
            int ones = 0;

			for (int j = 0; j < n; j++) {
				//if (nums[j] & 1 << i) {
				if (nums[j]>>i & 1 ) {   /************************************************************************/
					ones++;
				}
				if ( 2*ones > n) {
					candidate |= 1 << i;
				}
			}
		}
		return candidate;
	}
};
