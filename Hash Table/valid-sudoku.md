## Valid Sudoku

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

![](/assets/250px-Sudoku-by-L2G-20050714.svg.png)

A partially filled sudoku which is valid.


> 数独规则，是横、竖、九个格 不能重复

```
#include<iostream>
#include<vector>
using namespace std;

class Solution {
public:
	bool isValidSudoku(vector<vector<char>>& board) {
		int row=0,column = 0,i=0,block,k,m;
		vector<char> data;
		//横向不重复
		for (row = 0; row < 9; row++){
			int table[9] = { 0 };
			for (column = 0; column < 9; column++){
				if (board[row][column] != '.'  ){
					if (table[board[row][column]-'0'-1] == board[row][column])
						return false;
					else{
						table[board[row][column] - '0'-1] = board[row][column];
					}
				}
			}
		}

		// 竖向不重复
		for (column = 0; column < 9; column++){
			int Columntable[9] = { 0 };
			for (row = 0; row < 9; row++){
				if (board[row][column] != '.'){
					if (Columntable[board[row][column]-'0'-1] == board[row][column])
						return false;
					else{
						Columntable[board[row][column] - '0'-1] = board[row][column];
					}
				}
			}
		}

		//每个小块不重复
		for (block = 0; block < 9; block++){
			int blockTable[9] = { 0 };
			for (k = 0; k < 3; k++){
				for (i = 0; i < 3; i++){
					if (board[block / 3 * 3 + k][block % 3 * 3 + i] != '.'){
						if (blockTable[k * 3 + i] != '.'){
							if (blockTable[board[block / 3 * 3 + k][block % 3 * 3 + i]-'0'-1] == board[block / 3 * 3 + k][block % 3 * 3 + i]){
								return false;
							}
							else
							{
								blockTable[board[block / 3 * 3 + k][block % 3 * 3 + i]-'0'-1] = board[block / 3 * 3 + k][block % 3 * 3 + i];
							}
						}
					}
	
				}
			}
		}
		return true;
	}	
};
int main() {
	vector <vector<char> > str = {
		{ '.', '8', '7', '6', '5', '4', '3', '2', '1' },
		{ '2', '.', '.', '.', '.', '.', '.', '.', '.' },
		{ '3', '.', '.', '.', '.', '.', '.', '.', '.' },
		{ '4', '.', '.', '.', '.', '.', '.', '.', '.' },
		{ '5', '.', '.', '.', '.', '.', '.', '.', '.' },
		{ '6', '.', '.', '.', '.', '.', '.', '.', '.' },
		{ '7', '.', '.', '.', '.', '.', '.', '.', '.' },
		{ '8', '.', '.', '.', '.', '.', '.', '.', '.' },
		{ '9', '.', '.', '.', '.', '.', '.', '.', '.' }
	};
	Solution solution;
	cout<<solution.isValidSudoku(str);
}
```

这道题用hash Table 去做

* 遍历横向数据、或者竖向数据、或格子数据时,把数据放入一个空间为9的数组 a[9] ={0}
* 假如现在遍历的数组值为2 ，先判断一下a[1]是否为0，如果是，那么a[1] = 2 ,如果遍历的值为7 ，那么a[6] = 7,如果7再一次出现，那么a[6] 已经不等于0了，表示已经有值，7已经重复，数独不成立

* **值得注意的是：** 在判断每个block 的时候`board[block / 3 * 3 + k][block % 3 * 3 + i]`当前值得表示