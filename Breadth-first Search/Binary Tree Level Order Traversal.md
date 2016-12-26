## Binary Tree Level Order Traversal


> Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

> For example:
Given binary tree [3,9,20,null,null,15,7],

```
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:

```
[
  [3],
  [9,20],
  [15,7]
]
```

这道题使用广度优先遍历，广度优先遍历:利用的是队列的出队和入队

* 根据子元素是否在队列，循环这一层，push_back 到 vector

```
#include<iostream>
#include<vector>
#include<queue>
using namespace std;


struct TreeNode {
	int val;
	TreeNode *left;
	TreeNode *right;
	TreeNode(int x) : val(x), left(NULL), right(NULL) {}
	
};

class Solution {
public:
	vector<vector<int>> levelOrder(TreeNode* root) {
		queue<TreeNode *> q;
		vector<vector<int>> result;
		if (!root) return result;

		q.push(root);
		while (!q.empty())
		{

			vector<int> data;
			for (int i = 0, n = q.size(); i < n; i++){
				TreeNode* Node = q.front();
				data.push_back(Node->val);
				q.pop();
				if (Node->left != NULL)
					q.push(Node->left);
				if (Node->right != NULL)
					q.push(Node->right);
			}
			result.push_back(data);
			
		}
		return result;
	}

	void createTree(TreeNode* &T, int a[], int length, int index)
	{
		if (index > length)
			return;
		T = new TreeNode(a[index]);
		createTree(T->left, a, length, 2 * index + 1);
		createTree(T->right, a, length, 2 * index + 2);
	}
};

int main()
{
	int data[] = { 1, 2, 3, 4, 5, 6 };
	TreeNode* T;
	Solution solution;
	solution.createTree(T,data,6,0);
	solution.levelOrder(T);
}
```