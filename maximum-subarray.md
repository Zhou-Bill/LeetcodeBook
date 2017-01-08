## Maximum Subarray

> Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

> For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.

这道题是经典的动态规划题，可以用**全局最优**与**局部最优解** 做

全局最优，就是到当前元素为止最优的解是，一个是局部最优，就是必须包含当前元素的最优的解。

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

* **local** 表示局部最优解，即当前**nums[i]**与**local + nums[i]**
* 如果 **local** 为负数，那么还不如不要，直接去 nums[i]
* global 表示全局最优解