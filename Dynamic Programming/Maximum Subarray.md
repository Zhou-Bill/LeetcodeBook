## Maximum Subarray

> Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

> For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.

这道题是经典的动态规划题，可以用**全局最优**与**局部最优解** 做

```
class Solution {
public:
	int maxSubArray(vector<int>& nums) {
		if ( nums.size() == 0)
			return 0;
		int global = nums[0];
		int local = nums[0];
		for (int i = 1; i<nums.size(); i++)
		{
			local = max(nums[i], local + nums[i]);
			global = max(local, global);
		}
		return global;
	}
};
```