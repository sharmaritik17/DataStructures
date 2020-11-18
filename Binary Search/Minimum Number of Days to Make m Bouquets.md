``` cpp
//  https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/

class Solution {
public:
	bool is_valid(vector<int>&a, int size, int m, int k, int mid) {
		int b_count = 0;
		int f_count = 0;
		for (int i = 0; i < size; i++) {
			f_count = (a[i] <= mid) ? f_count + 1 : 0;

			if (f_count == k) {
				f_count = 0;
				b_count++;
			}
			if (b_count == m) {
				return true;
			}
		}
		return 0;
	}
	int minDays(vector<int>& a, int m, int k) {
		if (m == 0 || k == 0 || a.empty())
			return 0;

		if (m * k > a.size()) {
			return -1;
		}

		int l = INT_MAX;
		int r = INT_MIN;
		for (int i = 0; i < a.size(); i++) {
			l = min(l, a[i]);
			r = max(r, a[i]);
		}
		while (l <= r) {
			int mid = l + (r - l) / 2;
			if (is_valid(a, a.size(), m, k, mid)) {
				r = mid - 1;
			}
			else
				l = mid + 1;
		}
		return l;
	}
};

```
