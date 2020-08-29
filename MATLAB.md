## Basic Commands
```
clear
clc
exist varname
```

## help
```
help
doc apiName
```

## create Matrices
```
randi([10, 50], 3, 5) // create a 3 x 5 matrix filled with integers chosen randomly from the interval [10, 50]

matrixname(row, column)
```

## The Computing API
```
isprime(4)
isreal(3)
zeros(n,m) // returns an [n x m] matrix of 0s
ones(n,m) // returns an [n x m] matrix of 1s
eye(n,m) // returns an [n x m] matrix filled with 1s in the main diagonal and 0s elsewhere
// if A = eye(n,m) then A(i,j) = 1 if i=j and A(i,j) = 0 if i  j

rand(n,m) // returns an [n x m] matrix of random numbers uniformly distributed on the interval [0,1]
randn(n,m) // returns an [n x m] matrix of random numbers following the standard normal distribution N(0,1)
diag(v) // takes a vector v and creates a matrix with the elements of v along the main diagonal and 0s elsewhere.
size(A) // returns vector [n, m] (the dimensions of A)
det(A) // returns the determinant of square (n x n) matrix A
inv(A) // returns the inverse of square matrix A (if exists)
trace(A) // returns the sum of the elements in the main diagonal of square matrix A:
diag(A) // returns a vector which includes the elements in the main diagonal of matrix A
flipud(A) // flips (turns) matrix A upside down 
fliplr(A) // flips matrix A from left to right
```

## The Colon Operator
```
x = 0:0.1:2*pi;
x = linspace(0, 2*pi, 100);
