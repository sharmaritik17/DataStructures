https://leetcode.com/problems/find-the-most-competitive-subsequence/

https://leetcode.com/problems/find-the-most-competitive-subsequence/discuss/952934/C%2B%2B-O(n)-sliding-window-mono-sequence-%2B-in-place-solution



``` cpp
class Solution {
  void fillVector(stack<int> stack,vector<int> &ans,int i){
    while(stack.size()){
      ans[i--] = stack.top();
      stack.pop();
    }
  }
public:
    vector<int> mostCompetitive(vector<int>& nums, int k) {
        stack<int> stack;
        vector<int>ans(k);
        int n = nums.size();

        for(int i=0;i<n;i++){
          while(!stack.empty() && stack.top()>nums[i] && stack.size()-1 + n - i >=k){
            stack.pop();
          }

          if(stack.size()<k){
            stack.push(nums[i]);
          }
        }

      fillVector(stack,ans,k-1);
        return ans;
    }
};
