# Seperable_convolution
The program expects two command-line arguments: num-rows and num-columns, representing the height and width of the input matrix, respectively.

The input matrix (matrix_a) is created with random float values between 0 and 1, and it is copied to another matrix (matrix_c) for later comparison.

The Gaussian kernel (gaussian_kernel) is created using the create_kernel function. The COEFF macro defines the coefficient for the Gaussian distribution, and HALF_WIDTH defines the half-width of the convolution kernel.

The convolution is first computed on the CPU using the compute_gold function. This function performs the separable convolution by first convolving the input matrix along its rows and then convolving the resulting matrix along its columns using the Gaussian kernel. The result is stored in matrix_a.

The compute_on_device function is marked with FIXME because it's the part that should be implemented to compute the convolution on the GPU. This function transfers the necessary data (input matrix and kernel) to the GPU, launches CUDA kernels (convolve_rows_kernel_naive and convolve_columns_kernel_naive) to perform the row-wise and column-wise convolution, respectively, and then transfers the result back to the host (gpu_result).

After both CPU and GPU convolution, the program compares the results between matrix_a (CPU result) and gpu_result (GPU result) using the L1 norm. If the difference is within a certain epsilon (eps), the test is considered passed.

The program includes functions to print the convolution kernel (print_kernel) and the contents of the matrix (print_matrix) if the DEBUG macro is uncommented.

The program frees the allocated memory and exits.

To use the program, compile it using the provided Makefile by running make. After compilation, execute the program with the desired matrix dimensions as command-line arguments. The program will perform the convolution on both the CPU and GPU and compare the results for correctness.
