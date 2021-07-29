``` cpp
#include<iostream>
using namespace std;

template<typename T>
class BinaryTreeNode{
    public:
    T data;
    BinaryTreeNode<T> *left;
    BinaryTreeNode<T> *right;   
    BinaryTreeNode(T data){
        this->data = data;
        left = NULL;
        right = NULL;
    }
};

BinaryTreeNode<int>* takeInput(){
    int rootData;
    cin>>rootData;
    if(rootData==-1){
        return NULL;
    }

    BinaryTreeNode<int> *root = new BinaryTreeNode<int>(rootData);
    queue<BinaryTreeNode<int>*> pendingNodes;
    pendingNodes.push(root);

    while(pendingNodes.size()){
        auto current_node = pendingNodes.front();
        pendingNodes.pop();

        int leftData;
        cin>>leftData;
        if(leftData!=-1){
            BinaryTreeNode<int> *leftchild = new BinaryTreeNode<int>(leftData);
            current_node->left = leftchild;
            pendingNodes.push(leftchild);
        }
        int rightData;
        cin>>rightData;
        if(rightData!=-1){
            BinaryTreeNode<int> *rightChild = new BinaryTreeNode<int>(rightData);
            current_node->right = rightChild;
            pendingNodes.push(rightChild);
        }
    }
    return root;
}

void printTree(BinaryTreeNode<int> *root){
    if(!root){
        return;
    }
    cout<<root->data<<endl;
    printTree(root->left);
    printTree(root->right);
}

int main(){
      BinaryTreeNode<int> *root = takeInput();
      printTree(root);
      return 0;
}

/*
1 2 3 4 5 6 7 -1 -1 -1 -1 -1 -1 -1 -1

       1
    2    3
4     5  6  7
*/
```
