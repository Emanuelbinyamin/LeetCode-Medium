public class Solution {
    public bool IsValidSudoku(char[][] board) {
        int[] countArrRow = new int[9];
        int[] countArrCol = new int[9];
        int[] countArrBox = new int[9];

        // Iterate through the rows and columns
        for (int i = 0; i < 9; i++) {
            //The method Array.Clear() in C# is used to reset all elements of an array to their default values,
            // starting from a specified index for a specified length : Array.Clear(array, startIndex, length);
            Array.Clear(countArrRow, 0, 9);
            Array.Clear(countArrCol, 0, 9);
            Array.Clear(countArrBox, 0, 9);

            for (int j = 0; j < 9; j++) {
                // Check rows
                if (board[i][j] != '.') {
                    int value = board[i][j] - '1';
                    if (countArrRow[value]++ > 0) {
                        return false;
                    }
                }

                // Check columns
                if (board[j][i] != '.') {
                    int value = board[j][i] - '1';
                    if (countArrCol[value]++ > 0) {
                        return false;
                    }
                }

                // Check 3x3 sub-boxes
                int boxRow = (i / 3) * 3 + j / 3;
                int boxCol = (i % 3) * 3 + j % 3;
                if (board[boxRow][boxCol] != '.') {
                    int value = board[boxRow][boxCol] - '1';
                    if (countArrBox[value]++ > 0) {
                        return false;
                    }
                }
            }
        }

        return true;
    }
}
