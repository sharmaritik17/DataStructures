``` cpp

https://leetcode.com/problems/number-of-good-ways-to-split-a-string/

https://leetcode.com/problems/number-of-good-ways-to-split-a-string/discuss/955091/Prefix-or-Sliding-Window-or-Explanation-With-Comments

Approach 2:- Sliding Window + Precomputation

TIME COMPLEXITY -- O(N) WHERE N = STRING LENGTH
SPACE COMPLEXITY -- O(1) // 26 is constant

class Solution {
public:
	int numSplits(string s) {
		int n = s.size();
		int left[26] = {} , right[26] = {}, uniqueLeft = 0, uniqueRight = 0, ans = 0;
		for (auto it : s) {
			uniqueRight += ++right[it - 'a'] == 1; // counting unique chars and how many times what char is occuring in given stream
		}
		for (int i = 0; i < n; i++) {
			uniqueLeft += ++left[s[i] - 'a'] == 1;  // here entering a char will be unique
			uniqueRight -= --right[s[i] - 'a'] == 0; //here last leaving from pack of that chars(alphabets) will be unique
			if (uniqueLeft > uniqueRight)  // we want balance strings(unique chars)
				break;
			ans += uniqueLeft == uniqueRight;
		}
		return ans;
	}

};
