https://leetcode.com/problems/maximal-rectangle/

https://leetcode.com/problems/maximal-rectangle/discuss/29172/my-on3-solution-for-your-reference
``` cpp
------------------------------------------------------------------------------
class Solution {
public:
 	int largestArea(vector<int>&histogram) {
		vector<int> left, right;
		stack<int> s;

		for (int i = 0; i < n; i++) {
			while (!s.empty() && histogram[s.top()] >= histogram[i]) {
				s.pop();
			}

			if (s.empty()) {
				left.push_back(-1);
			}
			else {
				left.push_back(s.top());
			}

			s.push(i);
		}

		while (!s.empty()) {
			s.pop();
		}

		for (int i = n - 1; i >= 0; i--) {
			while (!s.empty() && histogram[s.top()] >= histogram[i]) {
				s.pop();
			}

			if (s.empty()) {
				right.push_back(n);
			}
			else {
				right.push_back(s.top());
			}

			s.push(i);
		}

		int max_area = 0;
		int calc_area = 0;
		for (int i = 0; i < n; i++) {
			calc_area = histogram[i] * (right[n - 1 - i] - left[i] - 1);
			max_area = max(max_area, calc_area);
		}

		return max_area;
	}
    int maximalRectangle(vector<vector<char>>& matrix) {
        int m=matrix.size();
        if(m==0) return 0;
        int n=matrix[0].size(), result=0;
        vector<int> histogram(n, 0);
        
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                if(matrix[i][j]=='1')
                    histogram[j]+=1;
                else
                    histogram[j]=0;
            }
            
            result = max(result, largestArea(histogram));
            //cout<<result<<" ";
        }
        return result;
    }
};




class Solution {
public:
    int maximalRectangle(vector<vector<char> > &matrix) {
        int num_i=matrix.size();
        if (num_i==0) return 0;
        int num_j=matrix[0].size();
        if (num_j==0) return 0;
        vector<vector<int>> max_x(num_i,vector<int>(num_j,0));  //number of consecutive 1s to the left of matrix[i][j], including itself
       
        int area=0;
        for (int i=0;i<num_i;i++){
            for (int j=0;j<num_j;j++){
                if (matrix[i][j]=='1'){
                    if (j==0) max_x[i][j]=1;
                    else max_x[i][j]=max_x[i][j-1]+1;
                    int y=i,count=1;
                    int x=num_j;
                    while((y>=0)&&(matrix[y][j]=='1')){
                        x=min(x, max_x[y][j]);
                        area=max(area,x*(count));
                        y--; count++;
                    } 
                }
            }
        }
        

        
        return area;
        
        
    }
};
