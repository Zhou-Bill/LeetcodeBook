## Jump Game

> Given an array of non-negative integers, you are initially positioned at the first index of the array.

>Each element in the array represents your maximum jump length at that position.

> Determine if you are able to reach the last index.

For example:
A = [2,3,1,1,4], return true.

A = [3,2,1,0,4], return false.

* 题目意思是数组中每个元素的往后的最大跳跃数

```
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

class Solution {
public:
	bool canJump(vector<int>& nums) {
		// 这道题用dp 的全局最优解和当前最优解
		int reach = 0; // 记录往后跳的最大值
		int i;
		for (i = 0; i < nums.size() && i <= reach;  i++){
			reach = max(reach, i + nums[i]);
		}
		if (reach >= nums.size() - 1)
			return true;
		else
			return false;

	}
};
Jump Game


int main()
{
	vector<int> data = { 2, 3, 1, 1, 4 };
	Solution solution;
	solution.canJump(data);
}
```