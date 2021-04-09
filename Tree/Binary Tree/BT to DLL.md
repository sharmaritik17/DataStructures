https://practice.geeksforgeeks.org/problems/binary-tree-to-dll/1#

``` cpp
class Solution
{
  void bToDLL_Helper(Node *root, Node *&head,Node *&prev){
    if(!root){
      return;
    }

    bToDLL_Helper(root->left,head,prev);

    if(head==NULL){
    	head = root;
    	prev = root;
    }
    else{
    	prev->right = root;
    	root->left = prev;
    	prev = root;
    }

    bToDLL_Helper(root->right,head,prev);
  }
    public: 
    //Function to convert binary tree to doubly linked list and return it.
    Node *bToDLL(Node *root)
    {
        Node *head=NULL,*prev = NULL;
        bToDLL_Helper(root,head,prev);
        return head;
    }
};
