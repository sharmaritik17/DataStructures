``` cpp

https://leetcode.com/problems/find-a-value-of-a-mysterious-function-closest-to-target/


class Solution {
public:
	int closestToTarget(vector<int>& arr, int target) {
		int ans = INT_MAX, n = arr.size();

		set<int> st[n];
		// set[i] -> contains **unique** AND values of subarrays starting from ith index

		st[n - 1] = { arr[n - 1] };
		for (int i = n - 2; i >= 0; i--)
		{
			// calcuting st[i] with help of st[i+1]
			st[i].insert(arr[i]);
			for (auto &val : st[i + 1])
			{
				int new_val = (arr[i] & val);
				st[i].insert( new_val );
			}
		}

		// Iterate over all possible AND values and find the ans
		for (int i = 0; i < n; i++)
		{
			for ( auto &val : st[i] ) ans = min(ans, abs(val - target));
		}

		return ans;
	}
};
