``` cpp

// https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

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
