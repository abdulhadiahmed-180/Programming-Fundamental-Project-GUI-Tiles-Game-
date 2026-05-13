# GUI Tiles Game – 15 Puzzle Game

A graphical 15 Puzzle Game developed in C++ using the BGI Graphics Library as a Programming Fundamentals (PF) project. The game consists of numbered tiles arranged in a 4x4 grid with one empty space. Players use keyboard controls to move tiles and arrange them in the correct numerical order.

---

# Project Overview

The project demonstrates the implementation of:

* 2D arrays
* Functions
* Conditional statements
* Loops
* Graphics programming
* Randomization and shuffling
* Game logic handling
* User interaction through keyboard controls

The game includes a graphical board, move counter, tile coloring system, puzzle completion checking, and restart functionality.

---

# Features

* Interactive GUI using graphics.h
* 4x4 sliding puzzle board
* Randomized tile shuffling
* Move counter tracking
* Keyboard-based controls (W/A/S/D)
* Automatic puzzle completion detection
* Restart and exit options
* Color indication for correctly placed tiles

---

# Technologies Used

* Language: C++
* Graphics Library: BGI Graphics Library (`graphics.h`)
* Compiler: Turbo C++ / Dev C++ with WinBGIm
* Concepts Used:

  * Arrays
  * Functions
  * Boolean Logic
  * Random Number Generation
  * GUI Programming

---

# Game Controls

| Key | Function        |
| --- | --------------- |
| W   | Move Tile Up    |
| S   | Move Tile Down  |
| A   | Move Tile Left  |
| D   | Move Tile Right |
| R   | Restart Game    |
| X   | Exit Game       |

---

# Game Logic

## Tile Movement

The blank tile swaps its position with adjacent numbered tiles depending on the key pressed by the player.

## Puzzle Completion

The game continuously checks whether all tiles are arranged in ascending order from 1 to 15.

## Tile Colors

* Green Tile → Correct Position
* Blue Tile → Incorrect Position
* Black Tile → Empty Space

---

# Project Structure

```bash
GUI-Tiles-Game/
│── main.cpp             # Complete source code
│── README.md            # Project documentation
│── screenshots/         # Gameplay screenshots
```

---

# Installation and Setup

## Requirements

* C++ Compiler
* graphics.h Library
* WinBGIm setup (if using Dev C++)

## Compile and Run

```bash
g++ main.cpp -o game -lbgi -lgdi32 -lcomdlg32 -luuid -loleaut32 -lole32
```

Run the executable after successful compilation.

---

# How to Play

1. Start the game.
2. Observe the shuffled numbered tiles.
3. Use W, A, S, and D keys to move tiles.
4. Arrange the numbers from 1 to 15 in correct order.
5. Complete the puzzle in minimum moves.

---

# Functions Used

| Function         | Purpose                         |
| ---------------- | ------------------------------- |
| `movetile()`     | Moves tile into blank position  |
| `Solved()`       | Checks whether puzzle is solved |
| `drawBoard()`    | Draws complete game interface   |
| `shuffleBoard()` | Randomizes tile positions       |

---

# Screenshots

Add gameplay screenshots here.

```markdown
![Gameplay](screenshots/gameplay.png)
```

---

# Learning Outcomes

This project helped in learning:

* Graphics programming in C++
* Game development basics
* Problem-solving techniques
* Keyboard event handling
* Matrix manipulation
* GUI rendering concepts
* Randomization techniques

---

# Future Improvements

* Add timer system
* Add difficulty levels
* Add mouse controls
* Improve animations
* Add sound effects
* Add score saving feature

---

# Contributors

* Abdul Hadi Ahmed

---

# License

This project is created for educational purposes as part of the Programming Fundamentals course
