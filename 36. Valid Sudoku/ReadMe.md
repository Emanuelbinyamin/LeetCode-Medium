# Valid Sudoku Solver

This repository contains my solution to the **Valid Sudoku** problem from [LeetCode](https://leetcode.com/problems/valid-sudoku/). The solution is implemented in **C#** and follows a structured and efficient approach to validate Sudoku boards according to specific rules.

---

## Problem Description

**Determine if a 9x9 Sudoku board is valid.**  
Only the filled cells need to be validated based on the following rules:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3x3` sub-boxes of the grid must contain the digits `1-9` without repetition.

### Notes:
- A valid Sudoku board (partially filled) is not necessarily solvable.
- Empty cells are denoted by the character `'.'` and should be ignored during validation.

---

## Example Inputs and Outputs

### Example 1:
**Input:**
```plaintext
[["5","3",".",".","7",".",".",".","."],
 ["6",".",".","1","9","5",".",".","."],
 [".","9","8",".",".",".",".","6","."],
 ["8",".",".",".","6",".",".",".","3"],
 ["4",".",".","8",".","3",".",".","1"],
 ["7",".",".",".","2",".",".",".","6"],
 [".","6",".",".",".",".","2","8","."],
 [".",".",".","4","1","9",".",".","5"],
 [".",".",".",".","8",".",".","7","9"]]
```

**Output:**
```plaintext
true
```

---

### Example 2:
**Input:**
```plaintext
[["8","3",".",".","7",".",".",".","."],
 ["6",".",".","1","9","5",".",".","."],
 [".","9","8",".",".",".",".","6","."],
 ["8",".",".",".","6",".",".",".","3"],
 ["4",".",".","8",".","3",".",".","1"],
 ["7",".",".",".","2",".",".",".","6"],
 [".","6",".",".",".",".","2","8","."],
 [".",".",".","4","1","9",".",".","5"],
 [".",".",".",".","8",".",".","7","9"]]
```

**Output:**
```plaintext
false
```

**Explanation:**  
In the top-left `3x3` sub-box, the digit `8` appears twice, making it invalid.

---

## Constraints
- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit `1-9` or `'.'`.

---

## Approach to the Solution

To solve the problem, the solution iteratively validates:
1. Each **row** for duplicate digits.
2. Each **column** for duplicate digits.
3. Each `3x3` **sub-box** for duplicate digits.

### Steps:
1. **Initialize counting arrays** for rows, columns, and sub-boxes to track occurrences of digits.
2. **Iterate through the board**, checking:
   - Rows and columns simultaneously.
   - Sub-boxes based on their calculated indices.
3. Reset the counting arrays after each iteration.
4. Return `false` if any rule is violated; otherwise, return `true`.

---

## Solution Code

```csharp
public class Solution {
    public bool IsValidSudoku(char[][] board) {
        int[] countArrRow = new int[9];
        int[] countArrCol = new int[9];
        int[] countArrBox = new int[9];

        for (int i = 0; i < 9; i++) {
            Array.Clear(countArrRow, 0, 9);
            Array.Clear(countArrCol, 0, 9);
            Array.Clear(countArrBox, 0, 9);

            for (int j = 0; j < 9; j++) {
                // Check row
                if (board[i][j] != '.') {
                    int num = board[i][j] - '1';
                    if (countArrRow[num]++ > 0) return false;
                }

                // Check column
                if (board[j][i] != '.') {
                    int num = board[j][i] - '1';
                    if (countArrCol[num]++ > 0) return false;
                }

                // Check 3x3 sub-box
                int rowBox = (i / 3) * 3 + j / 3;
                int colBox = (i % 3) * 3 + j % 3;
                if (board[rowBox][colBox] != '.') {
                    int num = board[rowBox][colBox] - '1';
                    if (countArrBox[num]++ > 0) return false;
                }
            }
        }
        return true;
    }
}
```

---

## How to Approach the Problem
- **Understand the rules:** Break down the problem into three separate validations (rows, columns, and sub-boxes).
- **Plan:** Decide how to count occurrences and reset counters when needed.
- **Optimize:** Combine validations in a single loop to minimize redundant iterations.

### Key Learning:
- Use arrays to efficiently track digit occurrences.
- Calculate sub-box indices dynamically using mathematical formulas.

---

Feel free to contribute or suggest optimizations!
