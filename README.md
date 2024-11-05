# Tic-tac-toe
#include <stdio.h>

char board[3][3]; 
char currentPlayer;

void initializeBoard() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            board[i][j] = ' ';
        }
    }
}

void printBoard() {
    printf(" %c | %c | %c \n", board[0][0], board[0][1], board[0][2]);
    printf("---|---|---\n");
    printf(" %c | %c | %c \n", board[1][0], board[1][1], board[1][2]);
    printf("---|---|---\n");
    printf(" %c | %c | %c \n", board[2][0], board[2][1], board[2][2]);
}

void switchPlayer() {
    currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
}

int isMoveValid(int row, int col) {
    return (row >= 0 && row < 3 && col >= 0 && col < 3 && board[row][col] == ' ');
}

int checkWin() {
    // Check rows and columns
    for (int i = 0; i < 3; i++) {
        if ((board[i][0] == currentPlayer && board[i][1] == currentPlayer && board[i][2] == currentPlayer) ||
            (board[0][i] == currentPlayer && board[1][i] == currentPlayer && board[2][i] == currentPlayer)) {
            return 1;
        }
    }
    // Check diagonals
    if ((board[0][0] == currentPlayer && board[1][1] == currentPlayer && board[2][2] == currentPlayer) ||
        (board[0][2] == currentPlayer && board[1][1] == currentPlayer && board[2][0] == currentPlayer)) {
        return 1;
    }
    return 0;
}

int isBoardFull() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] == ' ') {
                return 0;  
            }
        }
    }
    return 1;  
}

int main() {
    int row, col;
    currentPlayer = 'X'; 
    initializeBoard();

    while (1) {
        printBoard();
        printf("Player %c, enter your move (row and column): ", currentPlayer);
        scanf("%d %d", &row, &col);

        if (isMoveValid(row, col)) {
            board[row][col] = currentPlayer;
            if (checkWin()) {
                printBoard();
                printf("Player %c wins!\n", currentPlayer);
                break;
            }
            if (isBoardFull()) {
                printBoard();
                printf("It's a draw!\n");
                break;
            }
            switchPlayer();
        } else {
            printf("Invalid move! Try again.\n");
        }
    }

    return 0;
}
