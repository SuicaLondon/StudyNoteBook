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
randi(100, 4, 7)

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

round(B)
log2(B)
mod(B, 2)
sum(B) // each column
max(B) // each column
min(B) // each column
sort(B) // each column
// min, max, sort, sum, cumsum, mean, median, std, etc are columnwise by defauly

sum(B,2) // sum is taken along rows
max(B,2) // elementwise comparison between F and 2
max(B,[],2) // max is taken along rows
sort(B,2) // F is sorted along rows

// get the whole matrix
min(min(B))
sum(B(:))

A1 = reshape(A, 3, 10) // Rearranges the elements of a matrix A into a p x q matrix so that the linearindices remain unchanged. The total number of elements cannot change so this only works if p * q = numel(A)
```


## The Colon Operator
```
x = 0:0.1:2*pi;
x = linspace(0, 2*pi, 100);
```

## Referencing Subarrays
```
v(3: 5)
v(4: end)
A(:, 3:6)
A(:)
A([1, 3, 5:end], :)
```

## 2D Plot example
```
clear
close all
hold on
axis tight/equal
xlabel('x'), ylabel('y')
title('title')
axis([0, 10, 0, 10])
grid on, grid minor, box on

x=0:0.01:2*pi;
y=sin(4*pi);
plot(x, y, 'r', 'LineWidth', 2)
fill(x, y, 'red')
```

## Other API
```
k = sub2ind([n, m], i, j) // Finds the linear index of element (i, j) in an n x m matrix and stores the output in variable k

[i,j] = ind2sub([n,m],k) // Finds the row and column numbers of element k in an n x m matrix and stores the output in variables i and j
```
