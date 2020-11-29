``` cpp
https://leetcode.com/problems/minimum-flips-to-make-a-or-b-equal-to-c/

https://leetcode.com/problems/minimum-flips-to-make-a-or-b-equal-to-c/discuss/953388/Explanation-or-Comments-or-Bit-Masking

class Solution {
public:
	int minFlips(int a, int b, int c) {
		int count = 0;
		int aOrB = a | b;

		for (int i = 0; i < 32; i++) {
			if (!(aOrB >> i & 1) && (c >> i & 1))
				count++;
			
			else if ((aOrB >> i & 1) && !(c >> i & 1)) {
				if ((a >> i & 1) && (b >> i & 1)) {
					count += 2;
				}
				else {
					count++;
				}
			}

		}

		return count;
	}
};
