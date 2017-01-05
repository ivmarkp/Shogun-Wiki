# Getting involved
Welcome to our FAQ on how to get involved with Shogun and Google Summer of Code. While this FAQ is mostly written for GSoC students, it also contains lots of useful tips for getting involved in general. If you can't find what you're looking for, contact us. 

## First steps - “Shogun seems huge (and messy), where do I start?”
Shogun **is** huge and messy. Half of the fun is that nobody really understands all parts of it. But don't be intimidated, the basics are very simple ;)

First step, install it, see [INSTALL.md](https://github.com/shogun-toolbox/docs/blob/master/INSTALL.md). If you have trouble, search the web. If you still have trouble, ask us. If you think that your issue might be worth being documented, we greatly appreciate if you then would update the corresponding README (this is what open-source is about).

After an installation, try running the [examples](http://shogun-toolbox.org/examples) locally. You can also try to run the tests. Check the [readmes](https://github.com/shogun-toolbox/docs/blob/master/) for that. Once everything is set up and working, have a look at our [showroom](http://shogun-toolbox.org/showroom), and maybe try to run things locally. Pick an example of your choice and play with it. You could for example modify the data that is used, or plug in another algorithm. If you find a bug or problem, tell us about it!

###Your first patch
... is **small and simple**: pick an [entrance task](https://github.com/shogun-toolbox/shogun/issues?q=is%3Aopen+is%3Aissue+label%3Aentrance) you like and submit a small patch that solves it. Do something very simple, like fixing a typo in the docs or [add/port an example](https://github.com/shogun-toolbox/shogun/issues/3555).
We've compiled a list of [**example patches**](GSoC-2016-example-patches) to give you a better idea of what we're looking for.
Before sending a patch, check the [DEVELOPING.md](https://github.com/shogun-toolbox/docs/blob/master/DEVELOPING.md) readme.

Generally, we won't assign you an issue to solve because we think that you should be solving the one you're most interested in. It's worth having a look at the mailing list archives, to see whether other people might already be working on this. Of course, if you have a technical question about a particular issue you can talk to the people who submitted it. 

And that's it - you've made a start :)

## Google Summer of Code & What we are looking for
If you are here to join us in GSoC, please have a look at our [past projects](GSoC-follow-up-blog-posts) and our [GSoC 2016 projects](Google%20Summer%20of%20Code%202016%20Projects) to get a good feeling for GSoC with Shogun means.
We have successfully participated in a number of GSoC. Your help is extremely welcome. Therefore if...

 * you are interested in Machine Learning (ML), Statistics, Optimization, framework design, or just C++ coding
 * you enjoy working with a vibrant team of experienced ML scientists and software engineers
 * you always wanted to join open-source 

then GSoC with Shogun is for you! You'll spend the summer working with our enthusiastic and open-minded team of developers who are creating one of the largest ML toolboxes out there.

GSoC is a great program and every year we have lots of fun.

## Female contributors
Without few exceptions, most Shogun developers are male. We would like to change this - to create a nicer atmosphere and to [work more effectively](http://www.nytimes.com/2015/01/18/opinion/sunday/why-some-teams-are-smarter-than-others.html?_r=0). In order to achieve a more balanced gender distribution (in GSoC and general), **we are in particular looking for female contributors to join us**.

## Applicability - “Am I good enough to do this?”
You are the right person!! The main skill that we are looking for is motivation - we greatly appreciate people who take initiative, come up with creative ideas and are self-organised in making them happen (with our guidance of course). Since Shogun is about ML, most projects are technically involved in some sense: probability distributions, linear algebra, optimization, as well as object-oriented programming, compilers, and git should be things that do not scare you (not too much at least ;) ). However, we do not require you to be a master in the topics that the projects are about, our community is also about enjoying to learn and all of us started from zero.

## Communication - “I don’t want to bother the Shogun developers with my stupid question”
Wrong! Communication is among the most important things in GSoC and in open-source in general. We will not find out what you are doing and what you are able to do, if you don’t tell us. We also don’t bite :) So ask us if you have problems, and **after** having asked Google.
Let us know in what you are interested and what your ideas are. The best way to get in touch is via IRC, or the mailing list. Ask any of the present [authors](AUTHORS). Most of us live in European timezones. You are also encouraged to help out other students if you know something that they don’t.

## GSoC Projects - “All those projects sound hard-core, what should I choose?”
If you cannot make up your mind, try to ask yourself what you would find most interesting and what matches your skills best. Are you more into mathematical ML or into C++ coding, do you want to implement bleeding edge algorithms or write nice examples for established ones? We are trying to offer a wide range of projects that are suitable for many backgrounds. There are even a few purely software-engineering type ones. While we are open for your own project suggestions, that is usually hard in practice since we need a mentor (who we know). Having said that, we are very open to suggestions or extensions on existing projects. In fact, if you make the description more concrete in terms of what to do exactly, or even write a prototype, this will be a big plus for your application. Speaking of application

## GSoC applications - “How do I convince the Shogun people of myself”
As already mentioned above, you have to commit us of your excitement about Shogun and your selected project. Apart from talking to us directly, the best way to do so is to contribute to Shogun before the student application deadline. In fact, we will not consider application from people who did not send us any code. The higher quality work, the better for your application. We have a number of [issues on our github tracker](https://github.com/shogun-toolbox/shogun/issues), where we collect bugs, problems, and in particular GSoC entrance tasks. The latter are small programming tasks that are meant to be a fun introduction to Shogun while being useful for the GSoC project or Shogun in general. There are both projects related and general ones, some of which are open-ended and some of them are very concrete. If you come up with other things, that is also highly appreciated. For example, writing new notebooks, examples, or documentation is a great way to contribute, as well as fixing bugs (which is a bit harder usually). For the application itself, try to tell a nice story why you are the best candidate. We usually get around 50-100 proposals while being able to offer 5-8 slots, so be aware of competition.

##Commitment - “How much time do I really need to spend on GSoC”
GSoC is a fulltime job (40h/week)! While it is not important where you work, we expect students to hand in code every week at least, so you should work on your project continuously. We also encourage you to stick around in IRC in order to help each other, get involved with the community, and to share the fun. In addition, preparing the GSoC requires quite a bit of time and effort: preparing your application, getting involved in Shogun development before the deadline, reading about project details etc.

### Our Expectation - “What you have to deliver”
All code that you write is directly merged into our development branch because we want to avoid that you build a separate branch which nobody else sees. This means you will get feedback for every pull request you send us - lots of room for discussion!    New code might break existing [tests](https://github.com/shogun-toolbox/docs/blob/master/DEVELOPING.md#testing). We expect you to keep our tests green. We expect you to provide unit tests for all the code you write. We also expect you to write [API examples](http://shogun-toolbox.org/examples) for the website.

In addition, a big part of every GSoC project with us is a final report in the form of a [notebook](http://shogun-toolbox.org/showroom), or a [blog post](GSoC-follow-up-blog-posts). You should plan the final two weeks as time to write this - it is the most visible part of your project and therefore it should receive a lot of love. To help you with this, there is a peer-review from among our students at the end of GSoC: another student will review your code with respect to (interface) documentation, usability, and bugs - and you do the same with their work. In the optimal case, you write an example or notebook extension for each other. 

As we are aiming to change our license model from GPL to BSD style license, we will require all code to be submitted under this new model.
