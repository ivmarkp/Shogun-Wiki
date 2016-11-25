GETTING STARTED     {#developer}
===============

**NOTE**: This page is deprecated and will soon be replaced by [Developing-Shogun](Developing-Shogun)

Shogun is split up into libshogun which contains all the machine learning
algorithms and 'static interfaces' helpers,
the static interfaces python_static, octave_static, matlab_static, r_static and
the modular interfaces python_modular, octave_modular and r_modular (all found
in the src/interfaces/ subdirectory with corresponding name). See 
[INSTALL](https://github.com/shogun-toolbox/shogun/wiki/INSTALL) for
instructions on how to install shogun.

In case one wants to extend shogun the best way is to start using its library.
This can be easily done as a number of examples in examples/libshogun document.

The simplest libshogun based program would be

    #include <shogun/base/init.h>

    using namespace shogun;

    int main(int argc, char** argv)
    {
        init_shogun();
        exit_shogun();
        return 0;
    }

which could be compiled with `g++ -lshogun minimal.cpp -o minimal` or
`g++ minimal.cpp -lshogun -o minimal` (if the former command does not work, you
might need to run `ldconfig` to configure dynamic linker run-time bindings after
the first time installation) and obviously does nothing (apart form initializing
and destroying a couple of global shogun objects internally).

In case one wants to redirect shoguns output functions SG_DEBUG, SG_INFO,
SG_WARN, SG_ERROR, SG_PRINT etc, one has to pass them to init_shogun() as
parameters like this

    void print_message(FILE* target, const char* str)
    {
        fprintf(target, "%s", str);
    }

    void print_warning(FILE* target, const char* str)
    {
        fprintf(target, "%s", str);
    }

    void print_error(FILE* target, const char* str)
    {
        fprintf(target, "%s", str);
    }

    init_shogun(&print_message, &print_warning,
    					&print_error);

To finally see some action one has to include the appropriate header files,
e.g. we create some features and a gaussian kernel

    #include <shogun/labels/Labels.h>
    #include <shogun/features/DenseFeatures.h>
    #include <shogun/kernel/GaussianKernel.h>
    #include <shogun/classifier/svm/LibSVM.h>
    #include <shogun/base/init.h>
    #include <shogun/lib/common.h>
    #include <shogun/io/SGIO.h>

    using namespace shogun;

    void print_message(FILE* target, const char* str)
    {
    	fprintf(target, "%s", str);
    }

    int main(int argc, char** argv)
    {
    	init_shogun(&print_message);

    	// create some data
    	SGMatrix<float64_t> matrix(2,3);
    	for (int32_t i=0; i<6; i++)
    		matrix.matrix[i]=i;

    	// create three 2-dimensional vectors
    	// shogun will now own the matrix created
    	CDenseFeatures<float64_t>* features= new CDenseFeatures<float64_t>();
    	features->set_feature_matrix(matrix);

    	// create three labels
    	CBinaryLabels* labels=new CBinaryLabels(3);
    	labels->set_label(0, -1);
    	labels->set_label(1, +1);
    	labels->set_label(2, -1);

    	// create gaussian kernel with cache 10MB, width 0.5
    	CGaussianKernel* kernel = new CGaussianKernel(10, 0.5);
    	kernel->init(features, features);

    	// create libsvm with C=10 and train
    	CLibSVM* svm = new CLibSVM(10, kernel, labels);
    	svm->train();

    	// classify on training examples
    	for (int32_t i=0; i<3; i++)
    		SG_SPRINT("output[%d]=%f\n", i, svm->apply_one(i));

    	// free up memory
    	SG_UNREF(svm);

    	exit_shogun();
    	return 0;

    }

Now you probably wonder why this example does not leak memory. First of all,
supplying pointers to arrays allocated with new[] will make shogun objects own
these objects and will make them take care of cleaning them up on object
destruction. Then, when creating shogun objects they keep a reference counter
internally. Whenever a shogun object is returned or supplied as an argument to
some function its reference counter is increased, for example in the example
above

    CLibSVM* svm = new CLibSVM(10, kernel, labels);

increases the reference count of kernel and labels. On destruction the
reference counter is decreased and the object is freed if the counter is <= 0.

It is therefore your duty to prevent objects from destruction if you keep a
handle to them globally *which you still intend to use later*. In the example
above accessing labels after the call to SG_UNREF(svm) will cause a
segmentation fault as the Label object was already destroyed in the SVM
destructor. You can do this by SG_REF(obj). To decrement the reference count of
an object, call SG_UNREF(obj) which will also automagically destroy it if the
counter is <= 0 and set obj=NULL only in this case.


Generally, all shogun C++ Objects are prefixed with C, e.g. CSVM and derived
from CSGObject. Since variables in the upper class hierarchy, need to be
initialized upon construction of the object, the constructor of base class needs
to be called in the constructor, e.g. CSVM calls CKernelMachine, CKernelMachine
calls CClassifier which finally calls CSGObject.

For example if you implement your own SVM called MySVM you would in the
constructor do

    class MySVM : public CSVM
    {
        MySVM( ) : CSVM()
        {
            ...
        }
    };

In case you got your object working we will happily integrate it into shogun
provided you follow a number of basic coding conventions detailed below (see
FORMATTING for formatting instructions, MACROS on how to use and name macros,
TYPES on which types to use, FUNCTIONS on how functions should look like and
NAMING CONVENTIONS for the naming scheme.

*CODING STYLE:*
See [here](Code-style)

*VERSIONING SCHEME:*

The git repo for the project is hosted on GitHub at
https://github.com/shogun-toolbox/shogun. To get started, create your own fork
and clone it
([howto](https://help.github.com/articles/fork-a-repo "GitHub help - Fork a repo")).
Remember to set the upstream remote to the main repo by:

    git remote add upstream git://github.com/shogun-toolbox/shogun.git

Its recommended to create local branches, which are linked to branches from
your remote repository.  This will make "push" and "pull" work as expected:

    git checkout --track origin/master
    git checkout --track origin/develop

Each time you want to develop new feature / fix a bug / etc consider creating
new branch using:

    git checkout -b new_feature_name

While being on new_feature_name branch, develop your code, commit things and do
everything you want.

Once your feature is ready (please consider larger commits that keep shogun in
compileable state), rebase your new_feature_name branch on upstream/develop
with:

    git fetch upstream
    git checkout develop
    git rebase upstream/develop
    git checkout new_feature_name
    git rebase develop

Now you can push it to your origin repository:

    git push

And finally send a pull request (PR) to the develop branch of the shogun
repository in github.


- Why rebasing?

    What rebasing does is, in short, "Forward-port local commits to the updated
    upstream head". A longer and more detailed illustration with nice figures
    can be found at http://git-scm.com/book/en/v2/Git-Branching-Rebasing. So
    rebasing (instead of merging) makes the main "commit-thread" of the repo a
    simple series.

    Rebasing before issuing a pull request also enable us to find and fix any
    potential conflicts early at the developer side (instead of at the one who
    merges your pull request).

- Multiple pull requests

    You can have multiple pull requests by creating multiple branches. Github
    only tracks the branch names you used for identify the pull request. So when
    you push new commits to your remote branch at github, the pull request will
    "update" accordingly.

- Non-fast-forward error

    This error happens when:

  1. `git checkout -b my-branch`
  2. ... do something ...
  3. ... rebasing ...
  4. `git push origin my-branch`
  5. ... do more thing ...
  6. ... rebasing ...
  7. `git push origin my-branch`

    then git will complain about non-fast-forward error and not pushing into the
    remote my-branch branch. This is because the first push has already created
    the my-branch branch in origin. Later when you run rebasing, which is a
    destructive operation for the local history. Since the local history is no
    longer the same as those in the remote branch, pushing is not allowed.

    Solution for this situation is to delete your remote branch by

        git push origin :my-branch

    and push again by

        git push origin my-branch

    note deleting your remote branch will not delete your pull request
    associated with that branch. And as long as you push your branch there
    again, your pull request will be OK.

- Unit testing/Pre-commit hook
    As shogun-toolbox is getting bigger and bigger code-reviews of pull requests
    are getting harder and harder. In order to avoid breaking the functionality
    of the existing code, we highly encourage contributors of shogun to use the
    supplied unit testing, that is based on Google C++ Mock Framework.

    Use cmake/ccmake with the `ENABLE_TESTING` switched on and `make GoogleMock`
    to download and compile Google Mock.

    For example:
  ```
  mkdir build
  cd build
  cmake -DENABLE_TESTING=on ..
  make GoogleMock
  make unit-tests     # if you want to compile and run the unit-tests
  ```
    If GoogleMock complains for some reason (Hash mismatch after download etc.)
    then manually download GoogleMock from
    [this link](http://googlemock.googlecode.com/files/gmock-1.7.0.zip),
    replace it in `shogun/third-party/GoogleMock` and run `make GoogleMock`
    again. `shogun/third-party` dir is created after you do
    `cmake -DENABLE_TESTING=on ..`.

    Once it's detected if you add new classes to the code please define some
    basic unit tests for them under ./tests/unit (see some of the examples under
    that directory). As one can see the naming convention for files that
    contains the unit tests are: \<classname\>_unittest.cc

    Before committing or sending a pull request please run `make unit-tests`
    under root directory in order to check that nothing has been broken by the
    modifications and the library is still acting as it's intended.

    One possible way to do this automatically is to add into your pre-commit
    hook the following code snippet (.git/hook/pre-commit):
  ```
  #!/bin/sh

  # run unit testing for basic checks
  # and only let commiting if the unit testing runs successfully
  make unit-tests
  ```
    This way before each commit the unit testing will run automatically and if
    it fails it won't let you commit until you don't fix the problem (or remove
    the
    pre-commit script :P)

    Note that the script should be executable, i.e.

        chmod +x .git/hook/pre-commit

    You can also test all the examples in shogun/exapmles to check whether your
    configuration and environment is totally okay. Please note that some of the
    examples are dependent on data sets, which should be downloaded beforehand,
    and so that you can pass all the tests of those examples. Downloading data
    can be easily done by calling a git command (please refer to
    [README_data.md](https://github.com/shogun-toolbox/shogun/blob/develop/doc/md/README_data.md)).
    Afterwards, you can test the examples by:

        make test

To make a release, adjust the [NEWS](NEWS) file properly, i.e. date, release
version (like 3.0.0), adjust the soname if required
(cf. [README_soname](README_soname.md)) and if a new data version is required
add that too.
