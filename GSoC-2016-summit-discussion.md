Viktor and Heiko had some really good discussions on the GSoC 2016 mentor summit, as a result of spending a week of hacking Shogun before the summit. See photo of notes on bottom.

##Hacking
 * Updated the website, and automated its deployment
 * Automated the release process
 * Automate nightly binaries for ubuntu
 * Extended integration testing across all interfaces
 * fixed tons of bugs
 * ...

##Next steps
This is a suggestion for a set of releases, roughly ordered in priority, with big blobs (that require a major release) grouped together. There is a parallel stream of smaller fixes below, along with a set of more vague goals for the more distant future.

###5.0
 * This release was prepared at the summit

###5.1
 * Bugfix release for 5.0
 * [milestone](https://github.com/shogun-toolbox/shogun/milestone/10)
 * Mostly about fixing problems we wanted to fix at the summit, but did not find time.
 * All relatively high priority and should be done before moving on, at least partly
 * Add scala in examples (re-uses java)

#6.0
 * [milestone](https://github.com/shogun-toolbox/shogun/milestone/11)
 * Integrate tags GSoC 2016 project (requires a `SG_ADD` hack)
 * Integreate cereal GSoC 2016 project (requires tags)
 * Based on new cerealisation, make a hash based equals method
 * remove existing parameter framework
 * c++11 hard requirement
 * integrate linalg GSoC 2016 project

#7.0
 * Constrained parameters
 * Every parameter gets a range of valid values it can take, potentially a domain
 * ...

#8.0 (maybe can be merged with previous)
 * shared pointer shogun wide
 * base interface for ML (abstract classes, restructure shoguns API, depends on constrained parameters)
 * split SWIG/cmake/tests, modularise library, ship separate binaries

#Other changes, independent of release, in increasing priority
 * integration of interfaces into target language system (e.g. maven for java)
 * BSD license change
 * get rid of jblas and ndarray and replace with more modern libraries
 * New typemaps and examples for js, Matlab, D

# Important things for moving the project forward
 * Build a pipeline for supervised prediction, fix things on the fly
 * Pull out the interfaces from the Shogun repo (and examples, testing, build)
 * Establish affiliation (numfocus or other) for funding, give up on own eV

# Distance future dreams
 * graph based representation of computation, use something as tensorflow as backend, just like linalg
 * Standard ML API with Shogun as reference implementation
 * OpenML
 

# Photo of notes
[[https://github.com/shogun-toolbox/shogun-wiki/blob/master/img/gsoc_2016_mentor_summit_shogun_future.JPG|alt=mentor_summit_notes]]
