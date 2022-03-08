Deletion Distance
The deletion distance of two strings is the minimum number of characters you need to delete in the two strings in order to get the same string. For instance, the deletion distance between "heat" and "hit" is 3:

By deleting 'e' and 'a' in "heat", and 'i' in "hit", we get the string "ht" in both cases.
We cannot get the same string from both strings by deleting 2 letters or fewer.
Given the strings str1 and str2, write an efficient function deletionDistance that returns the deletion distance between them. Explain how your function works, and analyze its time and space complexities.

Examples:

input:  str1 = "dog", str2 = "frog"
output: 3

input:  str1 = "some", str2 = "some"
output: 0

input:  str1 = "some", str2 = "thing"
output: 9

input:  str1 = "", str2 = ""
output: 0
Constraints:

[input] string str1
[input] string str2
[output] integer



``` cpp
#include <iostream>
#include <string>
#include<vector>

using namespace std;

int deletionDistance( const string& str1, const string& str2 ) 
{
  // your code goes here
  int m = str1.size(),n = str2.size();
  
  vector<vector<int>> dp(m+1,vector<int>(n+1,0));
  
   for(int i=0;i<=m;i++) dp[i][0]=i;
  
  for(int i=0;i<=n;i++) dp[0][i]=i;
  
  for(int i=1;i<=m;i++){
    for(int j=1;j<=n;j++){
      if(str1[i-1]==str2[j-1]){
        dp[i][j] = dp[i-1][j-1];
      }
      else{
        dp[i][j] = min(1+dp[i-1][j],min(dp[i-1][j-1]+2,1+dp[i][j-1]));
      }
    }
  }
  return dp[m][n];
}

int main() {
  return 0;
}

/*

h -- h
e -- i
a -- t
t -- ''

--> 1st --- hat -- hit
--> 2nd -- heat -- ht
--> both chars -- hat -- ht

m*n

m = len of str1
n = len of str2

m=0, ans=n vice versa


h
hi

h  "" hi
h
he
h
    h i t   
  0 1 2 3
h 1 0 1 2
e 2 1
a 3
t 4

*/
