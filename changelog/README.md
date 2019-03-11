# Style Guidelines: Changelog
> *A set of guidelines to changelogs.*
<br />


## Table of Contents
1. [Changelog](#changelog)
    - [What is a changelog?](#what-is-a-changelog)
    - [Why keep a changelog?](#why-keep-a-changelog)
2. [Guidelines](#guidelines)
3. [Roadmap](#roadmap)
4. [Example](#example)


## Changelog
### What is a changelog?
A changelog is a file which contains, in detail, all the notable changes for each release of a project, written in a chronological order.

### Why keep a changelog?
Looking at git commits and summaries for a project can sometimes be troublesome and time consuming, having a changelog helps users and contributors alike easily see the current state of a project in a much more human readable format.


## Guidelines
Although every project differs, a general guideline is to keep everything as humanly readable as possible and group changes together to easily differentiate between new and removed features for example, keeping the latest updates towards the top of the changelog. Types of changes should be categorized and grouped as follows:

1. New
2. Updated
3. Removed
4. Security Fixes
5. Bug Fixes
6. Fixed
7. Release Notes

Under each group, use bullet points for each item using: "Added", "Updated", "Removed" and "Fixed", in a similar fashion to the [Git](https://github.com/joemottershaw/style-guidelines/tree/master/git) guidelines but with the non-imperative. If an issue was resolved or closed because of a commit, always link to the issue in parenthesis at the end of the bullet point for easy referencing.

Release notes can be added at the end detailing specific note-worthy additions or developer messages.


## Roadmap
To help maintain a visual roadmap of where the project is heading and which features are to be added or removed. If possible, keep a roadmap section at the top of the changelog detailing the future project implementations. Not only does this help users and contributors understand the direction of the project, it also helps when updating the changelog as it can be moved from there to the changelog itself once it has been implemented.


## Example
```markdown
# Roadmap

### New
- Added remember me option at user login

### Update
- Updated user profiles with cover photos


-----


# v1.1.1

### Bug Fixes
- Fixed overlay bug in legacy browsers

### Release Notes
- Overlays should now work back to IE9


-----


# v1.1.0

### New
- Added mini bio for user profiles
- Added online now icon to user profiles

### Security Fixes
- Fixed sensitive data being stored in cookies (#1)


-----

# v1.0.0

### Initial Release
```


## Attributions
This changelog guideline is adapted from [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
