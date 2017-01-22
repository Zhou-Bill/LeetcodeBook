## Balanced Binary Tree

>Given a binary tree, determine if it is height-balanced.

>For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

* 高度平衡树定义为左右子树的高度相差不大于1

```
#include<iostream>
#include<algorithm>
using namespace std;

struct TreeNode {
	int val;
	TreeNode *left;
	TreeNode *right;
	TreeNode(int x) : val(x), left(NULL), right(NULL) {}
	
};

class Solution {
public:
	bool isBalanced(TreeNode* root) {
		if (!root)
			return 1;
		int k = abs(getHeight(root->left) - getHeight(root->right)) > 1 ? 0 : 1;
		int result = k*isBalanced(root->left)*isBalanced(root->right);
		return result;
	}
	int getHeight(TreeNode* root){
		if (!root)
			return 0;
		return max(getHeight(root->left) + 1, getHeight(root->right) + 1);
	}
	void createTree(TreeNode* &root, int a[], int length, int index){
		if (index > length)
			return;
		root = new TreeNode(a[index]);
		createTree(root->left, a, length, 2 * index + 1);
		createTree(root->right, a, length, 2 * index + 2);
	}
};

int main()
{
	int data[] = { 1, 2, 3, 4, 5, 6, 7 };
	TreeNode* T;
	Solution solution;
	solution.createTree(T,data,7,0);
}
```

> 思想

* 我通过计算左右子树的最大深度，然后相减 比较一下是否大于1 取0/1；
* 然后再递归左右子树，得到的值都乘起来，得到的就是0/1了；
* 有两个递归，时间很慢