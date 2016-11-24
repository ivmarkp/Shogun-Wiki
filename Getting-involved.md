## Getting involved with Shogun
Welcome to our FAQ on how to get involved with Shogun and Google Summer of Code. While this FAQ is mostly written for GSoC students, it also contains lots of useful tips for getting involved in general. If you can't find what you're looking for, contact us. 

## How to start
Your first step is small and simple: **pick an [entrance task](https://github.com/shogun-toolbox/shogun/issues?q=is%3Aopen+is%3Aissue+label%3Aentrance)** you like and **submit a small patch that solves it**. 

We've compiled a list of [**example patches**](GSoC-2016-example-patches) to give you a better idea of what we're looking for.

Generally, we won't assign you an issue to solve because we think that you should be solving the one you're most interested in. It's worth having a look at the mailing list archives, to see whether other people might already be working on this. Of course, if you have a technical question about a particular issue you can talk to the people who submitted it. 

And that's it - you've made a start :)

## Google Summer of Code
If you are here to join us in GSoC, please have a look at our [past projects](GSoC-follow-up-blog-posts) to get a good feeling for GSoC with Shogun means.

## What we are looking for
We have successfully participated in four summers of GSoC. This year we want to take Shogun up another notch with your help:


 * if you are interested in Machine Learning (ML), Statistics, Optimization, framework design, or just C++ coding
 * if you enjoy working with a vibrant team of experienced ML scientists
 * if you always wanted to join open-source 

then GSoC with Shogun is for you! You'll spend the summer working with our enthusiastic and open-minded team of developers who are creating one of the largest ML toolboxes out there.

GSoC is a great program and every year we have lots of fun. You can read some blog posts about our past participations [here](GSoC_follow_ups).

## Female students
Without exception, currently all Shogun developers are male. We would like to change this - to create a nicer atmosphere and to [work more effectively](http://www.nytimes.com/2015/01/18/opinion/sunday/why-some-teams-are-smarter-than-others.html?_r=0). In order to achieve a more balanced gender distribution in GSoC, **we are in particular looking for female students to apply to us**.

## Applicability - “Am I good enough to do this?”
If your answer to this question is “YES!”, then you are the right person ;) The main skill that we are looking for is motivation - we greatly appreciate people who take initiative, come up with creative ideas and are self-organised in making them happen (with our guidance of course). Since Shogun is about ML, most projects are technically involved in some sense: probability distributions, linear algebra, optimization, as well as object-oriented programing, compilers, and git should be things that do not scare you (not too much at least ;) ). However, we do not require you to be a master in the topics that the projects are about, GSoC is also about enjoying learning new things and all of us started from zero.

## First steps - “Shogun seems huge (and messy), where do I start?”
A good (and sometimes already challenging) start into Shogun is to try to install it. In particular, check out the development repository on [github](https://github.com/shogun-toolbox/shogun/tree/develop) and compile/install it in debug mode with a modular interface of your choice (say Python). If you have troubles doing so, have a look at the [wiki](https://github.com/shogun-toolbox/shogun/wiki) and the [documentation files)](https://github.com/shogun-toolbox/shogun/tree/develop/doc). If you still have trouble, ask us. If you think that your issue might be worth being documented, we greatly appreciate if you then would update the corresponding README (this is what open-source is about). After having installed Shogun, try running the [C++](https://github.com/shogun-toolbox/shogun/tree/develop/examples/undocumented/libshogun) and the [modular](https://github.com/shogun-toolbox/shogun/tree/develop/examples/undocumented/python_modular) examples. You can also try to run the [unit](https://github.com/shogun-toolbox/shogun/tree/develop/tests/unit) and [integration](https://github.com/shogun-toolbox/shogun/tree/develop/tests/integration) tests that we use to keep Shogun working (more on those later). Once everything is set up and working, have a look at our [IPython notebooks](http://www.shogun-toolbox.org/page/documentation/notebook), and maybe try to run them locally. Those contain writeups on last year’s GSoC projects. Pick an example (C++, (python,octave,java)-modular, IPython) of your choice and play with it. You could for example modify the data that is used, or plug in another algorithm. Again, if you have any problems with that, please get back to us, which brings us to the next point.

## Communication - “I don’t want to bother the Shogun developers with my stupid question”
Wrong! Communication is among the most important things in GSoC and in open-source in general. We will not find out what you are doing and what you are able to do, if you don’t tell us. We also don’t bite :) So ask us if you have problems. Let us know in what you are interested and what your ideas are. The best way to get in touch is via IRC, or the mailing list, see [here](http://www.shogun-toolbox.org/page/contact/contacts), where you can find the IRC nicknames of the core-developers. Most of us live in European timezones. You are also encouraged to help out other students if you know something that they don’t. For questions about GSoC 2016 contact [Lea](https://github.com/shogun-toolbox/shogun/wiki/Lea-Goetz).

## Projects - “All those projects sound hard-core, what should I choose?”
If you cannot make up your mind, try to ask yourself what you would find most interesting and what matches your skills best. Are you more into mathematical ML or into C++ coding, do you want to implement bleeding edge algorithms or write nice examples for established ones? We are trying to offer a wide range of projects that are suitable for many backgrounds. There are even a few purely software-engineering type ones. While we are open for your own project suggestions, that is usually hard in practice since we need a mentor (who we know). Having said that, we are very open to suggestions or extensions on existing projects. In fact, if you make the description more concrete in terms of what to do exactly, or even write a prototype, this will be a big plus for your application. Speaking of application

## Your application - “How do I convince the Shogun people of myself”
As already mentioned above, you have to commit us of your excitement about Shogun and your selected project. Apart from talking to us directly, the best way to do so is to contribute to Shogun before the student application deadline. In fact, we will not consider application from people who did not send us any code. The higher quality work, the better for your application. We have a number of [issues on our github tracker](https://github.com/shogun-toolbox/shogun/issues), where we collect bugs, problems, and in particular GSoC entrance tasks. The latter are small programming tasks that are meant to be a fun introduction to Shogun while being useful for the GSoC project or Shogun in general. There are both projects related and general ones, some of which are open-ended and some of them are very concrete. If you come up with other things, that is also highly appreciated. For example, writing new notebooks, examples, or documentation is a great way to contribute, as well as fixing bugs (which is a bit harder usually). For the application itself, try to tell a nice story why you are the best candidate. We usually get around 50-100 proposals while being able to offer 5-8 slots, so be aware of competition.

##Commitment - “How much time do I really need to spend on GSoC”
GSoC is a fulltime job (40h/week)! While it is not important where you work, we expect students to hand in code every week at least, so you should work on your project continuously. We also encourage you to stick around in IRC in order to help each other, get involved with the community, and to share the fun. In addition, preparing the GSoC requires quite a bit of time and effort: preparing your application, getting involved in Shogun development before the deadline, reading about project details etc.

### Our Expectation - “What you have to deliver”
All code that you write is directly merged into our development branch because we want to avoid that you build a separate branch which nobody else sees. This means you will get feedback for every pull request you send us - lots of room for discussion!    New code might break existing unit/integration tests. This is checked via [Travis](https://travis-ci.org/shogun-toolbox/shogun) and our [buildbot farm](http://buildbot.shogun-toolbox.org/waterfall). Travis is a web-service that checks your pull request for C++ compile errors and broken unit tests before merging; after merging, our buildbot farm compiles Shogun under a large variety of configurations and operating systems, and finally runs every test. We expect you to keep our tests green. We expect you to provide unit tests for all the code you write. We also expect you to write C++ and python_modular (aka integration test) mini-examples that demonstrate the API.

In addition, a big part of every GSoC project with us is a final report in the form of an IPython notebook. Have a look at the [notebooks from last year](http://www.shogun-toolbox.org/page/documentation/notebook). You should plan the final two weeks as time to write this notebook - it is the most visible part of your project and therefore it should receive a lot of love. To help you with this, there is a peer-review from among our students at the end of GSoC: another student will review your code with respect to (interface) documentation, usability, and bugs - and you do the same with their work. In the optimal case, you write an example or notebook extension for each other. 

As we are aiming to change our license model from GPL to BSD style license, we will require all code to be submitted under this new model.

### Shogun development cycle in a nutshell - “How to get my code into Shogun”
Here is a very basic list of things how to get started hacking Shogun. It requires some basic knowledge about Git(Hub), for which you can easily find help online.

1. Register on GitHub.
2. Fork the shogun repository.
3. Clone your fork locally, add the orignal (our) repository as upstream (in order to rebase your clone). If it does not exist yet, create locally a new branch called develop. Then, rebase it against the upstream. For example using git pull --rebase upstream develop. If you did your fork recently, your develop branch will probably be already up to date with upstream develop. In any case, it is a good practice to check and synchronise your develop branch with upstream develop from time to time to receive the latest changes made by other contributors.
4. Create a new feature branch locally, work (and commit your work) in there. When done, merge this (possibly with the squash option) to your local develop branch. If you want, use [Git Flow](http://nvie.com/posts/a-successful-git-branching-model/) (search in the [archives of our mailing list](http://blog.gmane.org/gmane.comp.ai.machine-learning.shogun) for more information about how we are using Git flow).
5. Push the changes to your fork on github.
6. Send a pull request against the development branch of the original Shogun repository.
7. We hope you did not forget to write a unit test for your changes (or tell us why there is no need).
8. Every pull request will trigger travis to compile and run tests on your branch, see [travis](https://travis-ci.org/shogun-toolbox/shogun). If those are all green, someone of the core-developers will merge after giving feedback. Feedback usually takes a few iterations of you changing things and us commenting in the beginning.
9. Goto 4.

### Useful resources
 * [Develop branch](https://github.com/shogun-toolbox/shogun/tree/develop)
 * [Markdown doc files]([https://github.com/shogun-toolbox/shogun/tree/develop/doc])
 * [C++ examples (aka libshogun examples)]((https://github.com/shogun-toolbox/shogun/tree/develop/examples/undocumented/libshogun))
 * [Python modular examples](https://github.com/shogun-toolbox/shogun/tree/develop/examples/undocumented/python_modular))
 * [Unit tests](https://github.com/shogun-toolbox/shogun/tree/develop/tests/unit)
 * [Integration tests](https://github.com/shogun-toolbox/shogun/tree/develop/tests/integration)
 * [IPython notebooks](http://www.shogun-toolbox.org/page/documentation/notebook)
 * [Contacts](http://www.shogun-toolbox.org/page/contact/contacts)
 * [GitHub issues tracker](https://github.com/shogun-toolbox/shogun/issues)
 * [Shogun in Travis](https://travis-ci.org/shogun-toolbox/shogun)
 * [Buildbots](http://buildbot.shogun-toolbox.org/waterfall)
 * [Git Flow](http://nvie.com/posts/a-successful-git-branching-model/)
 * [Previous GSoC blog posts](GSoC-follow-up-blog-posts)
 * [Mailing list archives](http://blog.gmane.org/gmane.comp.ai.machine-learning.shogun)
 * [List of Shogun interfaces](http://www.shogun-toolbox.org/doc/en/latest/namespaceshogun.html)