---
layout: post
title: "Implementing a sparse matrix using HashMap in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Sparse matrices are matrices that have a significant number of zero values compared to the total number of elements. To efficiently represent such matrices in computer programs, we can use a HashMap data structure.

In Java, HashMap is a key-value based data structure that provides constant-time complexity for basic operations like insertion, deletion, and lookup. By utilizing this data structure, we can effectively store and retrieve non-zero values in a sparse matrix, avoiding unnecessary memory allocation for zero values.

Let's see how we can implement a sparse matrix using a HashMap in Java.

## Creating the Sparse Matrix Class

```java
import java.util.HashMap;

public class SparseMatrix {
    private int rows;
    private int columns;
    private HashMap<String, Integer> matrix;

    public SparseMatrix(int rows, int columns) {
        this.rows = rows;
        this.columns = columns;
        this.matrix = new HashMap<>();
    }

    public void setValue(int row, int column, int value) {
        if (row < 0 || row >= rows || column < 0 || column >= columns) {
            throw new IndexOutOfBoundsException("Invalid matrix index");
        }
        String key = row + "," + column;
        if (value == 0) {
            matrix.remove(key);
        } else {
            matrix.put(key, value);
        }
    }

    public int getValue(int row, int column) {
        if (row < 0 || row >= rows || column < 0 || column >= columns) {
            throw new IndexOutOfBoundsException("Invalid matrix index");
        }
        String key = row + "," + column;
        return matrix.getOrDefault(key, 0);
    }
}
```

In the above code, we have defined a `SparseMatrix` class that utilizes a HashMap (`matrix`) to store the non-zero values of the matrix. The `setValue()` method allows us to set a specific value at the given row and column index, while the `getValue()` method retrieves the value at a given index. If a value is set to zero, we remove it from the HashMap to maintain sparsity.

## Using the Sparse Matrix Class

We can now use the `SparseMatrix` class to create and manipulate sparse matrices. Here's an example:

```java
public class Main {
    public static void main(String[] args) {
        int rows = 5;
        int columns = 5;

        SparseMatrix sparseMatrix = new SparseMatrix(rows, columns);

        sparseMatrix.setValue(0, 0, 1);
        sparseMatrix.setValue(1, 1, 2);
        sparseMatrix.setValue(3, 2, 3);
        sparseMatrix.setValue(4, 3, 4);

        System.out.println(sparseMatrix.getValue(0, 0));
        System.out.println(sparseMatrix.getValue(1, 1));
        System.out.println(sparseMatrix.getValue(2, 2));
        System.out.println(sparseMatrix.getValue(3, 2));
        System.out.println(sparseMatrix.getValue(4, 3));
        System.out.println(sparseMatrix.getValue(4, 4));
    }
}
```

In the above example, we create a 5x5 sparse matrix using the `SparseMatrix` class. We set a few non-zero values at different indices and then retrieve the values using the `getValue()` method. The output demonstrates successful retrieval of non-zero values and default zero value for missing indices.

Sparse matrices provide an efficient way to store and process large matrices with mostly zero values. By using a HashMap to implement a sparse matrix, we can reduce memory usage and improve performance.

_References:_
- [HashMap documentation](https://docs.oracle.com/en/java/javase/16/docs/api/java.base/java/util/HashMap.html)
- [Sparse matrix - Wikipedia](https://en.wikipedia.org/wiki/Sparse_matrix)
- [Data Structure to Store Sparse Matrix](https://www.geeksforgeeks.org/sparse-matrix-representations-set-3-csr/)