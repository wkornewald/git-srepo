[![Build Status](https://travis-ci.org/allbuttonspressed/git-srepo.svg?branch=master)](https://travis-ci.org/allbuttonspressed/git-srepo)

# git-srepo
Import other repositories into your git repository.
This is a simpler alternative to git subtree, submodule, stree, and subrepo.

Commits to an imported repo are kept within your project repo until you push
them to the imported repo.
Local changes are maintained as a clean, rebased set of patches for upstream
contribution.

## Installation
Just add the git-srepo script to your PATH.

Supported platforms: Linux, OS X, and Windows.

## Examples
Import d3 repository into lib/d3 folder::

  git srepo import lib/d3 https://github.com/mbostock/d3

Pull new changes::

  git srepo pull lib/d3

Push your changes::

  git srepo push lib/d3

Push your changes to custom repo::

  git srepo push lib/d3 https://github.com/myaccount/d3 master

Export a folder into a separate repo::

  git srepo export src/mylib https://github.com/myaccount/mylib master

List imported repositories::

  git srepo list

## More details
This extension maintains a linear, rebased set of your local changes, so there
won't be any merge commits, etc.
This is important because most projects won't accept your patches unless
they're clean.

All state (including the rebased set of patches!) is committed to your
repository. This means anyone can pull new changes and contribute your team's
changes back upstream.

Also, this extension does all its pull/push magic in a separate clone (in
.git/.subrepo).
This is important because you'll most likely have existing software (an IDE,
a build script, etc.) monitoring your repository for changes. It would be
really annoying if your IDE closed all your files during a pull.

## Why?
None of the other solutions allows maintaining your changes in a way that
allows easy upstream contribution through a linear, rebased set of patches.
This is the main problem I want to solve.

Additionally, the other solutions have these issues:

With git subtree your history gets polluted. See here for more details:
https://medium.com/@porteneuve/mastering-git-subtrees-943d29a798ec

With git submodule you have to be aware of imported repos and run extra
commands and create forks for your project-specific commits. This makes
using your project unnecessarily complicated. See here for more reasons:
http://blogs.atlassian.com/2013/05/alternatives-to-git-submodule-git-subtree/

With git stree, the subtree's settings are kept local to your repo, so you're
the only one who can pull new changes and you better do some backups in case
your disk dies.

With git subrepo, pulls can lose your local changes. This bug might also exist
in git stree. Also, with git subrepo, the subrepo gets checked out within your
project repository on every subrepo pull. This breaks your IDE and any build
scripts watching your repo, as described above.

## Contributing
Contributions are always welcome. Just create a fork of this repo and send a
pull request. Thank you. :)
