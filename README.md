#include <iostream>
#include <vector>

const int SIZE = 9; 

void printGrid(const std::vector<std::vector<int>>& grid) {
    for (int i = 0; i < SIZE; ++i) {
        for (int j = 0; j < SIZE; ++j) {
            std::cout << grid[i][j] << " ";
        }
        std::cout << std::endl;
    }
}


bool isSafe(const std::vector<std::vector<int>>& grid, int row, int col, int num) {
    
    for (int x = 0; x < SIZE; ++x) {
        if (grid[row][x] == num) {
            return false;
        }
    }

    
    for (int x = 0; x < SIZE; ++x) {
        if (grid[x][col] == num) {
            return false;
        }
    }

    
    int startRow = row - row % 3;
    int startCol = col - col % 3;
    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 3; ++j) {
            if (grid[i + startRow][j + startCol] == num) {
                return false;
            }
        }
    }

    return true;
}


bool solveSudoku(std::vector<std::vector<int>>& grid) {
    for (int row = 0; row < SIZE; ++row) {
        for (int col = 0; col < SIZE; ++col) {
            if (grid[row][col] == 0) {
                for (int num = 1; num <= SIZE; ++num) {
                    if (isSafe(grid, row, col, num)) {
                        grid[row][col] = num; 
                        if (solveSudoku(grid)) {
                            return true;
                        }
                        grid[row][col] = 0; 
                    }
                }
                return false;
            }
        }
    }
    return true;
}


void inputGrid(std::vector<std::vector<int>>& grid) {
    std::cout << "Enter  Sudoku puzzle (use 0 for empty cells):\n";
    for (int i = 0; i < SIZE; ++i) {
        for (int j = 0; j < SIZE; ++j) {
            std::cin >> grid[i][j];
        }
    }
}

int main() {
    std::vector<std::vector<int>> grid(SIZE, std::vector<int>(SIZE, 0));

    inputGrid(grid);

    if (solveSudoku(grid)) {
        std::cout << "Sudoku puzzle solved:\n";
        printGrid(grid);
    } else {
        std::cout << "No solution for the given Sudoku puzzle.\n";
        std::cout <<"coded by tripathyjii"
    }

    return 0;
}
