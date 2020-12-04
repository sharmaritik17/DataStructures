``` cpp

https://leetcode.com/problems/find-a-value-of-a-mysterious-function-closest-to-target/

##   MUST CHECK
https://leetcode.com/problems/find-a-value-of-a-mysterious-function-closest-to-target/discuss/959830/Four-Variables-%2B-O(N)-or-Basic-Concepts-or-C%2B%2B


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

Approach 2:- No need of Prefix/Suffix Array.... Four variables will help us.
Time Complexity - O(N)
Space Complexity - O(1)
class Solution {
public:
	int closestToTarget(vector<int>& arr, int target) {
		int n = arr.size();
		int finalAns = INT_MAX;

		int SuffixCurrent = 0;
		int suffixAhead = 0;

		suffixAhead = arr[n - 1];
		finalAns = min(finalAns, abs(suffixAhead - target));

		for (int i = n - 2; i >= 0; i--) {
			SuffixCurrent = arr[i] & suffixAhead;
			finalAns = min(finalAns, min(abs(SuffixCurrent - target), abs(arr[i] - target)));
			suffixAhead = SuffixCurrent;
		}

		int prefixCurrent = 0;
		int prefixPrevious = 0;

		prefixPrevious = arr[0];
		finalAns = min(finalAns, abs(prefixPrevious - target));
		
		for (int i = 1; i < n; i++) {
			prefixCurrent = arr[i]  & prefixPrevious;
			finalAns = min(finalAns, abs(prefixCurrent - target));
			prefixPrevious = prefixCurrent;
		}

		return finalAns;
	}
};
