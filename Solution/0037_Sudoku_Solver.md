# Sudoku Solver / 解数独

Leetcode: https://leetcode.com/problems/sudoku-solver

力扣：https://leetcode.cn/problems/sudoku-solver

## Description / 题目描述

Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy  **all of the following rules** :

1. Each of the digits `1-9` must occur exactly once in each row.
2. Each of the digits `1-9` must occur exactly once in each column.
3. Each of the digits `1-9` must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.

The `'.'` character indicates empty cells.

编写一个程序，通过填充空格来解决数独问题。

数独的解法需 ** 遵循如下规则** ：

1. 数字 `1-9` 在每一行只能出现一次。
2. 数字 `1-9` 在每一列只能出现一次。
3. 数字 `1-9` 在每一个以粗实线分隔的 `3x3` 宫内只能出现一次。（请参考示例图）

数独部分空格内已填入了数字，空白格用 `'.'` 表示。

## Constraints **/ 提示**

* `board.length == 9`
* `board[i].length == 9`
* `board[i][j]` is a digit or `'.'`. / `board[i][j]` 是一位数字或者 `'.'`
* It is **guaranteed** that the input board has only one solution. / 题目数据 **保证** 输入数独仅有一个解

## Solution: PreProcessing + DFS / 预处理 + 深度优先搜索

Use an integer 2D matrix `intBoard`, convert the characters in the given `board` array into integers for further processing.

Use three boolean 2D matrices: `rowPossibleNums`, `colPossibleNums`, and `blockPossibleNums` to record the available numbers in each row, each column, and each 3x3 block respectively (the index of the block is calculated by `(row / 3) * 3 + (col / 3)`). `false` means available, `true` means occupied. For example, `rowPossibleNums[2][3] == true` means that the number 4 has already appeared in the third row.

First, preprocess the given 2D matrix `board`. If the current cell `[i][j]` contains a digit, set that digit to `intBoard[i][j]` and set the corresponding positions in `rowPossibleNums`, `colPossibleNums`, and `blockPossibleNums` to `true`. Otherwise (if the current cell `[i][j]` contains a '.'), set `intBoard[i][j]` to `-1`.

The problem statement ensures that there is exactly one solution. Therefore, we can first identify answers that do not require DFS. Traverse `intBoard`, and if any cell `intBoard[i][j]` has any integer `k` (0 <= k < 9) satisfying `!rowPossibleNums[i][k] && !colPossibleNums[j][k] && !blockPossibleNums[(i / 3) * 3 + (j / 3)][k]` and there is exactly one such integer `k`, it means we have found an answer that does not require DFS. Every time an answer is found, repeat the above traversal until no more answers can be found without DFS.

Then use DFS for searching. For each cell with a value of `-1`, try to fill in a possible number and proceed with recursion (the possible numbers for the current cell `intBoard[i][j]` are those satisfying `!rowPossibleNums[i][k] && !colPossibleNums[j][k] && !blockPossibleNums[(i / 3) * 3 + (j / 3)][k]` where 0 <= k < 9). If any cell's value is `-1` and there are no possible numbers to fill in, backtrack to the previous cell with a filled number and continue trying the next possible number.

Finally, convert the integers in `intBoard` back to characters and fill them into `board` accordingly.

The time complexity of this algorithm is `O((n!)^n)`, where `n=9` in this problem. It is worth noting that due to the preprocessing step, the actual time complexity is often significantly better than `O((n!)^n)`.

*Based on the principles of modular programming, we can store the value 9 in a global variable.

创建一个整数的二维矩阵 `intBoard`，将既定数组 `board` 中的字符转换为整数，以便后续处理。

创建三个布尔值的二维矩阵 `rowPossibleNums`，`colPossibleNums`，`blockPossibleNums`，分别用于记录每一行，每一列，和每一个3x3的方格中可用的数字（方格的下标为从左到右，从上到下，判断当前元素处于哪个方格的计算方法为 `(row / 3) * 3 + (col / 3)`）。`false` 代表可用，`true` 代表已经被占用，例如 `rowPossibleNums[2][3] == true` 代表第三行中数字4已经出现过。

首先对给定二维矩阵 `board` 进行预处理，如果当前单元格的元素 `[i][j]` 是一个整数，则将该数字填入 `intBoard[i][j]`，同时将 `rowPossibleNums`，`colPossibleNums`，`blockPossibleNums` 中对应位置的值变为 `true`。反之（当前单元格的元素 `[i][j]` 是 '.'），则将 `intBoard[i][j]` 的值设为 `-1`。

题目中明确表示本题有且只有一个答案，所以我们可以先将不需要DFS搜索就能找到的答案确定。对 `intBoard` 进行遍历，如果当前单元格的元素 `intBoard[i][j]` 有任何整数 `k` (0 <= k < 9）满足条件 `!rowPossibleNums[i][k] && !colPossibleNums[j][k] && !blockPossibleNums[(i / 3) * 3 + (j / 3)][k]`且满足条件的整数 `k` 有且只有一个时，就代表我们找到了一个不需要DFS搜索就能找到的答案。每当一个答案被找出，我们就应该重复上述遍历，直至找不到任何不需要DFS搜索就能找到的答案。

之后使用DFS进行搜索。对于每一个值为 `-1` 的单元格，尝试填入一个可能的数字并进行递归（能填入当前单元格 `intBoard[i][j]` 的可能的数字为满足条件 `!rowPossibleNums[i][k] && !colPossibleNums[j][k] && !blockPossibleNums[(i / 3) * 3 + (j / 3)][k]` 的整数 `k`，且 `0 <= k < 9`）。如果搜索到有任何单元格的值为 `-1` 且没有任何可以填入的数字，则回溯到上一个填入数字的单元格，继续尝试下一个可能的数字。

最后，将 `intBoard` 中的整数转换为字符，一一对应地填入 `board` 中即可。

此算法时间复杂度为 `O((n!)^n)`，在本题中 n=9。值得一提的是，因为我们对给定二维矩阵进行了预处理，在通常情况下，此解法的时间复杂度会大幅度优于 `O((n!)^n)`。

*基于模块化编程的思想，我们可以将代码中的整数9存入一个全局变量

Java

```java
class Solution {
    public void solveSudoku(char[][] board) {
        int[][] intBoard = new int[9][9];
        boolean[][] rowPossibleNums = new boolean[9][9];
        boolean[][] colPossibleNums = new boolean[9][9];
        boolean[][] blockPossibleNums = new boolean[9][9];

        // Convert char[][] into int[][], set rows, cols and blocks to true when we find an int
        for (int i = 0; i < 9; i++){
            for (int j = 0; j < 9; j++){
                if (board[i][j] == '.') {
                    intBoard[i][j] = -1;
                } else{
                    int temp = board[i][j] - '0';
                    intBoard[i][j] = temp;
                    rowPossibleNums[i][temp - 1] = true;
                    colPossibleNums[j][temp - 1] = true;
                    blockPossibleNums[(i / 3) * 3 + (j / 3)][temp - 1] = true;
                }
            }
        }

        preProcessBoard(intBoard, rowPossibleNums, colPossibleNums, blockPossibleNums);
        DFS(intBoard, rowPossibleNums, colPossibleNums, blockPossibleNums);

      	// Convert int back to char
	for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                board[i][j] = (char)(intBoard[i][j] + (int)'0');
            }
        }

    }

    // Fill in cells that can find answer without DFS
    public void preProcessBoard(int[][] intBoard, boolean[][] rowPossibleNums, boolean[][] colPossibleNums, boolean[][] blockPossibleNums){
        boolean updated = false;
        for (int i = 0; i < 9; i++){
            for (int j = 0; j < 9; j++) {
                if (intBoard[i][j] == -1){
                    int possibleNums = 0;
                    int num = 0;
                    for (int k = 0; k < 9; k++){
                        if (!rowPossibleNums[i][k] && !colPossibleNums[j][k] && !blockPossibleNums[(i / 3) * 3 + (j / 3)][k]) {
                            num = k;
                            possibleNums++;
                        }
                        if (possibleNums > 1) break;
                    }
                    if (possibleNums == 1){ // update the cell when there is only 1 possible number for that cell
                        intBoard[i][j] = num + 1;
                        rowPossibleNums[i][num] = true;
                        colPossibleNums[j][num] = true;
                        blockPossibleNums[(i / 3) * 3 + (j / 3)][num] = true;
                        updated = true;
                    }
                }
            }
        }
        if (updated) preProcessBoard(intBoard, rowPossibleNums, colPossibleNums, blockPossibleNums);
    }

    public boolean DFS(int[][] intBoard, boolean[][] rowPossibleNums, boolean[][] colPossibleNums, boolean[][] blockPossibleNums) {
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (intBoard[i][j] == -1) { // Skip cells that have a vaild number
                    for (int num = 0; num < 9; num++) {
                        if (!rowPossibleNums[i][num] && !colPossibleNums[j][num] && !blockPossibleNums[(i / 3) * 3 + (j / 3)][num]) {
                            intBoard[i][j] = num + 1;
                            rowPossibleNums[i][num] = true;
                            colPossibleNums[j][num] = true;
                            blockPossibleNums[(i / 3) * 3 + (j / 3)][num] = true;

                            if (DFS(intBoard, rowPossibleNums, colPossibleNums, blockPossibleNums)) {
                                return true;
                            }

                            intBoard[i][j] = -1;
                            rowPossibleNums[i][num] = false;
                            colPossibleNums[j][num] = false;
                            blockPossibleNums[(i / 3) * 3 + (j / 3)][num] = false;
                        }
                    }
                    return false; // No valid number can be placed in this cell
                }
            }
        }
        return true; // All cells have been successfully filled
    }
}
```

Python

```python
class Solution:

    def solveSudoku(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        int_board = [[-1 for _ in range(9)] for _ in range(9)]
        row_possible_nums = [[False for _ in range(9)] for _ in range(9)]
        col_possible_nums = [[False for _ in range(9)] for _ in range(9)]
        block_possible_nums = [[False for _ in range(9)] for _ in range(9)]

      	# Convert chars to int, and set rows, cols and blocks to true when board[i][j] is a vaild num
	for i in range(9):
            for j in range(9):
                if board[i][j] != '.':
                    temp = int(board[i][j])
                    int_board[i][j] = temp
                    row_possible_nums[i][temp - 1] = True
                    col_possible_nums[j][temp - 1] = True
                    block_possible_nums[i//3*3 + j//3][temp - 1] = True


      	# Find all vaild answer without using DFS
	def preProcessBoard():
            updated = False
            for i in range(9):
                for j in range(9):
                    if int_board[i][j] == -1:
                        num = 0
                        possible_numbers = 0
                        for k in range(9):
                            if row_possible_nums[i][k] == False and col_possible_nums[j][k] == False and block_possible_nums[i//3*3 + j//3][k] == False:
                                num = k
                                possible_numbers += 1

                            if possible_numbers > 1:
                                break
  
                        if possible_numbers == 1: # Update cell only if cell has 1 possible number to fill in
                            int_board[i][j] = num + 1
                            row_possible_nums[i][num] = True
                            col_possible_nums[j][num] = True
                            block_possible_nums[i//3*3 + j//3][num] = True
                            updated = True

            if updated:
                preProcessBoard()

        def DFS() -> bool:
            for i in range(9):
                for j in range(9):
                    if int_board[i][j] == -1:
                        for num in range(9):
                            if not row_possible_nums[i][num] and not col_possible_nums[j][num] and not block_possible_nums[i//3*3 + j//3][num]:
                                int_board[i][j] = num + 1
                                row_possible_nums[i][num] = True
                                col_possible_nums[j][num] = True
                                block_possible_nums[i//3*3 + j//3][num] = True

                                if DFS():
                                    return True

                                int_board[i][j] = -1
                                row_possible_nums[i][num] = False
                                col_possible_nums[j][num] = False
                                block_possible_nums[i//3*3 + j//3][num] = False
                        return False # No vaild number can be place in this cell, backtrack
            return True # successfully filled in all cells


        preProcessBoard()
        DFS()

        for i in range(9):
            for j in range(9):
                board[i][j] = str(int_board[i][j])
```
