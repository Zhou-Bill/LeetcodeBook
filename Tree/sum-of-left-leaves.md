## Sum of Left Leaves

> Find the sum of all left leaves in a given binary tree.

```
    3
   / \
  9  20
    /  \
   15   7

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
```

找到所有左叶子然后相加得到的和

**注意** ： 这里所说的左叶子是有规定的

1. 左叶子没有左孩子和右孩子，之前一直忽略以为只要在左边的都是左叶子，但其实并不是
1. 所以我们从根节点开始 判断一下**有没有左孩子**，然后**左孩子有没有它的左、右孩子**
1. 从上面两点得到`int result = (root->left!= NULL && root->left->left == NULL && root->left->right == NULL)? root->left->val:0;`

```
class Solution {
public:
	int sumOfLeftLeaves(TreeNode* root) {
		if (root == NULL)
			return 0;
        int result = (root->left!= NULL && root->left->left == NULL && root->left->right == NULL)? root->left->val:0;
		return result+sumOfLeftLeaves(root->left) + sumOfLeftLeaves(root->right);

	}

	void createTree(TreeNode* &root, int a[], int length, int index){
		if (index > length)
			return;
		root = new TreeNode(a[index]);
		createTree(root->left, a, length, 2 * index + 1);
		createTree(root->right, a, length, 2 * index + 2);
	}
};
```