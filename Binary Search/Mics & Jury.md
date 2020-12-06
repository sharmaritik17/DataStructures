``` cpp

https://practice.geeksforgeeks.org/contest-problem/mics-jury/1/

class Solution
{
private:
	bool isPossible(int mid, int n, int tobeMade, int *teams) {
		int count = 0;
		for (int i = 0; i < n; i++) {
			count += teams[i] / mid; //this will be like 5/2 = 2times
			if (teams[i] % mid)  //as 1 from there left --  can be calculated 5%2 = 1
				count++;
		}
		if (count <= tobeMade) {
			return true;
		}
		return false;
	}

public:
	int micsandjury(int tobeMade, int n, int teams[])
	{
		//code here

		int left = 1;
		int right = *max_element(teams, teams + n);

		while (left <= right) {
			int mid = left + ((right - left) / 2);

			if (isPossible(mid, n, tobeMade, teams)) {
				right = mid - 1;
			}
			else {
				left = mid + 1;
			}
		}
		return left;
	}
};
