//Straussen
#include <stdio.h>
#include <stdlib.h>

int** allocate_matrix(int size) {
    int** matrix = (int**)malloc(size * sizeof(int*));
    for (int i = 0; i < size; i++) {
        matrix[i] = (int*)malloc(size * sizeof(int));
    }
    return matrix;
}

void free_matrix(int** matrix, int size) {
    for (int i = 0; i < size; i++) {
        free(matrix[i]);
    }
    free(matrix);
}

void add_matrices(int size, int** A, int** B, int** result) {
    for (int i = 0; i < size; i++) {
        for (int j = 0; j < size; j++) {
            result[i][j] = A[i][j] + B[i][j];
        }
    }
}

void subtract_matrices(int size, int** A, int** B, int** result) {
    for (int i = 0; i < size; i++) {
        for (int j = 0; j < size; j++) {
            result[i][j] = A[i][j] - B[i][j];
        }
    }
}

void strassen_multiply(int size, int** A, int** B, int** C) {
    if (size == 1) {
        C[0][0] = A[0][0] * B[0][0];
        return;
    }

    int newSize = size / 2;
    int** A11 = allocate_matrix(newSize);
    int** A12 = allocate_matrix(newSize);
    int** A21 = allocate_matrix(newSize);
    int** A22 = allocate_matrix(newSize);
    int** B11 = allocate_matrix(newSize);
    int** B12 = allocate_matrix(newSize);
    int** B21 = allocate_matrix(newSize);
    int** B22 = allocate_matrix(newSize);
    int** C11 = allocate_matrix(newSize);
    int** C12 = allocate_matrix(newSize);
    int** C21 = allocate_matrix(newSize);
    int** C22 = allocate_matrix(newSize);
    int** M1 = allocate_matrix(newSize);
    int** M2 = allocate_matrix(newSize);
    int** M3 = allocate_matrix(newSize);
    int** M4 = allocate_matrix(newSize);
    int** M5 = allocate_matrix(newSize);
    int** M6 = allocate_matrix(newSize);
    int** M7 = allocate_matrix(newSize);
    int** tempA = allocate_matrix(newSize);
    int** tempB = allocate_matrix(newSize);

    for (int i = 0; i < newSize; i++) {
        for (int j = 0; j < newSize; j++) {
            A11[i][j] = A[i][j];
            A12[i][j] = A[i][j + newSize];
            A21[i][j] = A[i + newSize][j];
            A22[i][j] = A[i + newSize][j + newSize];
            B11[i][j] = B[i][j];
            B12[i][j] = B[i][j + newSize];
            B21[i][j] = B[i + newSize][j];
            B22[i][j] = B[i + newSize][j + newSize];
        }
    }

    add_matrices(newSize, A11, A22, tempA);
    add_matrices(newSize, B11, B22, tempB);
    strassen_multiply(newSize, tempA, tempB, M1);

    add_matrices(newSize, A21, A22, tempA);
    strassen_multiply(newSize, tempA, B11, M2);

    subtract_matrices(newSize, B12, B22, tempB);
    strassen_multiply(newSize, A11, tempB, M3);

    subtract_matrices(newSize, B21, B11, tempB);
    strassen_multiply(newSize, A22, tempB, M4);

    add_matrices(newSize, A11, A12, tempA);
    strassen_multiply(newSize, tempA, B22, M5);

    subtract_matrices(newSize, A21, A11, tempA);
    add_matrices(newSize, B11, B12, tempB);
    strassen_multiply(newSize, tempA, tempB, M6);

    subtract_matrices(newSize, A12, A22, tempA);
    add_matrices(newSize, B21, B22, tempB);
    strassen_multiply(newSize, tempA, tempB, M7);

    add_matrices(newSize, M1, M4, tempA);
    subtract_matrices(newSize, tempA, M5, tempB);
    add_matrices(newSize, tempB, M7, C11);

    add_matrices(newSize, M3, M5, C12);

    add_matrices(newSize, M2, M4, C21);

    add_matrices(newSize, M1, M3, tempA);
    subtract_matrices(newSize, tempA, M2, tempB);
    add_matrices(newSize, tempB, M6, C22);

    for (int i = 0; i < newSize; i++) {
        for (int j = 0; j < newSize; j++) {
            C[i][j] = C11[i][j];
            C[i][j + newSize] = C12[i][j];
            C[i + newSize][j] = C21[i][j];
            C[i + newSize][j + newSize] = C22[i][j];
        }
    }

    free_matrix(A11, newSize);
    free_matrix(A12, newSize);
    free_matrix(A21, newSize);
    free_matrix(A22, newSize);
    free_matrix(B11, newSize);
    free_matrix(B12, newSize);
    free_matrix(B21, newSize);
    free_matrix(B22, newSize);
    free_matrix(C11, newSize);
    free_matrix(C12, newSize);
    free_matrix(C21, newSize);
    free_matrix(C22, newSize);
    free_matrix(M1, newSize);
    free_matrix(M2, newSize);
    free_matrix(M3, newSize);
    free_matrix(M4, newSize);
    free_matrix(M5, newSize);
    free_matrix(M6, newSize);
    free_matrix(M7, newSize);
    free_matrix(tempA, newSize);
    free_matrix(tempB, newSize);
}

void print_matrix(int size, int** matrix) {
    for (int i = 0; i < size; i++) {
        for (int j = 0; j < size; j++) {
            printf("%d ", matrix[i][j]);
        }
        printf("\n");
    }
}

int main() {
    int size = 4; 
    int** A = allocate_matrix(size);
    int** B = allocate_matrix(size);
    int** C = allocate_matrix(size);

    for (int i = 0; i < size; i++) {
        for (int j = 0; j < size; j++) {
            A[i][j] = i + j;
            B[i][j] = i - j;
        }
    }

    strassen_multiply(size, A, B, C);

    printf("Matrix A:\n");
    print_matrix(size, A);
    printf("Matrix B:\n");
    print_matrix(size, B);
    printf("Matrix C (A * B):\n");
    print_matrix(size, C);

    free_matrix(A, size);
    free_matrix(B, size);
    free_matrix(C, size);

    return 0;
}
