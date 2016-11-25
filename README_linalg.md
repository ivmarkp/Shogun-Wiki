# Internal linear algebra library

**NOTE:** Heavily deprecated as it will soon be replaced with Pan's [GSoC 2016 project](GSoC-2016-Final-Report-:-The-Shogun-Detox)


**Table of Contents**
- [Motivation](README_linalg#motivation)
- [Features of internal linear algebra library](README_linalg#features-of-internal-linear-algebra-library)
    * [For Shogun developers](README_linalg#for-shogun-developers)
        * [Using `linalg` operations](README_linalg#using-linalg-operations)
            * [Relying on globally set `linalg` backend](README_linalg#relying-on-globally-set-linalg-backend)
            * [Using operation specific `linalg` backend](README_linalg#using-operation-specific-linalg-backend)
    * [For `linalg` developers](README_linalg#for-linalg-developers)
        * [Understanding the backend setups](README_linalg#understanding-the-backend-setups)
        * [Understanding the module setups](README_linalg#understanding-the-module-setups)
        * [Understanding the global operations](README_linalg#understanding-the-global-operations)
        * [Understanding the backend specific implementation](README_linalg#understanding-the-backend-specific-implementation)

## Motivation
Linear algebra operations form the backbone for most of the computation components in any Machine Learning library. However, writing all of the required linear algebra operations from scratch is rather redundant and undesired, especially when we have some excellent open source alternatives. In Shogun, we prefer 
- [`Eigen3`](http://eigen.tuxfamily.org/index.php?title=Main_Page) for its speed and simplicity at the usage level,
- [`ViennaCL`](http://viennacl.sourceforge.net/) version 1.5 for GPU powered linear algebra operations, and
- [`Lapack`](http://www.netlib.org/lapack/) for its robustness and maturity.

For Shogun maintainers, however, the usage of different external libraries for different operations can lead to a painful task. 

- For example, consider some part of an algorithm originally written using `Eigen3` API. But a Shogun user wishes to use `ViennaCL` for that algorithm instead, hoping to obtain boosted performance utilizing a GPU powered platform. There is _no way_ of doing that without having the algorithm _rewritten_ by the developers using `ViennaCL`, which leads to _duplication_ of code and effort.
- Also, there is no way to do a _performance comparison_ for the developers while using _different_ external linear algebra libraries for the _same_ algorithm in Shogun code.
- It is also somewhat frustrating for a _new_ developer who has to invest significant amount of time and effort to learn each of these external APIs _just_ to add a new algorithm in Shogun.

## Features of internal linear algebra library
Shogun's **internal linear algebra library** (will be referred as `linalg` hereinafter) is a work-in-progress attempt to overcome these issues. We designed `linalg` as a modularized internal **header only** library in order to
- provide a uniform API for Shogun developers to choose any supported backend without having to worry about the syntactical differences in the external libraries' operations,
- handle native Shogun types for linear algebra operations without having to convert to external types,
- have the backend set for each operations at compile-time (for lesser runtime overhead) and therefore intended to be used internally by Shogun developers.

### For Shogun developers
----
#### Using `linalg` operations
The operations can be used in two ways:
##### Relying on globally set `linalg` backend
- Global setup is used whenever an operation **does not specify a particular backend**.
```c++
shogun::linalg::operation(arg1, ...);
```
- Preferred global backend can be specified via `cmake` options which sets that backend for **all** the `linalg` operations used in this fashion.
```bash
# this will set Eigen3 as the global linalg backend for all modules.
# Use -DUSE_VIENNACL for setting ViennaCL as global linalg backend instead
#
cmake -DUSE_EIGEN3
```
[for other cmake options, please refer to the [cmake wiki](README_cmake).]
- Module specific global setups can also be done via `cmake` options. We presently have 2 modules - `Core` and `Redux`.
```bash
# this will set Eigen3 for Redux module's global linalg backend
# and ViennaCL for Core module's global linalg backend.
cmake -DUSE_EIGEN3_REDUX -DUSE_VIENNACL_CORE
```
[see below for a complete list of supported operations under these modules].
- If no particular setup is specified in the `cmake` options, a `DEFAULT` backend is used as a global backend.
- Also, if module specific setup is specified but not for _all_ modules, then for the modules the setup is unspecified, `DEFAULT` backend is used.
[see below for the `DEFAULT` backend settings].
```bash
# this will set ViennaCL for Redux module's global linalg backend
# and Default for the rest of the modules
cmake -DUSE_VIENNACL_REDUX
```
##### Using operation specific `linalg` backend
- It is possible to use a **specific backend for a particular operation**, if desired, which then ignores the global or module specific setup and works with that particular backend. The backend can be specified using the `enum Backend`.
```c++
shogun::linalg::operation<Backend::backend_name>(arg1, ...);
```
- Currently supported backends are `EIGEN3`, `VIENNACL`, `NATIVE`.

**[The recommended practice for using `linalg` is to include just the file `linalg.h` (in `src/shogun/mathematics/linalg`) in the implementation of a Shogun algorithm (`.cpp` file). Please do not include this file in the `.h` file of an algorithm that is expected to be exposed to the modular API (exposed to SWIG). See [CustomKernel.cpp](https://github.com/shogun-toolbox/shogun/blob/develop/src/shogun/kernel/CustomKernel.cpp#L274) for an example.]**

### For `linalg` developers
----
The structure of `linalg` consists of three basic components
- backend identifier and module type specifier (in `linalg.h`)
- the operations exposed as global functions (in `linalg/internal/modules/`)
- the backend specific implementations (in `linalg/internal/implementation/`)

#### Understanding the backend setups
`enum class Backend` handles the backend identification in the operations. The `DEFAULT` backend would be the first constant defined. For example, if `cmake` finds all supported backends, the enum is defined as
```c++
// inside shogun::linalg namespace
enum class Backend
{
    EIGEN3, // will be 0
    VIENNACL, // will be 1
    NATIVE, // will be 2
    DEFAULT = 0 // therefore, will be EIGEN3
};
```
If only ViennaCL is found,
```c++
enum class Backend
{
    VIENNACL, // will be 0
    NATIVE, // will be 1
    DEFAULT = 0 // therefore, will be VIENNACL
};
```
If none of the supported backend libraries is found
```c++
enum class Backend
{
    NATIVE, // will be 0
    DEFAULT = 0 // therefore, will be NATIVE
};
```
`NATIVE` refers to Shogun's implementation which only provides a few operations. The operations specified with `NATIVE` backends work even in absence of any external linear algebra libraries. Therefore, while using the global backend, it is always safe to use those operations with a native implementation.

**The default backend is `Eigen3` (if found).**

#### Understanding the module setups
As mentioned earlier, the supported operations are clustered into different modules in order to provide module specific setup is desired. These modules are defined as structs with the backend information, e.g
```c++
template <enum Backend>
struct ModuleName
{
    // assuming that Eigen3 was set as the backend of this module
    const static Backend backend = Backend::EIGEN3;
};
```
In generic code, the backend set for a module can be inquired with `linalg_trait<ModuleName>::backend`.

#### Understanding the global operations
Coming soon.

#### Understanding the backend specific implementation
Coming soon.