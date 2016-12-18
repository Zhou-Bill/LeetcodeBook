## Symmetric Tree

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

> For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

```
But the following [1,2,2,null,3,null,3] is not:
    1
   / \
  2   2
   \   \
   3    3
```

```
#include<iostream>
#include<vector>
using namespace std;

struct TreeNode {
	int val;
	TreeNode *left;
	TreeNode *right;
	TreeNode(int x) : val(x), left(NULL), right(NULL) {
	}
};

class Solution {
public:
	bool isSymmetric(TreeNode* root) {
		// 中序遍历
		vector<int> data;
		in_order(root,data);
		int length = data.size();
		for (int i = 0; i < data.size()/2; i++){
			if (data[i] != data[length-1 - i]){
				return false;
			}
		}

		return true;
	}
	void in_order(TreeNode* root,vector<int> &a)
	{
		if (root == NULL)
			return;

		in_order(root->left,a);
		a.push_back(root->val);
		in_order(root->right,a);
	}


	void createTree(TreeNode* &T, int a[], int length, int index){

		if (index >= length)
			return;
		T = new TreeNode(a[index]);
		createTree(T->left, a, length, 2 * index + 1);
		createTree(T->right, a, length, 2 * index + 2);

	}
};

int main()
{
	int array[] = { 1, 2, 3, 3, NULL, 2, NULL };
	Solution solution;
	TreeNode *T, *N;
	solution.createTree(T, array, 7, 0);
	solution.isSymmetric(T);
}

```

在vs中可以通过，但在leecode上面不可以，在leecode上null,直接去掉了，所以大部分成功，但少量不成功

