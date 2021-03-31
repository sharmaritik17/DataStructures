https://practice.geeksforgeeks.org/problems/maximum-rectangular-area-in-a-histogram/0
```cpp
/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/
#include  <bits/stdc++.h>
#define ii      int
#define ll      long long
#define mod     1000000009
#define FIO     ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define nul     NULL
#define  z "\n"
#include <iostream>
#include <vector>
#include <climits>
#define ff first
#define ss second
using namespace std;
//#include "ComplexNumbers.h"
/* ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*/
ll getMaxArea(ll *arr,ll n){
     vector<ll> left,right;
     stack<ll> s;

     for(ll i=0;i<n;i++){
     	while(!s.empty() && arr[s.top()]>=arr[i]){
     		s.pop();
     	}

     	if(s.empty()){
     		left.push_back(-1);
     	}
     	else{
     		left.push_back(s.top());
     	}

     	s.push(i);
     }

       while(!s.empty()){
      	s.pop();
        }

      for(ll i=n-1;i>=0;i--){
      	while(!s.empty() && arr[s.top()]>=arr[i]){
      		s.pop();
      	}

      	if(s.empty()){
      		right.push_back(n);
      	}
      	else{
      		right.push_back(s.top());
      	}

      	s.push(i);
      }

      ll max_area = 0;
      ll calc_area = 0;
      for(ll i=0;i<n;i++){
      	calc_area = arr[i]*(right[n-1-i] - left[i]-1);
      	max_area = max(max_area,calc_area);
      }

      return max_area;
}
int main(){
	ll ntc;
	cin>>ntc;
	while(ntc--){
		ll n;
		cin>>n;
      ll arr[n];
      for(ll i=0;i<n;i++){
      	cin>>arr[i];
      }
      cout<<getMaxArea(arr,n)<<z;
	}

	return 0;
}


/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/  must check
https://leetcode.com/problems/largest-rectangle-in-histogram/


/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/ monotonically stack
// take example 2 3 4 5 for better understanding
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {

        stack<int> st;
        int n = heights.size();
        int max_area = 0;

        if (!n)
            return 0;

        // to wrap up arear for last element in height array
        heights.push_back(0);


        for (int i = 0; i < heights.size(); i++) {

            while (!st.empty() && heights[st.top()] > heights[i]) {
                int top_element = heights[st.top()];
                st.pop();

                // take an example with code since it's zero based indexing
                int ran = st.empty() ? -1 : st.top(); // in case we reached at the end of histogram
                int width = i - ran - 1; //-1 bcs we want to skip current(i) index cnadidiate
                max_area = max(max_area, (top_element * width));
            }

            st.push(i);
        }

        return max_area;
    }
};
