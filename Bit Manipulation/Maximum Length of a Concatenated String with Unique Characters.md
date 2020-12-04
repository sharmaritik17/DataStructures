``` cpp
https://leetcode.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters/discuss/959340/Back-Tracking-or-KnapSack(Modified)-Version-or-Solution

class Solution {
public:
	int maxLength(vector<string>& A) {

		vector<bitset<26>> dp = {bitset<26>()};

		int res = 0;
		for (auto& s : A) {
			bitset<26> a;

			for (char c : s) {
				a.set(c - 'a');
			}
			int n = a.count();
			if (n < s.size()) continue;

			for (int i = 0; i < dp.size(); ++i) {
				bitset c = dp[i];
				if ((c & a).any()) continue;
				dp.push_back(c | a);
				res = max(res, (int)c.count() + n);
			}
		}
		return res;
	}
};
