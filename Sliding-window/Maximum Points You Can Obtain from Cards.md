``` cpp
https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/


// TC O(N) SC O(1)
class Solution {
public:
	int maxScore(vector<int>& cardPoints, int k) {
		int n = cardPoints.size();

		int subSize = n - k; //n>k
		int windowSum = 0;
		for (int i = 0; i < subSize; i++) {
			windowSum += cardPoints[i];
		}

		int minFar = windowSum, total = windowSum;

		for (int i = subSize; i < n; i++) {
			windowSum += cardPoints[i] - cardPoints[i - subSize];
			total += cardPoints[i];
			minFar = min(minFar, windowSum);
		}

		return total - minFar;
	}
};


// TC O(K) SC O(1)
class Solution {
public:
	int maxScore(vector<int>& cardPoints, int k) {
		int n = cardPoints.size();

		int left = 0;
		//first k indexes
		for (int i = 0; i < k; i++) {
			left += cardPoints[i];
		}

		int ans = left;
		int right = 0;
		//leave k indexes from left from back one by one and choose from right
		
		for (int i = 0; i < k; i++) {
			left -= cardPoints[k - i - 1];
			right += cardPoints[n - i - 1];

			ans = max(ans, left + right);
		}

		return ans;
	}
};
