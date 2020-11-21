``` cpp

https://leetcode.com/problems/product-of-array-except-self/


#define ll int
class Solution {
public:
	vector<int> productExceptSelf(vector<int>& nums) {
		int n = nums.size();

		if (!nums.size())
			return {};

		vector<ll> prefix(n, 1);
		vector<ll> suffix(n, 1);

		prefix[0] = 1;
		suffix[n - 1] = 1;

		for (int i = 1; i < n; i++) {
			prefix[i] = prefix[i - 1] * nums[i - 1];
		}

		for (int i = n - 2; i >= 0; i--) {
			suffix[i] = suffix[i + 1] * nums[i + 1];
		}
		vector<ll> result;

		for (int i = 0; i < n; i++) {
			result.push_back(prefix[i]*suffix[i]);
		}

		return result;
	}
};


#define ll  int
class Solution {
public:
	vector<int> productExceptSelf(vector<int>& nums) {

		int n = nums.size();
		if (!n)
			return {};

		vector<ll> product(n);

		product[0] = 1;

		for (int i = 1; i < n; i++) {
			product[i] = product[i - 1] * nums[i - 1];
		}

		ll temp = 1;
		for (int i = n - 1; i >= 0; i--) {
			product[i] *= temp;
			temp *= nums[i];
		}

		vector<ll> result;
		for (int i = 0; i < n; i++) {
			result.push_back(product[i]);
		}

		return result;
	}
};


