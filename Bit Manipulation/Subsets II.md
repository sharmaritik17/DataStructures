``` cpp

https://leetcode.com/problems/subsets-ii/

class Solution {
public:
	vector<vector<int>> subsetsWithDup(vector<int>& nums) {
		int  n = nums.size();
		vector<vector<int>> finalSet = {{}};

		sort(nums.begin(), nums.end());

		for (int i = 0; i < n;) {
			int count = 0;

			while (count + i < n && nums[count + i] == nums[i]) count++;

			int finalSetSize = finalSet.size();
			for (int j = 0; j < finalSetSize; j++) {

				vector<int> currSubset = finalSet[j];

				for (int k = 0; k<count; k++) {
					currSubset.push_back(nums[i]);
					finalSet.push_back(currSubset);
				}
			}
			i += count;
		}
		return finalSet;
	}
};


// MUST CHECK --- COOL DOWN COMMPLEXITY TO ONE STEP LOWER BY AVOIDING UNNECESSARY WORK WITH DUPLICATE WORK

vector<vector<int> > subsetsWithDup(vector<int> &S) {
	sort(S.begin(), S.end());

	vector<vector<int>> ret = {{}};

	int size = 0, startIndex = 0;

	for (int i = 0; i < S.size(); i++) {

		startIndex = i >= 1 && S[i] == S[i - 1] ? size : 0;
		size = ret.size();

		for (int j = startIndex; j < size; j++) {

			// vector<int> temp = ret[j];
			// temp.push_back(S[i]);
			// ret.push_back(temp);
			ret.push_back(ret[j]);
			ret.back().push_back(nums[i]);
		}
	}
	return ret;
}
