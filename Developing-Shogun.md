# Shogun development cycle in a nutshell

Here is a very basic list of things how to get started hacking Shogun. First step is to compile from source, see [doc/readme/INSTALL.md](https://github.com/shogun-toolbox/docs/blob/master/INSTALL.md). And to run the [examples](https://github.com/shogun-toolbox/docs/blob/master/INTERFACES.md) and [tests](Testing) locally.

As we would like to avoid spending a lot of our time on explaining the same basic things many times
 * Please *excessively* use Google for any questions on the tools needed
 * Please *read* [guides](https://guides.github.com/) for collaborative open source development

## Steps, based on [git flow](https://guides.github.com/introduction/flow/)

1. Register on GitHub.
2. Fork the shogun repository.
3. Clone your fork, add the original shogun develop repository as a remote.
4. Create a feature branch.
5. Your code here: Fix bug or add feature. 
6. Make sure (!) it is [tested](Testing) and complying to the [code style](Code-style).
7. Commit locally, using neat and informative commit messages, grouping commits, potentially goto 5
8. [Rebase](https://git-scm.com/book/en/v2/Git-Branching-Rebasing) against shogun's develop branch
9. Push your commits to your fork
10. Send a pull request (PR)

## Requirements for merging your PR
 * All tests pass (your pull request causes travis to check all interfaces)
 * The PR is small.
 * The PR is clean and addresses *one* issue.
 * If C++ code: it is covered by tests, it doesn't leak memory, its API is documented.
 * If example/docs: it looks polished, English language is correct.