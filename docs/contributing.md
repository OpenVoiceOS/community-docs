# Contributing

## I'm non-technical, how do I contribute?

If you're non-technical, there are still many ways to contribute.

* You can give us **feedback** on this documentation, using [github](https://github.com/OpenVoiceOS/community-docs)
* You can join our community through our [Chat](https://matrix.to/#/!XFpdtmgyCoPDxOMPpH:matrix.org?via=matrix.org)
* You can contribute your **voice** to the [Community Wake Word Dataset](https://github.com/OpenVoiceOS/ovos-ww-community-dataset)

## I'm technically minded, how do I contribute?

Great! Let's get you started.

### Reporting Issues

* You'll need a [GitHub account](https://github.com/signup/free)
* Check our [Issues](https://github.com/issues?user=OpenVoiceOS) first to see if the Issue has already been reported.

If not, you'll need to create a new Issue. Help us to help fix the Issue quicker by following these guidelines. Your Issue should contain:

#### A description of the Issue in object-deviation format

Object-deviation format is a very specific way of describing faults. The more specific you can be, the easier it is for us to fix the fault. Begin with the _object_, such as function, a skill, or a hardware feature, then explain the _deviation from the expected condition_.

For example:

* "When my Mycroft Mark 1 device \(**object**\) powers on, the color of his eyes is red instead of blue \(**deviation - red - from expected condition - blue**\)
* "When I ask about the weather \(**object**\), Mycroft reports the low temperature correctly, but the high temperature is incorrectly reported as the low temperature \(**deviation - incorrect temperature - from expected condition - correct temperature**

### Making changes

1. [Fork the Project](https://help.github.com/articles/fork-a-repo/)
2. [Create a new Issue](https://help.github.com/articles/creating-an-issue/) if one doesn't already exist.
3. Create a **feature** or **bugfix** branch based on **dev** with your issue identifier. For example, if your issue identifier is: **issue-123** then you will create either: **feature/issue-123** or **bugfix/issue-123**. Use **feature** prefix for issues related to new functionalities or enhancements and **bugfix** in case of bugs found on the **dev** branch
4. Make sure you stick to the coding style and OO patterns that are used already.
5. Document code using [Google-style docstrings](http://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html).  All functions and class methods that are expected to be called externally should include a docstring.  \(And those that aren't [should be prefixed with a single underscore](https://docs.python.org/2/tutorial/classes.html#private-variables-and-class-local-references)\).
6. Make commits in logical units and describe them properly. Use your issue identifier at the very begin of each commit. For instance:

   `git commit -m "Issues-123 - Fixing 'A' sound on Spelling Skill"`

7. Once you have committed everything and are done with your branch, you have to rebase your code with **dev**. Do the following steps: 1. Make sure you do not have any changes left on your branch 2. Checkout on dev branch and make sure it is up-to-date 3. Checkout your branch and rebase it with dev 4. Resolve any conflicts you have 5. You will have to force your push since the historical base has changed 6. Suggested steps are:

   ```text
      git checkout dev
      git fetch
      git reset --hard origin/dev
      git checkout <your_branch_name>
      git rebase dev
      git push -f
   ```

8. Once everything is OK, you can finally [create a Pull Request \(PR\) on Github](https://help.github.com/articles/using-pull-requests/) in order to be reviewed and merged.

**Note**: Even if you have write access to the master branch, do not work directly on master!

## Submitting changes for review

* Push your changes to a topic branch in your fork of the repository.
* Open a pull request to the original repository and choose the right original branch you want to patch.
* If not done in commit messages \(which you really should do\) please reference and update your issue with the code changes. But _please do not close the issue yourself_.
* Even if you have write access to the repository, do not directly push or merge pull-requests. Let another team member review your pull request and approve.

## Additional Resources

* [General GitHub documentation](https://help.github.com/)
* [GitHub pull request documentation](https://help.github.com/articles/about-pull-requests/)
* [Read the Issue Guidelines by @necolas](https://github.com/necolas/issue-guidelines/blob/master/CONTRIBUTING.md) for more details

