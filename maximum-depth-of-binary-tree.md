## Maximum Depth of Binary Tree



计算二叉树的深度

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
	int maxDepth(TreeNode* root) {
		if (root == NULL)
			return 0;
		else
		{
			//return maxDepth(root->left) > maxDepth(root->right) ? maxDepth(root->left) + 1 : maxDepth(root->right) + 1;
			return max(maxDepth(root->left),maxDepth(root->right))+1;
		}
	}
	
	//创建二叉树
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
	Solution solution;
	TreeNode *T, *N;
	int data[] = { 1, 2, 3, 4, 5 }, data2[] = { 1, 2, 3, 4, 5 };
	solution.createTree(T, data, 5, 0);
	solution.maxDepth(T);
}
```


很可惜的是这个方法超时了，使用max巧妙避过超时问题,

* 这是一个比较左子树与右子数长度的问题，找到深度大的那一边+根节点就是当前二叉树最大的深度
* 这是一种深度优先搜索，简称dfs


## 一下是另一种方法，采用bfs，广度优先搜索

```
int maxDepth(TreeNode *root)
{
    if(root == NULL)
        return 0;
    
    int res = 0;
    queue<TreeNode *> q;
    q.push(root);
    while(!q.empty())
    {
        ++ res;
        for(int i = 0, n = q.size(); i < n; ++ i)
        {
            TreeNode *p = q.front(); // 返回队列中头部数据
            q.pop();
            
            if(p -> left != NULL)
                q.push(p -> left);
            if(p -> right != NULL)
                q.push(p -> right);
        }
    }
    
    return res;
}

* 这种方法使用了入队和出队，将根的两个孩子入队，根出队
```

