``` cpp

https://leetcode.com/problems/maximum-number-of-occurrences-of-a-substring/submissions/

class Solution {
public:
	int maxFreq(string s, int maxLetters, int minSize, int maxSize) {
		int start = 0;
		int result = 0;
		unordered_map<int, int> windowChars;
		unordered_map<string, int> totalSubstrings;

		for (int end = 0; end < s.size(); end++) {
			windowChars[s[end]]++;

			if (end - start + 1 > minSize) {
				if (--windowChars[s[start]] == 0) {
					windowChars.erase(s[start]);
				}
				start++;
			}

			if (end - start + 1 == minSize && windowChars.size() <= maxLetters) {
				result = max(result, ++totalSubstrings[s.substr(start, end - start + 1)]);
			}
		}
		return result;
	}
};
