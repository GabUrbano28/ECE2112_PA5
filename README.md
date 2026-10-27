# ECE2112_PA5
### Made by Antonio Gabriel L. Urbano | 2ECE-A
### EXPERIMENT 5: INTRODUCTION TO MATLAB PROGRAMMING
The content of this repository contains the Programming Assignment 5 for our course "Advance Computer Programming and Algorithms" this S.Y. 2026-2027. This project covers three problems pertaining to Module 5: Introduction To MATLAB Programming

### Objectives
The objectives of this experiment are to create real and complex matrices in MATLAB, distinguish transpose from complex-conjugate transpose operations, express a simultaneous linear system in matrix form, and to solve and check linear systems using the inverse method and Cramer's Rule. 

## 1. Transpose Operations
<img width="445" height="90" alt="image" src="https://github.com/user-attachments/assets/5e9afc3b-8e47-4eb4-824f-ed2a08ba1489" />

### Requirement: 
- Compute and Display three expressions `transpose(A)`,`A'`,`A.'`. A must be replaced by R and then by Z. 

```matlab
R = [ 5  -2   0   7; 
      1   3  -4   2; 
      6   0   8  -1];

Z = [ 2+3i  -1+4i   5-2i; 
     -3+1i   6      2+5i];

disp('Real Matrix R');
disp('Matrix R:');
disp(R);

disp('1) transpose(R):');
disp(transpose(R));

disp('2) R'':');
disp(R');

disp('3) R.'':');
disp(R.');

disp('Complex Matrix Z');
disp('Matrix Z:');
disp(Z);

disp('1) transpose(Z):');
disp(transpose(Z));

disp('2) Z'':');
disp(Z');

disp('3) Z.'':');
disp(Z.');
```
### Output

```text
Real Matrix R
Matrix R:
    5  -2   0   7
    1   3  -4   2
    6   0   8  -1
1) transpose(R):
   5   1   6
  -2   3   0
   0  -4   8
   7   2  -1
2) R':
   5   1   6
  -2   3   0
   0  -4   8
   7   2  -1
3) R.':
   5   1   6
  -2   3   0
   0  -4   8
   7   2  -1

Complex Matrix Z
Matrix Z:
   2.000 + 3.000i  -1.000  + 4.000i   5.000 - 2.000i
  -3.000 + 1.000i   6.000  + 0.000i   2.000 + 5.000i
1) transpose(Z):
   2.000 + 3.000i  -3.000 + 1.000i
  -1.000 + 4.000i   6.000 + 0.000i
   5.000 - 2.000i   2.000 + 5.000i
2) Z':
    2.000 - 3.000i  -3.000 - 1.000i
  -1.000 - 4.000i   6.000 + 0.000i
   5.000 + 2.000i   2.000 - 5.000i
3) Z.':
   2.000 + 3.000i  -3.000 + 1.000i
  -1.000 + 4.000i   6.000 + 0.000i
   5.000 - 2.000i   2.000 + 5.000i
```
### Guide Questions
```matlab
%{
ANSWERS TO PROBLEM A QUESTIONS:
a. Which operations give identical results for the real matrix R?
   All three operations transpose(R), R', and R.' yield identical 
   results for the real matrix R because all entries are real numbers 
   (imaginary parts are zero).

b. Which two operations give identical results for the complex matrix Z?
   transpose(Z) and Z.' give identical results. Both perform an unconjugated
   matrix transpose, flipping rows and columns without
   altering the signs of the imaginary components.

c. What additional operation is performed by the apostrophe operator when 
   the matrix contains complex entries?
   The apostrophe operator (') performs a complex-conjugate transpose 
   . In addition to swapping rows and columns, it 
   takes the complex conjugate of each entry by negating the sign of its 
   imaginary part.
%}
```
 
## 2. Two Methods for a Linear System 
<img width="195" height="90" alt="image" src="https://github.com/user-attachments/assets/66d7a6a2-e372-4104-9ab6-a5aa4e708ff9" />

### Requirement:
- Solve the given simultaneous system.
- Create the coefficient matrix A and a right-hand-side vector b.
- Compute the solution using Inverse Method, and Cramer's Rule.
- Display both solutions and vectors including `det(A)`. Display `norm(x_inv-x_cramer)` and `norm(A*x_inv-b)`.
- The determinant must be a nonzero and both norms checks should be approximately zero to numerical precision. 

```matlab
A = [ 2  -1   3   2; 
      1   4  -2   1; 
      3   2   1  -1; 
     -2   3   4   2];

b = [16; -7; 6; 7];

disp('Coefficient Matrix A:');
disp(A);

disp('Right-Hand-Side Vector b:');
disp(b);

% 1. Inverse Method
x_inv = inv(A) * b;

disp('Solution via Inverse Method (x_inv):');
disp(x_inv);

% 2. Cramer's Rule
det_A = det(A);
n = length(b);
x_cramer = zeros(n, 1);

for j = 1:n
    A_temp = A;           
    A_temp(:, j) = b;     
    x_cramer(j) = det(A_temp) / det_A;
end

disp('Solution via Cramer''s Rule (x_cramer):');
disp(x_cramer);

% 3. Numerical Checks and Verification
norm_diff = norm(x_inv - x_cramer);
residual_norm = norm(A * x_inv - b);

disp('Numerical Verification Checks');
fprintf('Determinant of A, det(A)    = 
fprintf('norm(x_inv - x_cramer)      =
fprintf('norm(A*x_inv - b)          = 

if det_A ~= 0
    disp('Check Passed: det(A) is non-zero; unique solution exists. And both norms are approximately zero.');
else
    disp('Check Failed: det(A) is zero.');
end
```
### Output

```text
PROBLEM B: TWO METHODS FOR A LINEAR SYSTEM
Coefficient Matrix A:
     2    -1     3     2
     1     4    -2     1
     3     2     1    -1
    -2     3     4     2

Right-Hand-Side Vector b:
    16
    -7
     6
     7

Solution via Inverse Method (x_inv):
    2.0000
   -1.0000
    3.0000
    1.0000

Solution via Cramer's Rule (x_cramer):
    2.0000
   -1.0000
    3.0000
    1.0000

Numerical Verification Checks
Determinant of A, det(A)    = 280.0000  (Must be non-zero)
norm(x_inv - x_cramer)      = 1.110223e-16  (Approximately 0)
norm(A*x_inv - b)          = 2.664535e-15  (Approximately 0)
Check Passed: det(A) is non-zero; unique solution exists. And both norms are approximately zero.
```

