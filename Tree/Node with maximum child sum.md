``` cpp
Node with maximum child sum
Send Feedback
Given a generic tree, find and return the node for which sum of its data and data of all its child nodes is maximum. In the sum, data of the node and data of its immediate child nodes has to be taken.
Input format :
The first line of input contains data of the nodes of the tree in level order form. The order is: data for root node, number of children to root node, data of each of child nodes and so on and so forth for each node. The data of the nodes of the tree is separated by space. 
Output format :
The first and only line of output contains the data of the node with maximum sum, as described in the task.
Constraints:
Time Limit: 1 sec
Sample Input 1 :
5 3 1 2 3 1 15 2 4 5 1 6 0 0 0 0
Sample Output 1 :
1


//DFS manner -- intutive
void maxSumNodeHelper(TreeNode<int> *root, TreeNode<int> *&saveNode, int &saveMaxSum) {
	int currSum = root->data;
	for (int i = 0; i < root->children.size(); i++) {
		currSum += root->children[i]->data;
		maxSumNodeHelper(root->children[i], saveNode, saveMaxSum);
	}

	if (currSum > saveMaxSum) {
		saveNode = root;
		saveMaxSum = currSum;
	}
	return;
}
TreeNode<int>* maxSumNode(TreeNode<int> *root) {
	TreeNode<int> *saveNode = NULL;
	int saveMaxSum = -1;
	maxSumNodeHelper(root, saveNode, saveMaxSum);
	return saveNode;
}

//worst complexity
TreeNode<int>* maxSumNode(TreeNode<int> *root) {
	if (!root)
		return root;

	TreeNode<int>* ans = root;
	int sum = root->data;

	for (int i = 0; i < root->children.size(); i++) {
		sum += root->children[i]->data;
	}

	for (int i = 0; i < root->children.size(); i++) {
		TreeNode<int> *child_ans = maxSumNode(root->children[i]);

		int child_sum = child_ans->data;
		for (int i = 0; i < child_ans->children.size(); i++) {
			child_sum += child_ans->children[i]->data;
		}

		if (child_sum > sum) {
			sum = child_sum;
			ans = child_ans;
		}

	}

	return ans;
}

//by DP
#include<climits>
pair<TreeNode<int>*, int> helper_maxSumNode(TreeNode<int> *root) {
	if (root == NULL) {
		pair<TreeNode<int>*, int> res;
		res.first = NULL;
		res.second = INT_MIN;
		return res;
	}

	pair<TreeNode<int>*, int> res;
	int sum = root->data;
	for (int i = 0; i < root->children.size(); i++) {
		sum += root->children[i]->data;
	}
	res.first = root;
	res.second = sum;

	for (int i = 0; i < root->children.size(); i++) {
		pair<TreeNode<int>*, int> child = helper_maxSumNode(root->children[i]);
		if (child.second > res.second) {
			res = child;
		}
	}

	return res;
}

TreeNode<int>* maxSumNode(TreeNode<int> *root) {
	return helper_maxSumNode(root).first;
}
