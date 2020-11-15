``` cpp
Given two strings s and t of lengths m and n respectively, find the Edit Distance between the strings.
Edit Distance of two strings is minimum number of steps required to make one string equal to other. 
In order to do so you can perform following three operations only :


1. Delete a character

2. Replace a character with another one

3. Insert a character

/*********************************************************************************************************/ //exponential

int editDistance(string s, string t){
    if(s.size()==0 || t.size()==0){
        return max(s.size(),t.size());
    }
    

    if(s[0]==t[0])
      return editDistance(s.substr(1),t.substr(1));
    
    int x = 1 + editDistance(s.substr(1),t);  
    int y = 1 + editDistance(s,t.substr(1));
    int z = 1 + editDistance(s.substr(1),t.substr(1));
    
    int ans = min(x,min(y,z));
    
    return ans;

}

/*********************************************************************************************************/ //memoization
int editDistance(string s, string t, int **dp) {
	int m = s.size();
	int n = t.size();

	//base case
	if (m == 0 || n == 0) //dp filler
		return max(m, n);

	if (dp[m][n] != -1)
		return dp[m][n];

	if (s[0] == t[0])
		return editDistance(s.substr(1), t.substr(1), dp);

	int x = 1 + editDistance(s.substr(1), t, dp);             // remove
	int y = 1 + editDistance(s, t.substr(1), dp);            //insert
	int z = 1 + editDistance(s.substr(1), t.substr(1), dp); //replace

	dp[m][n] = min(x, min(y, z));

	return dp[m][n];
}

int editDistance(string s, string t) {
	int m = s.size();
	int n = t.size();

	int **dp = new int*[m + 1];

	for (int i = 0; i <= m; i++) {
		dp[i] = new int[n + 1];
		for (int j = 0; j <= n; j++) {
			dp[i][j] = -1;
		}
	}

	return editDistance(s, t, dp);
}


/*********************************************************************************************************/ //dynamic programming
int editDistance(string s, string t) {
	int m = s.size();
	int n = t.size();

	int **dp = new int*[m + 1];

	for (int i = 0; i <= m; i++) {
		dp[i] = new int[n + 1];
	}

	for (int i = 0; i <= m; i++)
		dp[i][0] = i;
	for (int j = 1; j <= n; j++)
		dp[0][j] = j;

	for (int i = 1; i <= m; i++) {
		for (int j = 1; j <= n; j++) {
			if (s[m - i] == t[n - j])
				dp[i][j] = dp[i - 1][j - 1];
			else {
				int x = 1 + dp[i - 1][j];
				int y = 1 + dp[i][j - 1];
				int z = 1 + dp[i - 1][j - 1];

				dp[i][j] = min(x, min(y, z));
			}
		}
	}

	return dp[m][n];
}


```
