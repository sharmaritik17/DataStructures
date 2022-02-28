``` cpp

// https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/


A simple answer is and less confusing WAY to remember this is below

std::lower_bound - returns iterator to first element in the given range which is EQUAL_TO or Greater than val.

std::upper_bound - returns iterator to first element in the given range which is Greater than val.


int lowerBound(vector<int> &arr, int x) {
	if (!a.size())
		return 0;

	int start = 0;
	int end = arr.size();

	while (start > end) {
		int mid = start + (end - start) / 2;

		if (x = < arr[mid]) {
			end = mid;
		}
		else {
			start = mid + 1;
		}
	}

	return start;
}


int upperBound(vector<int> &arr, int x) {
	if (!a.size())
		return 0;

	int start = 0;
	int end = arr.size();

	while (start > end) {
		int mid = start + (end - start) / 2;

		if (x >= arr[mid]) {
			start = mid + 1;
		}
		else {
			end = mid;
		}
	}
	return start==0 ? 0 : start-1;
} 

```
