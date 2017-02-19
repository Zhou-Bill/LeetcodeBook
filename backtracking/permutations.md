\#\#Permutations

> 全排列

Given a collection of**distinct**numbers, return all possible permutations.

For example,  
`[1,2,3]`have the following permutations:  


```
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

```
#include<iostream>
#include<vector>
using namespace std;

class Solution {
public:
	
	vector<vector<int>> permute(vector<int>& nums) {
		vector<vector<int>> result;
		// key 作为保存数组中每个数，当每个数都出现一次的时候，那么我把key放入result
		vector<int> key;
		// data 作为标记当前nums 数组中的数是否已经用过了，用过为1，没用过为0
		vector<int> data(nums.size() , 0);
		digui(nums, key, data, result, 0);
		return result;
	}
	void digui(vector<int> nums, vector<int> &key, vector<int> &data, vector<vector<int>> &result, int step) {
		if (step == nums.size()){
			result.push_back(key);
		}
		else{
			for (int i = 0; i < nums.size(); i++){
				if (!data[i]){
					key.push_back(nums[i]);
					data[i] = 1;
					digui(nums, key, data, result, step + 1);
					key.pop_back();
					data[i] = 0;
				}
			}
		}
	}

};

int main()
{
	vector<int> nums = { 1, 2, 3 };
	Solution solution;
	solution.permute(nums);
}
```

全排列使用的是递归回溯，在使用过的数字中标记为1，没使用过标记为0，当一次递归完成后，我将数字pop\_back\(\)，并且当前状态设置成0，然后按step去计算是否等于了给定的数组的长度。。

