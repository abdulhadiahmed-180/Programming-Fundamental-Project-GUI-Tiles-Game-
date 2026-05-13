# Programming-Fundamental-Project-GUI-Tiles-Game-
rn 0; }

***Perfectly Running GUI Tiles Game in Dev-CPP IDE by installing the graphics library***

#include <graphics.h>
#include <conio.h>
#include <stdlib.h>
#include <time.h>
#include <stdio.h>
#include <stdbool.h> 

// Initializing of every thing used in code
int board[4][4];
int blankrow = 3, blankcolumn = 3;
int tilesize = 100;
int shiftX = 50;
int shiftY = 90; 
int move_counter = 0; 

void movetile(int r, int c) {
    int temp = board[r][c];
    board[r][c] = 0;
    board[blankrow][blankcolumn] = temp;
    
    blankrow = r; 
    blankcolumn = c;
    move_counter++; 
}

bool Solved() {
    int expected = 1;
    for (int r = 0; r < 4; r++) {
        for (int c = 0; c < 4; c++) {
            if (r == 3 && c == 3) {
                return board[r][c] == 0; 
            }
            if (board[r][c] != expected) return false;
            expected++;
        }
    }
    return false;
}

void drawBoard() {
    cleardevice();
    
    // Display Move Counter which would count every move of the user when W/A/S/D keys would pressed
    char Moves_Msg[50];
    sprintf(Moves_Msg, "Moves: %d", move_counter);
    setcolor(WHITE);
    settextstyle(DEFAULT_FONT, HORIZ_DIR, 2);
    outtextxy(shiftX, 10, (char*)Moves_Msg);
    
    // Display WASD Controls and its applications so that every move would be properly done by user
    char Controls_Msg[100];
    sprintf(Controls_Msg, "W=UP | S=DOWN | A=LEFT | D=RIGHT | X=EXIT");
    setcolor(YELLOW); 
    settextstyle(DEFAULT_FONT, HORIZ_DIR, 2);
    outtextxy(shiftX, 45, (char*)Controls_Msg);

    // Draw the Board in which the numerical 15 tiles game would be held respectively
    for (int r = 0; r < 4; r++) {
        for (int c = 0; c < 4; c++) {
            int x1 = shiftX + c * tilesize;
            int y1 = shiftY + r * tilesize;
            int x2 = x1 + tilesize;
            int y2 = y1 + tilesize;
            
            int expectedValue = r * 4 + c + 1;
            
            // Set tile colors based on correct place of every number and if it is not placed at correct place then tiles would be of two colors
            if (board[r][c] == 0) {
                setfillstyle(SOLID_FILL, BLACK); 
            } 
            else if (board[r][c] == expectedValue) {
                setfillstyle(SOLID_FILL, GREEN); 
            } else {
                setfillstyle(SOLID_FILL, BLUE); 
            }
            
            bar(x1, y1, x2, y2);
            setcolor(WHITE);
            rectangle(x1, y1, x2, y2);

            if (board[r][c] != 0) {
                char num[4];
                sprintf(num, "%d", board[r][c]);
                settextstyle(DEFAULT_FONT, HORIZ_DIR, 3);
                
                setcolor(WHITE); 
                
                int tw = textwidth(num);
                int th = textheight(num);
                outtextxy(x1 + (tilesize - tw)/2, y1 + (tilesize - th)/2, num);
            }
        }
    }
}

// Function to randomize the board state so that every time user plays so the tiles would be shuffled accordingly so unique randomization of numbers 
void shuffleBoard() {
    int init = 1;
    int array[16]; 

    // 1. Initialize the 1D array with values 1 to 15, and 0 at the end which is blank box so that movement tiles could occur
    for (int i = 0; i < 15; i++) {
        array[i] = init++; 
    }
    array[15] = 0; 
    
    // 2. Perform shuffle (random swapping of numerical tile numbers)
    srand(time(0));
    for (int i = 15; i > 0; i--) {
        int j = rand() % (i + 1); 
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }

    // 3. Convert the shuffled 1D array back to the 2D board so that tiles would be at 4x4 matrix
    for (int r = 0; r < 4; r++) {
        for (int c = 0; c < 4; c++) {
            board[r][c] = array[r * 4 + c];
            
            if (board[r][c] == 0) {
                blankrow = r; 
                blankcolumn = c;
            }
        }
    }
    
    move_counter = 0; 
}

int main() {
    int gd = DETECT, gm;
    
    initgraph(&gd, &gm, (char*)"");

    shuffleBoard();

    while (true) {
        drawBoard();
		// Checking off the grid that the numbers are plotted at right places and prompt suitable message when whole game completes
        if (Solved()) {
            setcolor(YELLOW);
            settextstyle(DEFAULT_FONT, HORIZ_DIR, 3);
            
            char finalMsg[100];
            sprintf(finalMsg, "PUZZLE COMPLETED in %d MOVES!", move_counter);
            outtextxy(shiftX, shiftY + 450, (char*)finalMsg);
            
            outtextxy(shiftX, shiftY + 500, (char*)"Press R/r to Restart or X/x to Exit");
            
            char choice = getch();
            if (choice == 'r' || choice == 'R') {
                shuffleBoard();
                continue;
            } else if (choice == 'x' || choice == 'X') {
                break;
            }
        }

        char ch = getch();
        
        if (ch == 'x' || ch == 'X') break;
        
        // Movement Logic and seeing which key is typed and then perform functions accordingly
        if ((ch == 'w' || ch == 'W') && blankrow < 3) {
            movetile(blankrow + 1, blankcolumn);
        }
        else if ((ch == 's' || ch == 'S') && blankrow > 0) {
            movetile(blankrow - 1, blankcolumn);
        }
        else if ((ch == 'a' || ch == 'A') && blankcolumn < 3) {
            movetile(blankrow, blankcolumn + 1);
        }
        else if ((ch == 'd' || ch == 'D') && blankcolumn > 0) {
            movetile(blankrow, blankcolumn - 1);
        }
    }

    closegraph();
    return 0;
}
