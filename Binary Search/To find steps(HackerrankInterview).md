``` cpp
https://www.geeksforgeeks.org/steps-to-reduce-n-to-zero-by-subtracting-its-most-significant-digit-at-every-step/
/*!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!*/
Task Description
In this problem, you are required to perform some
operations on an integer repeatedly. More precisely, for
a given integer you repeatedly subtract the leading non-

zero digit from it till it becomes zero.
For example, suppose the integer given is n = 13, the

process goes as follows:

1. The leading non-zero digit is 1, hence 13 - 1 = 12.
2. The leading non-zero digit is 1, hence 12 - 1 = 11.
3. The leading non-zero digit is 1, hence 11 - 1 = 10.
4. The leading non-zero digit is 1, hence 10 - 1 = 9.
5. The leading non-zero digit is 9, hence 9 - 9 = 0.

So for n = 13, we obtained a set of 6 distinct integers.
Given the number of distinct integers obtained in the
process, your task is to find the maximum possible
integer you can start with.

Function Description
Complete the function maxinteger in the editor below.
The function must return a single integer denoting
maximum possible integer.
maxinteger has the following parameter(s):

/*!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!*/
int getFirst(int n) {
	while (n >= 10)
		n /= 10;
	return n;
}
bool isBigger(int mid,int k) {
	int cnt = 1;
	while (mid) {
		int s = getFirst(mid);
		mid = mid - s;
		cnt++;
	}
	return cnt<=k;
}

int32_t main()
{
    int num; cin >> num;
    int left = 0, right = 100000;
    //can be further optimized with stoll but this is also upto some extent(need to work with bits)
    while (left <= right)
    {
    	int mid = left + (right - left)/2;
        if(isBigger(mid,num)){ 
            left = mid+1; //greddily finding bigger
        }
        else{
            right = mid-1;
        }
    }

    cout << left-1 << '\n';

    return 0;
}

/*!!!!!!!!!!!!!!!!!!!!!!!!!!!!^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!*/

int f(int num)
{
    if (!num)
        return 1;

    if (num < 10)
        return 2;

    string tmp = to_string(num);
    int dig = tmp[0] - '0';

    tmp[0]--;

    for (int i = 1; i < tmp.size(); ++i)
        tmp[i] = '9';

    int smaller = stoll(tmp);
    int steps = (num - smaller + dig - 1) / dig; //ceil(num-smaller)/dig

    return steps + f(num - steps * dig);
}


int32_t main()
{
    FIO;

    int num; cin >> num;
    int beg = 0, end = inf, ans;

    while (beg <= end)
    {
        int mid = (beg + end) / 2;
        int steps = f(mid); //6

        if (steps <= num) // if greater than or equal to given 
            ans = mid, beg = mid + 1;

        else
            end = mid - 1;
    }

    if (f(ans) != num)
        ans = -1;

    cout << ans << '\n';

    return 0;
}
