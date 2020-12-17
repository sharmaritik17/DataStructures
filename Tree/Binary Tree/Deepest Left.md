https://www.geeksforgeeks.org/deepest-left-leaf-node-in-a-binary-tree/
``` cpp


void helper(BinaryTreeNode<int>* root, bool isLeft, int &max_level, int currlevel, int &value) {
	if (!root)
		return;

	if (isLeft && !root->left && !root->right && currlevel >= max_level) {
		if (currlevel != max_level) {
			max_level = currlevel;
			value = root->data;
		}
		else
			value = max(value, root->data);
	}

	helper(root->left, true, max_level, currlevel + 1, value);
	helper(root->right, false, max_level, currlevel + 1, value);
}

int solve(BinaryTreeNode<int>* root) {
	int value = -1;
    int max_level = 0;
	helper(root, false, max_level, 0, value);

	return value;
}
