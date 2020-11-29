``` cpp

https://leetcode.com/problems/maximum-product-of-word-lengths/

Time Complexity -- O(N) where N is characters presents in all strings

because we don't know about max string length in this ques and we can't guess... so this will be enough to come up with

Space complexity -- O(1)  at most 2^26 entries only

class Solution {
public:
	int maxProduct(vector<string>& words) {
		int n = words.size();
		int result = 0;
		unordered_map<int, int> map;

		for (auto wrd : words) {
			int mask = 0;
			for (auto ch : wrd) {
				mask |= 1 << (ch - 'a');
			}
			map[mask] = max(map[mask], (int)wrd.size());
			for (auto it : map) {
				if (!(mask & it.first)) {
					result = max(result, (int)wrd.size() * it.second);
				}
			}
		}
		return result;
	}
};
