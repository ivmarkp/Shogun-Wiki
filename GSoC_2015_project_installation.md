# Easy installation on major platforms
**This is among the MOST IMPORTANT projects for GSoC**. It does not involve any Machine Learning but is a good way for hackers to get involved in Shogun. We might take 2 students with different OS skills here.
See also the [windows](GSoC_2015_windows) project.

### Mentors
 * [Sergey](Sergey%20Lisitsyn) (github: [lisitsyn](https://github.com/lisitsyn), IRC: lisitsyn)
 * [Viktor](Viktor%20Gal) (github: [vigsterkr](https://github.com/vigsterkr), IRC wiking)
 * [Bjoern](Bjoern%20Esser) (github: [besser82](https://github.com/besser82), IRC besser)
 * [Heiko](Heiko%20Strathmann) (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)

### Difficulty & Requirements

Rather easy but massive and needs scrutinizing some questions.
It suits you best if you:

* Are not afraid of Mac OS X, Linux and Windows
* Know essentials of building tools like CMake and Makefile
* Are ok with patching some C++ code
* Feel like real devops guy or a [duct tape programmer](http://www.joelonsoftware.com/items/2009/09/23.html)

### Description

We have to admit that Shogun is not really user-friendly to install. Users are going through some troubles even on quite major platforms which we should support better. We want to solve that. This project is the first step towards more smooth user experience that starts from the installation of Shogun on your favourite platform. The main goal of this project is to let users install Shogun on all major platforms in just a few clicks. And these should be documented (replacing all outdated documentation).

### Details

This project is a massive initiative to finally make Shogun really easy to try on all major platforms. First of all, we want to have an infrastructure to have a daily build of Shogun for Debian based platforms, and easy to integrate packages for debian. Next, we aim to cover .rpm packages which would make it easy to use Shogun on distributions like Fedora and RHEL. Next, we expect to see an easy way to install Shogun on Mac OS X using Homebrew or Macports. Finally (and more involved than the previous parts), a native build and installation on Windows (possibly in [another project](GSoC_2015_windows))

All of these commands are expected to work on any popular platform Linux/Max/Win machine:
 * ```apt-get install shogun```
 * ```yum install shogun```
 * ```brew install shogun```
 * ```port install shogun```
 * ```shogun_installer.exe```

In addition, we want the Python bindings to be installable as:
 * ```pip install shogun```
 * ```conda install shogun```

### Waypoints and initial work
See above. Initial work would be to start prototyping a solution for one of the above systems. Pick any.

#### Related entrance issues:
 * [#2720](https://github.com/shogun-toolbox/shogun/issues/2720).

### Optional
The possible optional part of the project is to provide a series of videos or blog posts that show how easy one can install Shogun with all the work carried out during the project.

### Why this is cool
By the end of this project we expect Shogun to be easy to install on any major platform and this would be really helpful for the whole project and its popularity. Again ***TOP PRIORITY***

### Useful resources
* [CMake documentation](http://www.cmake.org/documentation/)
* [Windows installer](https://msdn.microsoft.com/en-us/library/cc185688(v=vs.85).aspx)
* [Homebrew](http://brew.sh/)
* [Macports](https://www.macports.org/)