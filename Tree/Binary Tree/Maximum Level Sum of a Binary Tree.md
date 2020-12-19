

https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree/
``` cpp
#define data val
#include<unordered_map>
#define level first
#define value  second
class Solution {
	unordered_map<int, int> map;
	void maxLevelSumHelper(TreeNode *root, int level) {
		if (!root)
			return;

		map[level] += root->data;

		maxLevelSumHelper(root->left, level + 1);
		maxLevelSumHelper(root->right, level + 1);
	}
public:
	int maxLevelSum(TreeNode* root) {
		if (!root)
			return 0;

		int maxSum = root->data,saveLevel = 1;

		maxLevelSumHelper(root, 1);

		for (auto it : map) {
			if (it.value > maxSum || it.value == maxSum && it.level < saveLevel) {
				maxSum = it.value;
				saveLevel = it.level;
			}
		}
		return saveLevel;
	}
};
