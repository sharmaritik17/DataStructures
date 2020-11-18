``` cpp

// https://leetcode.com/problems/furthest-building-you-can-reach/

class Solution {
public:
	int furthestBuilding(vector<int>& arr, int bricks, int ladders) {
		priority_queue<int, vector<int>, greater<int>> pq;

		int n = arr.size();

		for (int i = 0; i < n - 1; i++) {
			if (arr[i + 1] <= arr[i])
				continue;

			pq.push(arr[i + 1] - arr[i]);

			if (pq.size() > ladders) {
				bricks -= pq.top();
				pq.pop();

				if (bricks < 0) {
					return i;
				}
			}
		}
		return n - 1;
	}
};
