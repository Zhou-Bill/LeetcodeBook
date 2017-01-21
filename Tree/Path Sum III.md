### Path Sum III

>You are given a binary tree in which each node contains an integer value.

> Find the number of paths that sum to a given value.

> The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

> The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```
树的值相加得到target值，问有多少种路径


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
	int pathSum(TreeNode* root, int sum) {
		if (root == NULL)
			return 0;
	
		int result = targetSum(root, 0, sum) + pathSum(root->left, sum) + pathSum(root->right, sum);
	
		return result;
	}
	int targetSum(TreeNode* root, int sum, int target){
		if (!root)
			return 0;

		if (root->val + sum == target){
			return 1;
		}
		else
		{
			return targetSum(root->left, sum + root->val, target) + targetSum(root->right, sum + root->val, target);
		}
	}
	void createTree(TreeNode* &root, int a[], int length, int index)
	{
		if (index > length){
			return;
		}
		root = new TreeNode(a[index]);
		createTree(root->left, a, length, index * 2 + 1);
		createTree(root->right, a, length, index * 2 + 2);

	}
};

int main()
{
	int data[] = { -1, -2, -3, 1, 3, -2, 0, -1 };
	TreeNode* T;
	Solution solution;
	solution.createTree(T,data,8,0);
	solution.pathSum(T,-1);
}
```

* 上面的代码是本正确的，因为在targetSum 的

`if (root->val + sum == target){return 1;}` 这里面如果等于了target，那么就不继续往下做了
* 加入数据是[-1, -2, -3, 1, 3, -2, 0, -1],target = -1那么就会少了一种，
* 以上面得到的结果是3种，事实上答案应该是4种的
  * 1->-2
  * -2 -> 1
  * -1
  * **1->-2->1->-1** 上面正是少了这一种
  
* 代码改进
 
 ```
 int targetSum(TreeNode* root, int sum, int target){
	if (!root)
		return 0;
	return ((root->val + sum == target)+targetSum(root->left, sum + root->val, target) + targetSum(root->right, sum + root->val, target);	
	}
 ```
 
 这样就不会停止了
 * 要说一下就是这里使用的是两个递归函数一个是pathSum
，另一个是targetSum函数
 * **pathSum** 作为树的子节点作为根去调用targetsum