``` cpp

https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/

https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/discuss/954451/Explanation-or-Trie-or-Approach

class TrieNode {
public:
	TrieNode *left;
	TrieNode *right;
};

void insertNode(int n, TrieNode *head) {
	TrieNode *curr = head;
	for (int i = 31; i >= 0; i--) {

		int bit = (n >> i) & 1;

		if (bit == 0) {
			if (!curr->left) {
				curr->left = new TrieNode();
			}
			curr = curr->left;
		}

		else {
			if (!curr->right) {
				curr->right = new TrieNode();
			}
			curr = curr->right;
		}

	}
}

class Solution {
public:
	int findMaximumXORHelper(vector<int>& nums, TrieNode *head, int size) {
		int maXOR = INT_MIN;

		for (int i = 0; i < size; i++) {
			int value = nums[i];
			TrieNode *curr = head;
			int currXOR = 0;

			for (int j = 31; j >= 0; j--) {

				int bit = (value >> j) & 1;

				if (bit == 0) {
					if (curr->right) {
						currXOR += 1 << j;
						curr = curr->right;
					}
					else {
						curr = curr->left;
					}
				}

				else {
					if (curr->left) {
						currXOR += 1 << j;
						curr = curr->left;
					}
					else {
						curr = curr->right;
					}
				}

			}

			maXOR = max(maXOR, currXOR);
		}
		return maXOR;
	}

	int findMaximumXOR(vector<int>& nums) {
		TrieNode *head = new TrieNode();
		for (int i = 0; i < nums.size(); i++) {
			insertNode(nums[i], head);
		}

		return findMaximumXORHelper(nums, head, nums.size());
	}
};
