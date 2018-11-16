# Style Guidelines: Changelog
> *A set of guidelines to changelogs.*
<br />


## Table of Contents
1. [Introduction](#introduction)
2. [Changelog](#changelog)
    - [What is a changelog?](#what-is-a-changelog)
    - [Why keep a changelog?](#why-keep-a-changelog)
4. [Guidelines](#guidelines)
5. [Roadmap](#roadmap)
6. [Example](#example)


## Introduction
This is a style guideline for changelogs that we use for projects at [cloudeight](https://github.com/cloudeight/) as part of our [style guidelines](https://github.com/cloudeight/style-guidelines) documentation project.

It is in no way perfect or the definitively correct way to write changelogs for your projects and we're always happy for insights, feedback, improvements and recommendations to help improve it!

Some projects written before this guideline may not follow it entirely or at all and there may be times when projects follow their own guidelines due to special use cases. Of course, these guidelines may be updated as and when needed.


## Changelog
### What is a changelog?
A changelog is a file which contains, in detail, all the notable changes for each release of a project, written in a chronological order.

### Why keep a changelog?
Looking at git commits and summaries for a project can sometimes be troublesome and time consuming, having a changelog helps users and contributors alike easily see the current state of a project in a much more human readable format.


## Guidelines
Although every project differs, a general guideline is to keep everything as humanly readable as possible and group changes together to easily differentiate between new and removed features for example, keeping the latest updates towards the top of the changelog. Types of changes should be categorized and grouped as follows:
1. New Features (Add)
2. Updated Features (Update)
3. Removed Features (Remove)
4. Security Fixes (Fix)
5. Bug Fixes (Fix)
6. Release Notes

Under each group, use bullet points for each item written with the imperative: "Add", "Update", "Remove" and "Fix". If an issue was resolved or closed because of an update, always link to the issue in parenthesis at the end of the bullet point for easy referencing.

Release notes can be added at the end detailing specific notes, developer messages or note-worthy additions to the update.

Note: Changelogs don't use the imperative as they are meant to be user-friendly and more human readable, rather than a list of commands like git commits.


## Roadmap
To help maintain a visual roadmap of where the project is heading and which features are to be added or removed. If possible, keep a roadmap section at the top of the changelog detailing the future project implementations. Not only does this help users and contributors understand the direction of the project, it also helps when updating the changelog as it can be moved from there to the changelog itself once it has been implemented.


## Example
```
Roadmap
--------------------------------------------------------------------------------
- Add remember me option at user login
- Update user profiles with cover photos

v1.1.1
-------------------------------------------------------------------------------
Bug Fixes
    - Fix overlay bug in legacy browsers

Release Notes
    - Overlays should now work back to IE9

v1.1.0
-------------------------------------------------------------------------------
New Features
    - Add mini bio for user profiles
    - Add online now icon to user profiles

Security Fixes
    - Fix sensitive data being stored in cookies (#1)
```


## Attributions
This changelog guideline is adapted from [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
