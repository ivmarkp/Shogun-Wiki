# How to release a new version of shogun

In order to create a new release of shogun, you just need to run the following commands, the rest will be taken care of the [release pipeline](http://buildbot.shogun-toolbox.org/builders/release).

First choose the new release version of the library. for this howto let's say we want to release `5.1.0`.

First of all checkout the `develop` branch of shogun and pull the latest from that branch:
```
git checkout develop
git fetch --tags
git pull
git submodule update
```

Make sure that the [NEWS](https://github.com/shogun-toolbox/shogun/blob/develop/NEWS) file contains a new section for the target release, where the first line in the change log should contain the version of shogun, e.g.
```
   * SHOGUN Release version 5.1.0 (libshogun 17.2, data 0.11, parameter 1)
```
please make sure that the major changes are reflected in the section for the new release.

Once it's done and committed to the `develop` branch run the following commits to create a release branch and then merge it into master, that will trigger the release pipeline:
```
git clean -dfx
git flow release start 5.1.0
git flow release finish -s 5.1.0
#(in case of merge conflicts fix them and do git commit -a ; git flow release finish -s 5.1.0 )
git push
git push --tags
```