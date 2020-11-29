```cpp

https://leetcode.com/problems/binary-number-with-alternating-bits/

to check neighbouting bits by n>>1 and n>>2

(n & n >> 2) == (n >> 2) this needed for the cases like where bits arent available like 0,1,2 only but this not base case (not recrsn)

class Solution {
public:
	bool hasAlternatingBits(int n) {
		return ((n & n >> 1)==0 && (n & n >> 2) == (n >> 2));
	}
};
