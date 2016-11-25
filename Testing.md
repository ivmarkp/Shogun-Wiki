# Testing in Shogun

## Basics
There are three types of tests that can be executed locally, C++ unit tests, running the API examples, and integration testing the results of the API examples. To activate them locally, enable the `-DENABLE_TESTING=ON` cmake switch before running cmake. Which tests are activated depends on your configuration. All activated tests can be executed with 

    make && make test

The first `make` is necessary as some (not all) tests need to be compiled first.

Sometimes, it is useful to run a single test, which can be done via [ctest](https://cmake.org/Wiki/CMake/Testing_With_CTest), for example

    ctest -R unit-LibSVR
    ctest -R generated_cpp-binary_classifier-kernel_svm
    ctest -R integration_meta_cpp-binary_classifier-kernel_svm -V

If you are interested in details how the test is executed (command, variables, directory), add the `-V` option. Further details can be extracted from the `CMakeLists.txt` configuration files in the tests folder.

## C++ Unit tests
These are based on the [googletest](https://github.com/google/googletest) framework. You can compile them with

    make shogun-unit-test

You can execute single tests via `ctest`, or via directly executing the unit test binary and passing it a filter, which gives a more grained control over which sub-tests are executed

    ./tests/unit/shogun-unit-test --gtest_filter=GaussianProcessRegression.apply_*

Note that wildcards are allowed. Running single sub-tests is useful if you want to use a memory checker such as [valgrind](http://valgrind.org/) (or a debugger such as [gdb](https://www.gnu.org/software/gdb/))

    valgrind ./shogun-unit-test --gtest_filter=GaussianProcessRegression.apply_apply_regression
    gdb ./shogun-unit-test --gtest_filter=GaussianProcessRegression.apply_apply_regression

If you do that, you might want to compile with debugging symbols and without compiler optimizations, which is the cmake switch `-DCMAKE_BUILD_TYPE=Debug`

**All your C++ unit tests should be checked to not leak memory!**

We aim to write clear, minimal, yet exhaustive tests of basic building blocks in Shogun. Whenever you send us C++ code, we will ask you for a unit test for it. We do test numerical results as compared to reference implementations (e.g. in Python), as well as corner cases, consistency etc. Check existing tests if unsure.

## API example tests
