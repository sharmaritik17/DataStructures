``` cpp
problem----- shorturl.at/eoz15
/*++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*/
https://www.geeksforgeeks.org/the-celebrity-problem/
/*++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*/


stack-based approach
/*++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*/

class Solution {
public:
	int celebrity(vector<vector<int> >& M, int n) {
		// code here
		int siz = M.size();

		if (siz < 1)
			return -1;
		stack<int> s;

		for (int i = 0; i < siz; i++)
			s.push(i);

		while (s.size() >= 2) {
			int i = s.top(); s.pop();
			int j = s.top(); s.pop();

			if (M[i][j]) {
				s.push(j);
			}
			else {
				s.push(i);
			}
		}
		int potential = s.top();
		s.pop();

		for (int i = 0; i < siz; i++) {
			if (i != potential && (M[potential][i] || !M[i][potential])) {
				return -1;
			}
		}
		return potential;
	}
};
