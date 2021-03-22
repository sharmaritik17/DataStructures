https://leetcode.com/problems/evaluate-reverse-polish-notation/

https://leetcode.com/problems/evaluate-reverse-polish-notation/discuss/1121830/Simple-or-C%2B%2B-or-Stack

``` cpp

class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> stack;

        for(auto curr:tokens){
          if(curr=="+"){
            int x = stack.top(); stack.pop();
            int y = stack.top(); stack.pop();
            stack.push(x+y);
          }
          else if(curr=="-"){
            int x = stack.top(); stack.pop();
            int y = stack.top(); stack.pop();
            stack.push(y-x);
          }
          else if(curr=="*"){
            int x = stack.top(); stack.pop();
            int y = stack.top(); stack.pop();
            stack.push(x*y);
          }
          else if(curr=="/"){
            int x = stack.top(); stack.pop();
            int y = stack.top(); stack.pop();
            stack.push(y/x);
          }
          else{
            stack.push(stoi(curr));
          }
        }
        return stack.top();
    }
};
