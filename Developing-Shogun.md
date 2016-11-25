# Shogun development cycle in a nutshell

Here is a very basic list of things how to get started hacking Shogun. First step is to compile from source, see [doc/readme/INSTALL.md](https://github.com/shogun-toolbox/docs/blob/master/INSTALL.md). And to run the [examples](https://github.com/shogun-toolbox/docs/blob/master/INTERFACES.md) and [tests](Testing) locally.

As we would like to avoid spending a lot of our time on explaining the same basic things many times
 * Please **excessively** use Google for any questions on the commands needed.
 * Please **read the manuals**, such as [GitHub guides](https://guides.github.com/).

## Steps, based on [git flow](https://guides.github.com/introduction/flow/)

0. [Read](https://guides.github.com/activities/hello-world/) [guide](https://guides.github.com/introduction/flow/)
1. Register on [GitHub](https://github.com/).
2. Fork the shogun repository.
3. Clone your fork, add the original shogun develop repository as a remote, and check out locally

        git clone https://github.com/YOUR_USERNAME/shogun
        cd shogun
        git remote add upstream https://github.com/shogun-toolbox/shogun
        git branch develop
        git checkout develop
        git pull --rebase upstream develop

4. Create a feature branch (from develop)

        git branch feature/BRANCH_NAME

5. Your code here: Fix bug or add feature.
6. Make sure (!) it compiles, it is [tested](Testing), it complies to the [code style](Code-style).

        make && make test

7. Commit locally, using neat and informative commit messages, grouping commits, potentially iterate over more changes to the code. The [amend option](https://help.github.com/articles/changing-a-commit-message/) is your friend if you are updating single commits

        git commit FILENAME(S) -m "Fix issue #1234"
        git commit FILENAME(S) -m "Add feature XYZ"

8. [Rebase](https://git-scm.com/book/en/v2/Git-Branching-Rebasing) against shogun's develop branch. This might cause rebase errors, which you need to [solve](https://help.github.com/articles/resolving-merge-conflicts-after-a-git-rebase/)

        git pull --rebase upstream develop
        
9. Push your commits to your fork

        git push origin feature/BRANCH_NAME

10. Send a pull request (PR) via GitHub

## Requirements for merging your PR
 * All tests pass (your pull request causes automatic checks)
 * The PR is small.
 * The PR is clean and addresses *one* issue.
 * If C++ code: it is covered by tests, it doesn't leak memory, its API is documented.
 * If example/docs: it looks polished, English language is correct.