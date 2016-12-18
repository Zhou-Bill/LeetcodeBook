## Minimum Depth of Binary Tree

> 找到二叉树的最小深度

* 这道题其实跟找二叉树的最大深度基本一样，但是要考虑这种情况

```
    1
   / 
  2
 /
3
```

即**右子树** 或 **左子树** 为NULL 的时候

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
	int minDepth(TreeNode* root) {
		if (root == NULL)
			return 0;
		if (root->left == NULL)
			return minDepth(root->right) + 1;
		else if (root->right ==NULL)
		{
			return minDepth(root->left)+1;
		}
		else
		{
			return min(minDepth(root->left), minDepth(root->right)) + 1;
		}
	}

	void createTree(TreeNode* &T, int a[], int length, int index){
		if (index > length)
			return;
		T = new TreeNode(a[index]);
		createTree(T->left, a, length, 2 * index + 1);
		createTree(T->right, a, length, 2 * index + 2);

	}
};

int main()
{
	int array[] = { 1, 2, 3, 4, 5 };
	Solution solution;
	TreeNode* T;
	solution.createTree(T,array,5,0);
	cout<<solution.minDepth(T);

}
```

* 所以加了一层判断，判断左子树是否为空，为空则返回右子树长度