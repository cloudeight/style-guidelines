# Style Guidelines: Version Control

*An undoubtedly debatable guideline to version control...*

## Table of Contents

1. [Introduction](#introduction)
2. [Semantic Versioning](#semantic-versioning)
    - [What is semantic versioning?](#what-is-semantic-versioning)
    - [Rules](#rules)
    - [Version Components](#version-components)
        - [Patch](#patch)
        - [Minor](#minor)
        - [Major](#major)
    - [Exceptions](#exceptions)
4. [Development](#development)
    - [Where to start?](#where-to-start)
    - [Alpha Build](#alpha-build)
    - [Beta Build](#beta-build)
    - [Stable Release](#stable-release)

## Introduction

This is a style guideline for version control that we use for projects at [cloudeight](https://github.com/cloudeight/) as part of our [style guidelines](https://github.com/cloudeight/style-guidelines) documentation project.

It is in no way perfect or the definitively correct way to version control your projects and we're always happy for insights, feedback, improvements and recommendations to help build on it!

Some projects written before this guideline may not follow it entirely or at all and there may be times when projects follow their own guidelines due to special use cases. Of course, these guidelines may be updated as and when needed.

## Semantic Versioning

### What is semantic versioning?

Semantic Versioning (SemVer) is a 3 component version control system, it uses an `x.y.z` format, where:

 - **x**: Major Version
 - **y**: Minor Version
 - **z**: Patch

This gives us a version number control of `major.minor.patch`.

SemVer works by incrementing the correct component depending on the update. This makes it easy to determine which type of version you should be incrementing for each release.

### Rules

 1. Version numbers should never contain negative numbers or contain leading zeroes.
 2. Each version component must increase numerically by a value of 1.
 3. When a version component of higher precedence is increased the other components return to 0.
     - Major version update: Minor and Patch return to 0.
     - Minor version update: Patch returns to 0.
 4. Pre release builds must suffixed with the corresponding `-alpha` or `-beta` identifier.
 5. Version `1.0.0` is considered the stable release with a public API and documentation.

### Version Components

##### Patch

If an update contains a bug fix, security update or something along the lines of a typo correction or better, more coherent commenting within the code, this would be considered a patch as no new features or code breaking changes have been implemented. This means the `z` patch component would increase in the version number.

##### Minor
If an update contains a new feature that is backwards compatible with the current API, this would be considered a minor release as there are no code breaking changes. This means the `y` minor version component would increase in the version number.

##### Major

If an update contains changes that are likely to break the current API as there are backwards compatibility issues, this would be considered a major release. This will inform users that they will need to update their own projects' code to accommodate for the new version. This means the `x` major version component would increase in the version number.

### Exceptions

 1. Alpha builds do not increase any of the 3 version components but have their own incremental build number.
 2. Beta builds do not increase the major version component, only the minor and patch version components.

## Development

### Where to start?

All projects start with a version number of `0.1.0`, not `1.0.0` or `0.0.1`. This is because, no project starts with a patch or stable release, it starts with a set of features, hence the minor version component being the first component to contain a value.

### Alpha Build

During the initial stages of the project development process, a project starts out as an alpha build and is updated heavily and usually very rapidly. This build shouldn't be publicly available on dependency package managers such as [npm](https://www.npmjs.com/), [yarn](https://yarnpkg.com/) or [composer](https://getcomposer.org/) etc and will only be available via a GitHub repository, usually private, but sometimes public.

All alpha builds should always contain the hyphen alpha suffix and start like so: `0.1.0-alpha`

Since there will be many code breaking changes and backwards compatibility issues with almost every update, the 3 version components are not changed, instead, the alpha suffix contains an alpha build number which is increased with each release, like so:

`0.1.0-alpha.9` -> `0.1.0-alpha.10` -> `0.1.0-alpha.11`

These build numbers should follow the same rules as the version components outlined [above](#rules).

### Beta Build

The beta phase begins when the project is feature complete but likely to contain a number of known bugs that need to be fixed.

Beta builds ***can*** be publicly available on dependency package managers such as [npm](https://www.npmjs.com/), [yarn](https://yarnpkg.com/) or [composer](https://getcomposer.org/) etc if required, but will usually just be available via a GitHub repository, usually public, but sometimes private.

All beta builds should always contain the hyphen beta suffix and start like so: `0.1.0-beta`

During this stage of the development process, the project is still updated heavily and rapidly but unlike alpha builds the minor and patch version components are now increased and the alpha build number is dropped, like so:

`0.1.9-beta` -> `0.1.10-beta` -> `0.1.11-beta` -> `0.2.0-beta` -> `0.2.1-beta`

However, even with code breaking changes or backwards compatibility issues in an update, the major version component must **never** be increased in a beta build as this signals the start of a stable release. This is because although minor versions may contain code breaking changes and cause backwards compatibility issues, this is expected in a beta build.

### Stable Release

A project is available as a stable release once all known bugs and security issues have been addressed and substantial documentation has been written and publicly available.

Alpha and beta suffixes and build numbers are now removed from the version number and the version number is bumped to `1.0.0`.

Stable releases can now be publicly available on dependency package managers such as [npm](https://www.npmjs.com/), [yarn](https://yarnpkg.com/) or [composer](https://getcomposer.org/) etc if required and version numbering should follow the [rules](#rules) listed above.
