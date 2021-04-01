https://www.geeksforgeeks.org/subarray-xor-less-k/

``` cpp //need to correct ryt now
#include<bits/stdc++.h>
using namespace std;
class TrieNode{
    public:
    TrieNode* left;
    TrieNode* right;
};

void insert(int n, TrieNode* head){
    
    TrieNode* curr = head;
    for(int i = 31; i >= 0; i--){
        int b = (n >> i) & 1;
        
        if(b == 0){
            if(!curr -> left){
                curr -> left = new TrieNode();
            }
            curr = curr -> left;
        }else{
            if(!curr -> right){
                curr -> right = new TrieNode();
            }
            curr = curr -> right;
        }
    }
}

int countLeaf(TrieNode* head){
    
    if(head == NULL){
        return 0;
    }
    
    if(head -> left == NULL && head -> right == NULL){
        return 1;
    }
    
    int a = countLeaf(head -> left); 
    int b = countLeaf(head -> right);
    return a + b;
}

int kXOR(TrieNode* head, int value, int k){
    
    int curr_ans = 0;
    TrieNode* curr = head;
    for(int i = 31; i >= 0 && curr != NULL; i--){
        int a = (value >> i) & 1;
        int b = (k >> i) & 1;
        if(a == 1 && b == 1){
            curr_ans += countLeaf(curr -> right);
            curr = curr -> left;
        }
        else if(a == 1 && b == 0){
            curr = curr -> right;
        }
        else if(a == 0 && b == 1){
            curr_ans += countLeaf(curr -> left);
            curr = curr -> right;
        }
        else if(a == 0 && b == 0){
            curr = curr -> left;
        }
    }
    return curr_ans;
}

int main() {

    int t;
    cin >> t;
    while(t--){
    int n, k;
      cin >> n >> k;
      int* arr = new int[n];
      for(int i = 0; i < n; i++){
          cin >> arr[i];
      }
      
      int ans = 0;
        int curr_xor = 0;
      TrieNode* head = new TrieNode();
      for(int i = 0; i < n; i++){
          insert(curr_xor, head);
            curr_xor = curr_xor ^ arr[i];
          ans += kXOR(head, curr_xor, k);
      }
      cout << ans << endl;
    }
}
