## Merge Sorted Array

> Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

>Note:
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

题目意思是将第二个数组按顺序插到第一个数组中

```
#include<iostream>
#include<vector>
using namespace std;

class Solution {
public:
	void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
		int j = 0, i = 0;
		while (i<m && j<n){
			if (nums1[i] < nums2[j]){
				i++;
				continue;
			}
			//解释一下为什么是m-1,m-1代表的是初始化nums1数组中最后一个数字，
			//当要执行下面程序时，表明现在开始要插入nums2的数字到nums1中了
			//所以后面要m++,随时保持nums1的最后一个数字，题目说明nums1有足够
			// 大的空间
			for (int k = m-1; k >= i; k--){
				nums1[k + 1] = nums1[k];
			}
			m++;
			nums1[i] = nums2[j];
			j++;
		}
		// 这里解决当nums1数组 初始化个数为0的时候，直接把第二个数组赋给第一个数组
		if (i == m && i == 0){
			for (int q = 0; q < nums1.size(); q++){
				nums1[q] = nums2[q];
			}
		}
		if (j < n && m<nums1.size()){
			for (int k = m; k < nums1.size(); k++)
				nums1[k] = nums2[j++];
		}
	}
};

int main()
{

	vector<int> nums1 = { 4,5,6, 0, 0, 0 };
	vector<int> nums2 = { 1,2,3 };
	Solution solution;
	solution.merge(nums1,3,nums2,3);
}
```