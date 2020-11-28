```  cpp

https://leetcode.com/problems/grumpy-bookstore-owner/

https://leetcode.com/problems/grumpy-bookstore-owner/discuss/951750/Resolving-BUD-property-Explanation-Brute-forceSliding-Window


Approach 1:- Brute Force
P.S. -- I love to find BUD property in every problem :)

class Solution {
public:
	int maxSatisfied(vector<int>& customers, vector<int>& grumpy, int X) {

		int result = -1;
		int n = grumpy.size();

		for (int i = 0; i < n; i++) {
			for (int j = i; j < min(n, i + X) ; j++) {  // bottle neck(wanting here to do all work at one go) --- sliding window

				int save = 0;
				for (int k = i; k <= j; k++) { // duplicate(again again sub array(window)) --- sliding window
					save += customers[k];
				}

				for (int it = 0; it < n; it++) { //unnecessary work(non-grumpy calculate) --- precalculate/prefix
					if (it >= i && it <= j) {
						continue;
					}

					if (grumpy[it] == 0) {
						save += customers[it];
					}
				}

				result = max(save, result);
			}
		}

		return result;
	}
};


Approach 2: After checking BUD, Sliding Window
P.S. -- I have taken the naming in very effective way. Hope it adds more to your thinking

class Solution {
public:
	int maxSatisfied(vector<int>& customers, vector<int>& grumpy, int X) {
		auto totalGrumpySum = 0, windowNonGrumpySum = 0, result = 0;

		for (int i = 0; i < customers.size(); i++) {

			totalGrumpySum +=  grumpy[i] ? 0 : customers[i];
			windowNonGrumpySum += grumpy[i] ? customers[i] : 0;

			if (i >= X) {
				windowNonGrumpySum -= grumpy[i - X] ? customers[i - X] : 0;
			}
			result = max(result, windowNonGrumpySum);
		}

		return totalGrumpySum + result;
	}
};
