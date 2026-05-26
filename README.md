# Crossword Puzzle Generator and Solver

An AI-powered crossword puzzle generator and solver using Constraint Satisfaction Problem (CSP) techniques.

## Overview

This project implements a complete crossword puzzle solution that can:
- **Parse crossword structures** from text files
- **Generate valid crossword assignments** using CSP solving techniques
- **Render crossword puzzles** as images
- **Handle complex constraints** with backtracking search

## Components

### `crossword.py`
Core crossword representation and parsing module:

- **`Variable` Class**: Represents a word position in the crossword
  - Tracks position (i, j), direction (ACROSS/DOWN), and length
  - Maintains list of cells occupied by the word
  - Implements hashing and equality for use in sets and dictionaries

- **`Crossword` Class**: Manages the entire crossword puzzle
  - Reads crossword structure from files (`_` for open cells, other characters for blocked cells)
  - Loads vocabulary from a word list
  - Automatically identifies all variables (across and down words)
  - Computes overlaps between intersecting words
  - Provides neighbor discovery for constraint propagation

### `generate.py`
Constraint Satisfaction Problem solver for crossword generation:

- **`CrosswordCreator` Class**: Solves the crossword puzzle using advanced techniques
  - **Node Consistency**: Removes words that don't match the required length
  - **Arc Consistency (AC-3)**: Enforces consistency between overlapping words
  - **Backtracking Search**: Finds valid complete assignments
  - **Smart Variable Selection**: Chooses variables with minimum remaining values (MRV heuristic)
  - **Conflict Ordering**: Sorts candidate values by constraint violations
  - **Visualization**: Prints solved puzzles to terminal and renders to images

## Key Algorithms

### Constraint Satisfaction Problem (CSP)
- **Variables**: Each across/down word in the crossword
- **Domain**: All words from the vocabulary matching the required length
- **Constraints**: 
  - All words must be distinct
  - Overlapping words must share the same letter at intersection points
  - Each word must fit its designated length

### Solving Strategy
1. **Enforce Node Consistency**: Filter domain values by word length
2. **AC-3 Algorithm**: Remove values that cannot satisfy arc constraints
3. **Backtracking Search**: Build a complete assignment through recursive search
4. **Heuristics**: 
   - Minimum Remaining Values (MRV) for variable selection
   - Least Constraining Value for value ordering

## Language Composition

- **Python**: 46.5% - Main implementation
- **Java**: 20.9%
- **C**: 14.1%
- **HTML**: 11.9%
- **R**: 2.8%
- **CSS**: 2.7%
- **Other**: 1.1%

## Usage

### Basic Generation
```bash
python generate.py structure.txt words.txt
```

Where:
- `structure.txt`: Crossword layout (use `_` for open cells, `#` or any other character for blocked cells)
- `words.txt`: Word list (one word per line)

### Generate and Save as Image
```bash
python generate.py structure.txt words.txt output.png
```

## File Formats

### Structure File (`structure.txt`)
```
_____
____#
_____
_____
#____
```
Use `_` for cells where words can go, and any other character for blocked cells.

### Words File (`words.txt`)
```
PYTHON
ALGORITHM
CONSTRAINT
SATISFACTION
SEARCH
```

## Features

✅ **Efficient Constraint Propagation**: Uses AC-3 algorithm to reduce search space  
✅ **Smart Search**: Employs backtracking with heuristics for fast solution finding  
✅ **Variable Overlap Detection**: Automatically identifies word intersections  
✅ **Image Export**: Renders solved puzzles to PNG with proper formatting  
✅ **Complete Validation**: Ensures all solutions are valid and consistent  

## Technical Highlights

- **Constraint Propagation**: Dramatically reduces search space before backtracking
- **Heuristic-Guided Search**: Selects most constrained variables first
- **Efficient Overlap Tracking**: Pre-computed overlaps speed up consistency checks
- **Domain Management**: Maintains and updates domains for each variable efficiently

## Requirements

- Python 3.x
- PIL/Pillow (for image generation)
- OpenSans font file (for rendering, customize path in `generate.py` if needed)

## Installation

```bash
pip install Pillow
```

## Example Output

When solved, the crossword is displayed in the terminal with filled letters and █ for blocked cells:
```
PYTHON
ALG█RM
CONSTR
SATISF
█EARCH
```
