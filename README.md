# Sudoku Solver

## Introduction
Sudoku is a classic puzzle which consists of a 9x9 matrix filled with numbers from 1 to 9. There are 9 sub matrices, each of dimension 3x3. The task is to fill each row and column  with numbers from 1 to 9 without repetition. Also each sub matrix can have only numbers from 1 to 9.

In this project, I have tried to automate the task of solving a Sudoku, given its image. The very task of solving the puzzle is simple, but the difficulty is in extracting the digits, given an image.

### Workflow
* Reading the Image
* Preprocessing the Image
* Finding the Contours & Extracting the Digits
* Reading the Digits
* Solving the Sudoku
* Projecting the Answer on the Image

## Reading the Image
The image is read using the CV2 module. It reads the image in BGR format, as a numpy array.

![The Original Image](https://github.com/thepankj/Sudoku-Solver/blob/main/images/sudoku_small.png)

## Preprocessing the Image
Before finding the contours of the puzzle, it needs to be preprocessed.
* First the image is made into grayscale
* Then is blurred. This reduces the resolution, thereby making it easier to detect edges
* Finally, the thresholding is applied, which makes the image binary, making the pixels stand out

![The preprocessing steps](https://github.com/thepankj/Sudoku-Solver/blob/main/images/preprocess.png)

## Finding the Contours & Extracting the Digits
After preprocessing, the contours of the image is found. To find the sudoku area, two conditions are used - the area of the contour should be maximum and the number of points in the contour should be 4 (because it's a square).

After this, the found Sudoku is divided into 9x9 boxes, each box contain an image of a digit or a blank box.

![The contours and Digits](https://github.com/thepankj/Sudoku-Solver/blob/main/images/contour.png)

## Reading the Digits
Each of the 81 boxes is read. They are passed into a [Digits Classifier](https://github.com/thepankj/Sudoku-Solver/blob/main/digitClassifier.h5) which classifies the digits into one of the 10 numbers.

If the probability of the prediction is below a certain threshold, the digit is appended as 0. 

## Solving the Sudoku
The digits found are preprocessed and passed into the [Sudoku Solver](https://github.com/thepankj/Sudoku-Solver/blob/main/sudokuSolver.py) which solves it and returns the solved array.

## Projecting the Answer on the Image
Finally, the solved answer is projected on the image. To do this, the answer is first warped into the sudoku area and then projected on the image.

![The final warping](https://github.com/thepankj/Sudoku-Solver/blob/main/images/warped.png)

# Final Output
![Final Output](https://github.com/thepankj/Sudoku-Solver/blob/main/images/comparison.png)

## Issues
* The Digit Classifier isn't perfect and sometimes returns wrong output
* The solver fails in low light
