
https://leetcode.com/problems/remove-k-digits/


``` cpp
class Solution {
public:
    string removeKdigits(string num, int k) {
      int n = num.size();
      string res ="";
      stack<char> stack;

        for(int i=0;i<n;i++){

          while(!stack.empty() && num[i]<stack.top() && k){
            k--;
            stack.pop();
          }

          if(!stack.empty() || num[i]!='0'){
            stack.push(num[i]);
          }
        }
        
        //if no greater element was found on left like in 1234 k=3
        while(!stack.empty() && k){
          k--;
          stack.pop();
        }

        while(!stack.empty()){
          res = stack.top() + res;
          stack.pop();
        }

        res.empty()==1 ? res+="0" : res;
        
        return res;
    }
};
