``` cpp

https://leetcode.com/problems/find-the-difference/

class Solution {
public:
	char findTheDifference(string s, string t) {
		char Xor = 0;
		for (auto it : s) {
			Xor ^= it;
		}
		for (auto it : t) {
			Xor ^= it;
		}
		return Xor;
	}
};
