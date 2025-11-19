# LCS String Finder in Binary Files

A C implementation of the Longest Common Subsequence (LCS) algorithm, designed to find the LCS between strings extracted from binary files.

## Overview

This program reads two binary files, extracts their string content, computes the Longest Common Subsequence using dynamic programming, and writes the result to an output file.

## Features

- **Binary File Handling**: Reads input directly from binary files
- **Dynamic Programming LCS**: Efficient O(n×m) algorithm for computing the longest common subsequence
- **File Output**: Writes the computed LCS to a specified output file
- **Modular Design**: Clean separation between file handling, matrix operations, and LCS computation

## Building

### Using Make

```bash
make all
```

### Using CMake

```bash
mkdir build
cd build
cmake ..
make
```

## Usage

```bash
./start <first_file> <second_file> <output_file>
```

### Parameters

| Parameter | Description |
|-----------|-------------|
| `first_file` | Path to the first binary input file |
| `second_file` | Path to the second binary input file |
| `output_file` | Path where the LCS result will be written |

### Example

```bash
./start input1.bin input2.bin result.txt
```

## How It Works

1. **File Reading**: Opens both input files in binary mode and reads their contents into buffers
2. **Matrix Allocation**: Creates a (n+1) × (m+1) matrix where n and m are the lengths of the input strings
3. **Matrix Initialization**: Sets the first row and column to zeros
4. **LCS Construction**: Fills the matrix using the classic LCS dynamic programming approach:
   - If characters match: `matrix[i][j] = matrix[i-1][j-1] + 1`
   - Otherwise: `matrix[i][j] = max(matrix[i-1][j], matrix[i][j-1])`
5. **Backtracking**: Traces back through the matrix to reconstruct the actual LCS string
6. **Output**: Writes the resulting LCS to the output file

## Project Structure

```
├── main.c          # Entry point and argument handling
├── extractlcs.c    # Core LCS algorithm implementation
├── extractlcs.h    # Header file with struct definitions and function declarations
├── Makefile        # Build configuration for Make
├── CMakeLists.txt  # Build configuration for CMake
└── README.md       # This file
```

## API Reference

### Main Functions

| Function | Description |
|----------|-------------|
| `controller()` | Main entry point that orchestrates the LCS computation |
| `openFiles()` | Opens input/output files and initializes the lcs_str structure |
| `allocMatrix()` | Allocates the dynamic programming matrix |
| `inizializeMatrix()` | Initializes matrix with zeros in first row/column |
| `buildLcs()` | Constructs the LCS using dynamic programming |
| `printLcs()` | Backtraces to extract the actual LCS string |
| `writeToOutput()` | Writes the result to the output file |

### Data Structures

#### `lcs_str`
Holds file handles and buffer information for input/output operations.

#### `LCS_matrix`
Contains the dynamic programming matrix and dimension information.

## Technical Details

- **Buffer Size**: Default buffer size is 512 bytes
- **C Standard**: C99
- **Memory Management**: Dynamic allocation for matrices and string buffers with proper cleanup

## Limitations

- Maximum string length is limited by the buffer size (512 bytes by default)
- Input files must contain valid string data

## Cleaning Up

```bash
make rm
```

## License

This project was created for educational purposes.
