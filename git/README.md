# Style Guidelines: Git

*An undoubtedly debatable guideline to git...*

## Table of Contents

1. [Introduction](#introduction)
2. [Best Practices](#best-practices)
    - [Concise Commits](#concise-commits)
    - [Commit Often](#commit-often)
    - [Use Branches](#use-branches)
3. [Git Commit Fields](#git-commit-fields)
    - [Summary](#summary)
    - [Description](#description)

## Introduction

This is a style guideline for documenting a git commit summary and description that we use for projects at [cloudeight](https://github.com/cloudeight/) as part of our [style guidelines](https://github.com/cloudeight/style-guidelines) documentation project.

It is in no way perfect or the definitively correct way to document your projects git commit summary and description and we're always happy for insights, feedback, improvements and recommendations to help improve it!

Some projects written before this guideline may not follow it entirely or at all and there may be times when projects follow their own guidelines due to special use cases. Of course, these guidelines may be updated as and when needed.

## Best Practices

### Concise Commits

If you have trouble summarizing what a commit does, this may be because there are several changes that can't be explained in one commit summary. It is always better to split them into separate commits as small commits make the development process easier to understand and easier for developers to roll back changes if something goes wrong.

### Commit Often

Regular commits help reduce the issue of being able to summarize what your commit does, as mentioned above. Not only does this help relieve this problem it also helps get your code into the hands of other developers and contributors to the project, causing less merge conflicts and a much more concise, rapid workflow for everyone.

### Use Branches

Always use branches when introducing backwards compatibility issues to older versions or if a large number of features are being implemented or removed from the project. This helps maintain an easier workflow and allows the "commit often" ideology to continue working.


## Git Commit Fields

### Summary

A summary line is required for each commit made to a git repository and should follow these simple rules:

 - Be no more than 50 characters long.
 - Start the line with Add, Update, Remove or Fix.
 - Don't end the line with a period.

### Description

The description should follow the [changelog guidelines](../version-control#guidelines) except use the imperative: "Add", "Update", "Remove" and "Fix". This helps maintain consistency with generated commit messages from commands such as "git merge".
