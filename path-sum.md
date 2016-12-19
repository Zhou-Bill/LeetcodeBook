## Path Sum

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

For example:
Given the below binary tree and sum = 22,

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
```

return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.

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
	bool hasPathSum(TreeNode* root, int sum) {
		if (root == NULL)
			return false;
		if (root->val == sum &&  root->left == NULL && root->right == NULL)
			return true;
		return hasPathSum(root->left, sum - root->val) || hasPathSum(root->right, sum - root->val);
			
	}
	void CreateTree(TreeNode* &T, int data[], int length, int index){
		if (index > length){
			return;
		}
		T = new TreeNode(data[index]);
		CreateTree(T->left, data, length, index * 2 + 1);
		CreateTree(T->right, data, length, index * 2 + 2);

	}
};

int main()
{
	int data[] = { 5, 4, 8, 11, NULL, 13, 4, 7, 2, NULL, NULL, NULL, 1 };
	Solution solution;
	TreeNode* T;
	solution.CreateTree(T, data, 13, 0);
	cout<<solution.hasPathSum(T, 22);
}
```

* 我们只需要判断一下当前节点的值是否等于sum-之前的值，如果是，那么就return true,当然这里有个前提,就是它的左右子节点都为空，