https://leetcode.com/problems/making-a-large-island/
```
cpp
class Solution {
	int paintAdjLand(vector<vector<int>>& grid,int i,int j,int color,vector<int> &directions){
		if(i<0 || j<0 || i>=grid.size() || j>=grid[0].size() || grid[i][j]!=1) return 0;
		grid[i][j]  = color;
		int countArea = 1;
		for(int d=0;d<4;d++){
			countArea += paintAdjLand(grid,i+directions[d],j+directions[d+1],color,directions);
		}
		return countArea;
	}
public:
    int largestIsland(vector<vector<int>>& grid) {
        int m = grid.size(),n = grid[0].size();
        unordered_map<int,int> paintData;
        vector<int> directions({0,1,0,-1,0});
       //paint the seperate lands
        int color = 2;
        for(int i=0;i<m;i++){
        	for(int j=0;j<n;j++){
        		if(grid[i][j]==1){
        			int paintedLandSize = paintAdjLand(grid,i,j,color,directions);
        			paintData[color] = paintedLandSize;
        			color++;
        		}
        	}
        }

        //now find the longest area bridge point
        unordered_set<int> UniqueAdjLand;
        int finalSize = paintData[2] ,currLandSize=0;
        for(int i=0;i<m;i++){
        	for(int j=0;j<n;j++){
        		if(grid[i][j]==0){
        		 unordered_set<int> UniqueAdjLand;
        			currLandSize = 1;
        			for(int d=0;d<4;d++){ //on all four directions
        				int x = i+directions[d],y =j+directions[d+1];
        				if(x>=0 && y>=0 && x<m && y<n){
        					UniqueAdjLand.insert(grid[x][y]);
        				}
        			}
        			//add unique adjacent
        			for(auto &it:UniqueAdjLand) currLandSize += paintData[it];
                    
        			finalSize = max(finalSize,currLandSize);
        		}
        	}
        }
        return finalSize;
    }
};
/*
find shortest distance btw 0 and all (great in number)clusters having one 


-- find the max distance from 1 to 0

where we will push 1 onto queue then process all of them

just follow the path if grid having 1 else just save onto your computation


while doing so mantain area++ counter

*/
