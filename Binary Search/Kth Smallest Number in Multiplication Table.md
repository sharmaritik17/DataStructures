``` cpp
https://leetcode.com/problems/kth-smallest-number-in-multiplication-table/

class Solution {
public:

	bool isMidPossible(int mid, int m, int n, int k) {
		int count = 0;
		for (int i = 1; i <= m; i++) {
			count += min(mid / i, n);
		}
		return count >= k;
	}

	int findKthNumber(int m, int n, int k) {
		int left = 1;
		int right = m * n;
		while (left < right) { // similar to left<=right need to use one thing extra then
			int mid = left + ((right - left) >> 1);
			
			if (!isMidPossible(mid, m, n, k)) {
				left = mid + 1;
			}
			else {
				right = mid; // this step
			}
		}

		return left;
	}
};
