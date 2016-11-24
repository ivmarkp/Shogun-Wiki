# Shogun development cycle in a nutshell - “How to get my code into Shogun”

Here is a very basic list of things how to get started hacking Shogun. While this might seem overwhelming at first, it is pretty standard.

As we would like to avoid spending a lot of our time on explaining the same basic things many times
 * Please *excessively* use Google for any questions on the tools needed
 * Please *read* [guides](https://guides.github.com/) for collaborative open source development

We use the [git flow] model

## Steps:

1. Register on GitHub.
2. Fork the shogun repository.
3. Clone your fork, add the original shogun repository as a remote.
4. Create a feature branch
5. Your code here: Fix bug or add feature. 
6. Make sure (!) it is [tested](Testing) and complying to the [code style](Code-style).
7. Commit locally, using clean and informative commit messages, potentially goto 5
8. Push your commits to your fork
9. Send a pull request