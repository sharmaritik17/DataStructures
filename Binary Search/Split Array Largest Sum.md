``` cpp
https://leetcode.com/problems/split-array-largest-sum/

https://leetcode.com/problems/split-array-largest-sum/discuss/942730/100-Faster-Fast-Explanation-with-comments-MIN-MAX

#define ll long long
class Solution {
public:

	bool isCutsPossible(vector<int> &nums, ll mid, int cuts) {
		int accumulate = 0;

		for (auto it : nums) {
			if (it > mid)
				return false;

			else if (accumulate + it <= mid) accumulate += it;

			else {
				cuts--;
				accumulate = it;

				if (cuts == 0) {
					return false;
				}
			}
		}

		return true;
	}

	int splitArray(vector<int>& nums, int m) {
		if (!nums.size())
			return -1;

		if (m > nums.size())
			return -1;

		ll  left = 0,right = 0;
		for (auto it : nums) {
			left = max(left, (ll)it);
			right += it;
		}

		while (left <= right) {
			ll mid = left + (right - left) / 2;

			if (isCutsPossible(nums, mid, m)) {
				right = mid - 1;
			}
			else {
				left = mid + 1;
			}
		}
		return left;
	}
};
