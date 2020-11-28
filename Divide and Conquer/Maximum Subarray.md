``` cpp

https://leetcode.com/problems/maximum-subarray/

https://leetcode.com/problems/maximum-subarray/discuss/952353/Divide-and-Conquer-Explanation-C%2B%2B

class Solution {
private:
	int maxSubArrayHelper(vector<int>& nums, int left, int right) {
		if (left > right)
			return INT_MIN;

		int mid = left + (right - left) / 2;

		int maxLeft = maxSubArrayHelper(nums, left, mid - 1);
		int maxRight = maxSubArrayHelper(nums, mid + 1, right);

		int maxLeftSum = 0, maxRightSum = 0;
		//use any indication, large mininmum won't burst some cases

		for (int i = mid - 1, sum = 0; i >= left; i--) {
			sum += nums[i];
			maxLeftSum = max(maxLeftSum, sum);
		}

		for (int i = mid + 1, sum = 0; i <= right; i++) {
			sum += nums[i];
			maxRightSum = max(maxRightSum, sum);
		}

		int maxSubarrays = max(maxLeft, maxRight);
		int currSubarray =  nums[mid] + maxLeftSum + maxRightSum;

		return max(maxSubarrays, currSubarray);
	}
public:
	int maxSubArray(vector<int>& nums) {
		return maxSubArrayHelper(nums, 0, nums.size() - 1);
	}
};
