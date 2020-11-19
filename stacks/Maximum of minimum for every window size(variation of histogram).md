``` cpp
https://www.geeksforgeeks.org/find-the-maximum-of-minimums-for-every-window-size-in-a-given-array/
/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/  variation of histogram----------------(hard problem)


#include  <bits/stdc++.h>
#define ii      int
#define ll      int
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
void help(int arr[],int n)
{
    stack<int> s;
    int left[n+1];
    int right[n+1];
    for(int i=0;i<n;i++)
    {
        left[i] = -1;
        right[i] = n;
    }
    for(int i=0;i<n;i++)
    {
        while(!s.empty()&&arr[s.top()]>=arr[i])
            s.pop();
        if(!s.empty())
            left[i]=s.top();
        s.push(i);
    }
    while(!s.empty())
        s.pop();
    for(int i=n-1;i>=0;i--)
    {
        while(!s.empty()&&arr[s.top()]>=arr[i])
            s.pop();
        if(!s.empty())
            right[i]=s.top();
        s.push(i);
    }
    int ans[n+1];
    for(int i=0;i<=n;i++)
    {
        ans[i]=0;
    }
    for(int i=0;i<n;i++)
    {
        int len = right[i]-left[i]-1;
        ans[len]=max(ans[len],arr[i]);
    }
    for(int i=n-1;i>=0;i--)
    {
        ans[i]=max(ans[i],ans[i+1]);
    }
    for(int i=1;i<=n;i++){
        cout<<ans[i]<<" ";
    }
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
      help(arr,n);
      cout<<z;
	}

	return 0;
}
