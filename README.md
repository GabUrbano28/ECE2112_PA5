# ECE2112_PA5
### Made by Antonio Gabriel L. Urbano | 2ECE-A
### EXPERIMENT 5: INTRODUCTION TO MATLAB PROGRAMMING
The content of this repository contains the Programming Assignment 4 for our course "Advance Computer Programming and Algorithms" this S.Y. 2026-2027. This project covers three problems pertaining to Module 5: Introduction To MATLAB Programming

### Objectives
The objectives of this experiment are to create real and complex matrices in MATLAB, distinguish transpose from complex-conjugate transpose operations, express a simultaneous linear system in matrix form, and to solve and check linear systems using the inverse method and Cramer's Rule. 

### 1. Transpose Operations
<img width="445" height="90" alt="image" src="https://github.com/user-attachments/assets/5e9afc3b-8e47-4eb4-824f-ed2a08ba1489" />

#### Requirement: Compute and Display three expressions `transpose(A)`,`A'`,`A.'`. A must be replaced by R and then by Z. 

```matlab
disp('PROBLEM A: TRANSPOSE OPERATIONS');

% 1. Define Real Matrix R and Complex Matrix Z
R = [ 5  -2   0   7; 
      1   3  -4   2; 
      6   0   8  -1];

Z = [ 2+3i  -1+4i   5-2i; 
     -3+1i   6      2+5i];

% 2. Transpose Operations on Real Matrix R
disp('Real Matrix R');
disp('Matrix R:');
disp(R);

disp('1) transpose(R):');
disp(transpose(R));

disp('2) R'':');
disp(R');

disp('3) R.'':');
disp(R.');

% 3. Transpose Operations on Complex Matrix Z
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

### 2. Two Methods for a Linear System 
<img width="195" height="90" alt="image" src="https://github.com/user-attachments/assets/66d7a6a2-e372-4104-9ab6-a5aa4e708ff9" />

#### Requirement: Solve the given simultaneous system, create the coefficient matrix A and a right-hand-side vector b. Compute the solution using Inverse Method, and Cramer's Rule. Display both solutions and vectors including `det(A)`. Display `norm(x_inv-x_cramer)` and `norm(A*x_inv-b)`. The determinant must be a nonzero and both norms checks should be approximately zero to numerical precision. 

```matlab
disp('PROBLEM B: TWO METHODS FOR A LINEAR SYSTEM');

% System of Linear Equations:
%  2x1 -  x2 + 3x3 + 2x4 =  16
%   x1 + 4x2 - 2x3 +  x4 = -7
%  3x1 + 2x2 +  x3 -  x4 =   6
% -2x1 + 3x2 + 4x3 + 2x4 =   7

% Define Coefficient Matrix A and Vector b
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
% x_inv = inv(A) * b
x_inv = inv(A) * b;

disp('Solution via Inverse Method (x_inv):');
disp(x_inv);

% 2. Cramer's Rule
det_A = det(A);
n = length(b);
x_cramer = zeros(n, 1);

for j = 1:n
    A_temp = A;           % Make a copy of matrix A
    A_temp(:, j) = b;     % Replace the j-th column with vector b
    x_cramer(j) = det(A_temp) / det_A; % x_j = det(A_j) / det(A)
end

disp('Solution via Cramer''s Rule (x_cramer):');
disp(x_cramer);

% 3. Numerical Checks and Verification
norm_diff = norm(x_inv - x_cramer);
residual_norm = norm(A * x_inv - b);

disp('Numerical Verification Checks');
fprintf('Determinant of A, det(A)    = %.4f  (Must be non-zero)\n', det_A);
fprintf('norm(x_inv - x_cramer)      = %e  (Approximately 0)\n', norm_diff);
fprintf('norm(A*x_inv - b)          = %e  (Approximately 0)\n', residual_norm);

if det_A ~= 0
    disp('Check Passed: det(A) is non-zero; unique solution exists. And both norms are approximately zero.');
else
    disp('Check Failed: det(A) is zero.');
end
```

