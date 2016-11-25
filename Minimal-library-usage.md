##The minimal libshogun example

    #include <shogun/base/init.h>

    using namespace shogun;

    int main(int argc, char** argv)
    {
        init_shogun_with_defaults();
        exit_shogun();
        return 0;
    }

It obviously does nothing (apart form initializing and destroying a couple of global shogun objects internally).
Check [INTERFACES.md](https://github.com/shogun-toolbox/docs/blob/master/INTERFACES.md) on how to compile and run it. See the [website API examples](http://shogun.ml/examples) and [EXAMPLES.md](https://github.com/shogun-toolbox/docs/blob/master/EXAMPLES.md) for more C++ examples.

## Redirecting output
In case one wants to redirect shoguns output functions `SG_DEBUG`, `SG_INFO`, etc one has to pass them to init_shogun() as parameters

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

    init_shogun(&print_message, &print_warning,	&print_error);

## Some action and manual semi-automatic managment
Let's include some header files, and create some features and a gaussian kernel (note this listing is not maintained, so it just serves illustration purposes)

    #include <shogun/labels/Labels.h>
    #include <shogun/features/DenseFeatures.h>
    #include <shogun/kernel/GaussianKernel.h>
    #include <shogun/classifier/svm/LibSVM.h>
    #include <shogun/base/init.h>
    #include <shogun/lib/common.h>
    #include <shogun/io/SGIO.h>

    using namespace shogun;


    int main(int argc, char** argv)
    {
    	init_shogun_with_defaults();

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
supplying pointers to arrays allocated with `new[]` will make shogun objects own
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
above accessing labels after the call to `SG_UNREF(svm)` will cause a
segmentation fault as the Label object was already destroyed in the SVM
destructor. You can do this by `SG_REF(obj)`. To decrement the reference count of
an object, call `SG_UNREF(obj)` which will also automagically destroy it if the
counter is <= 0 and set `obj=NULL` only in this case

**Note:** `SG_REF` and `SG_UNREF` are deprecated as of 2016. We are moving towards C++11 smart pointers and/or our own [`some`](https://github.com/shogun-toolbox/shogun/blob/develop/src/shogun/base/some.h) trick. Existing Shogun code, however, is full of `SG_REF`.

## Extending the base class
Generally, all shogun C++ Objects are prefixed with C, e.g. `CSVM` and derived
from `CSGObject`. Since variables in the upper class hierarchy, need to be
initialized upon construction of the object, the constructor of base class needs
to be called in the constructor, e.g. `CSVM` calls `CKernelMachine`, `CKernelMachine`
calls `CClassifier` which finally calls `CSGObject`.

For example if you implement your own `SVM` called `MySVM` you would in the
constructor do

    class MySVM : public CSVM
    {
        MySVM( ) : CSVM()
        {
            ...
        }
    };

In case you got your object working we will happily integrate it into shogun
provided you follow our development cycle outlines in [DEVELOPING.md](https://github.com/shogun-toolbox/docs/blob/master/DEVELOPING.md)