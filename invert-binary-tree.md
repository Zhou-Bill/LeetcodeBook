## Invert Binary Tree

Invert a binary tree.
```

     4
   /   \
  2     7
 / \   / \
1   3 6   9
```
to
```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```
## 做法是 左右子树互换

```
#include<iostream>
using namespace std;

struct TreeNode {
	int val;
	TreeNode *left;
	TreeNode *right;
	TreeNode(int x) : val(x), left(NULL), right(NULL) {}
	
};

class Solution {
public:
	TreeNode* invertTree(TreeNode* root) {
		if (root == NULL)
			return NULL;
		TreeNode *tempRoot = root->left;
		root->left = invertTree(root->right);
		root->left = invertTree(tempRoot);
		return root;
	}

	void createTree(TreeNode* &T, int a[], int length, int index){
		if (length < index)
			return;
		T = new TreeNode(a[index]);
		createTree(T->left, a, length, 2 * index + 1);
		createTree(T->right, a, length, 2 * index + 2);

	}
};

int main()
{
	int data[5] = { 1, 2, 3, 4, 5 };
	TreeNode* T;
	Solution solution;
	solution.createTree(T, data, 5, 0);
	solution.invertTree(T);
}
```