``` cpp
// gfg problem

#define L long long
int findFloor(vector<long long> arr, long long n, long long x) {
	if (!arr.size())
		return -1;

	L save = -1;

	L start = 0;
	L end = arr.size() - 1;

	while (start <= end) {
		L mid = start + (end - start) / 2;

		if (arr[mid] == x) {
			return mid;
		}
		else if (arr[mid] > x) {
			end = mid - 1;
		}
		else { //if(arr[mid]<x)
			save = mid;
			start = mid + 1;
		}
	}

	return save;
}
```
