``` cpp
https://leetcode.com/problems/rotate-image/

1 ---- a) reverse b) transpose

class Solution {
public:
	void rotate(vector<vector<int>>& matrix) {
		reverse(matrix.begin(), matrix.end());
        
		int n = matrix.size();
		for (int i = 0; i < n; i++)
			for (int j = 0; j < i; j++)
				swap(matrix[i][j], matrix[j][i]);
        
	}
};

2 ----- a) transposse b) reverse rows one by one

class Solution {
public:
	void rotate(vector<vector<int>>& matrix) {
		int n = matrix.size();
		for (int i = 0; i < n; i++)
			for (int j = 0; j < i; j++)
				swap(matrix[i][j], matrix[j][i]);

		for (int i = 0; i < n; i++) {
			reverse(matrix[i].begin(), matrix[i].end());
		}
        
	}
};


3 --- ring by ring

class Solution {
public:
	void rotate(vector<vector<int>>& matrix) {
		int n = matrix.size();

		for(int i=0;i<(n+1)/2;i++){ // (n+1)so will work when size is odd
			for(int j = 0;j<n/2;j++){
				// bottom left
				int save = matrix[n-j-1][i];
				matrix[n-j-1][i] = matrix[n-i-1][n-j-1]; // bottom right
				matrix[n-i-1][n-j-1] = matrix[j][n-i-1]; // top right
				matrix[j][n-i-1] = matrix[i][j]; // top left
				matrix[i][j] = save;
			}
		}
	}
};

anticlockwise will be opposite of all above what we are doing
