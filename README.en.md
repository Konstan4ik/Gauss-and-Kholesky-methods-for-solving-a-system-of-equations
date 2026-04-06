# Comparison of Gaussian and Cholesky Methods for Solving SLAE

## Project Description

This project implements two methods for solving systems of linear algebraic equations (SLAE) with a Hilbert matrix:

- **Gaussian elimination** (single division scheme)
- **Cholesky decomposition** (for symmetric positive-definite matrices)

For matrix sizes from 1 to 13, the solution is computed, execution time is measured, and the residual norm is evaluated.

## Hilbert Matrix

The elements of a Hilbert matrix of size \(n \times n\) are given by:
\[
H_{ij} = \frac{1}{i + j - 1}
\]

The Hilbert matrix is **symmetric** and **positive-definite**, which makes it suitable for Cholesky decomposition. However, it is **ill-conditioned**, especially for large \(n\), leading to increasing numerical errors.

## Project Structure

## Implemented Methods

### 1. Gaussian Elimination
- Forward elimination of variables
- Back substitution to find the solution
- Residual norm calculation

### 2. Cholesky Decomposition
- Decomposition \(G = C \cdot C^T\) (lower triangular matrix)
- Forward substitution: solve \(C y = B\)
- Back substitution: solve \(C^T x = y\)
- Positive-definiteness check

## Results

### Execution Time

| Size n | Gaussian (s) | Cholesky (s) |
|--------|--------------|--------------|
| 1      | 2.20e-06     | 4.90e-06     |
| 2      | 4.30e-06     | 6.20e-06     |
| ...    | ...          | ...          |
| 12     | 8.12e-05     | 6.72e-05     |
| 13     | 1.02e-04     | not applicable |

**Observations:**
- Cholesky is faster for \(n \leq 12\)
- At \(n = 13\), the Hilbert matrix ceases to be positive-definite within machine precision

### Residual Norm

| n | Gaussian | Cholesky |
|---|----------|----------|
| 1 | 0.00     | 0.00     |
| 2 | 5.00e-01 | 0.00     |
| 3 | 1.27     | 1.42e-14 |
| 4 | 2.50     | 3.22e-13 |
| 5 | 4.37     | 8.13e-12 |
| 6 | 7.16     | 4.69e-10 |
| 7 | 11.29    | 1.10e-08 |
| 8 | 17.35    | 3.29e-07 |
| 9 | 26.21    | 1.03e-05 |
| 10| 39.15    | 2.94e-04 |
| 11| 58.03    | 1.30e-02 |
| 12| 85.54    | 3.62e-01 |
| 13| 123.40   | ---      |

**Observations:**
- Gaussian residual grows rapidly with increasing \(n\)
- Cholesky produces significantly smaller residuals but also loses precision for large \(n\)
- At \(n = 13\), Cholesky decomposition fails due to loss of positive-definiteness

## Visualization
<img width="885" height="529" alt="image" src="https://github.com/user-attachments/assets/6458230e-da36-4b75-98b4-cdce23e3f632" />

The graph shows the execution time of both methods as a function of the matrix dimension. It can be seen that the Cholesky method is faster for all sizes where it is applicable.

```bash

