# Style Guidelines: Git
> *A set of guidelines to git.*
<br />


## Table of Contents
1. [Best Practices](#best-practices)
    - [Concise Commits](#concise-commits)
    - [Commit Often](#commit-often)
    - [Use Branches](#use-branches)
2. [Git Commit Fields](#git-commit-fields)
    - [Summary](#summary)
    - [Description](#description)
3. [Example](#example)


## Best Practices
### Concise Commits
If you have trouble summarizing what a commit does, this may be because there are several changes that can't be explained in one commit summary. It is always better to split them into separate commits as small commits make the development process easier to understand and easier for developers to roll back changes if something goes wrong.

### Commit Often
As mentioned above, regular commits help reduce the issue of being able to summarize what your commit does. Not only does this help relieve this problem it also helps get your code into the hands of other developers and contributors to the project, causing less merge conflicts and a much more concise, rapid workflow for everyone.

### Use Branches
Always use branches when introducing backwards compatibility issues to older versions or if a large number of features are being implemented or removed from the project. This helps maintain an easier workflow and allows the "commit often" ideology to continue working.


## Git Commit Fields
### Summary
A summary line is required for each commit made to a git repository, they should:

 - Use no more than 50 characters
 - Start the line with either
	 - Add
	 - Update
	 - Remove
	 - Fix
 - Never end the line with a period

### Description
Descriptions may not always be necessary if the summary itself covers the changes made with the commit summary, they should:

- Start the line with the summary as the subject
- Use bullet points treated as the body to detail each each
- Have an empty line between the subject and body

### Ordering
Always stick to the order:

- Add
- Update
- Remove
- Fix

There are 3 different levels of fixes, these should be listed using the Fix imperative in this order:

- Security fixes
- Bug fixes
- General fixes like typos, wording or declaration orders


## Example
```
Summary
--------------------------------------------------------------------------------
Update README.md

Description
--------------------------------------------------------------------------------
Update README.md

- Add project description
- Add install instructions
- Update credits and attributions
- Fix typo
```
