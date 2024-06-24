#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define _2D_array_rows      (unsigned int) 3
#define _2D_array_columns   (unsigned int) 2

// *(*(_2d_arr+2)+0) = _2d_arr[2][0]

int **_2d_arr = NULL, my_2d_arr[_2D_array_rows][_2D_array_columns] = { {11, 22,}, {33, 44,}, {55, 66,}, };  

int **_2D_array_malloc(unsigned int rows, unsigned int columns) {

    int **ptr = malloc(sizeof(int) * rows);                                                 // Ptr to 1st 1D array of 2D array.
    *ptr = malloc(sizeof(int) * (rows * columns));                                          // Ptr to 1st element of 1st 1D array of 2D array,
                                                                                            // this allocated memory for all elements of 2D array.

    for(unsigned int i = 0; i < rows - 1; i++) {

        ptr[i+1] = ptr[i] + columns;                                                        // set address offset by columns width for correct calling each 1D array of 2D array
        
    }

    return ptr;                                                                             // this ptr point to continuous 2D array, allocated by malloc (without mem fragmentation)

}

int main() {

    _2d_arr = _2D_array_malloc(_2D_array_rows, _2D_array_columns);

    memcpy(*_2d_arr, *my_2d_arr, (sizeof(int) * (_2D_array_rows * _2D_array_columns)));     // now you can easy work with 2D array like as 1D array...

    printf("%d, %d, %d\r\n", &_2d_arr[0][0], &_2d_arr[1][0], &_2d_arr[2][0]); 

    return 0;

}
