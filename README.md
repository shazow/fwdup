# **fwdup**: like back-ups, but forward

**This is super-duper experimental and incomplete, use at your own risk.**

You know what would be fun? If we set `GIT_WORK_TREE` to `$HOME` (or root, if you dare), sprinkled some `/*` into our `info/exclude`, and used Git as a whitelist-based backup system.

This works surprisingly well for small rarely-changing files like settings and configurations.

I hacked this up together in about an hour and only used it once for anything significant, so it's still quite lacking. I hope to continue fleshing it out with some ideas below.

## Overview

Here's what it looks like right now:

```
$ # Add the scripts to your PATH
$ export PATH="$PWD/bin:$PATH"
$ fwdup
Usage: /Users/shazow/projects/fwdup/bin/fwdup COMMAND

Where COMMAND is one of:
  add
  create
  enter
  manifest
  purge

$ # Create a backup storage (aka a git repo with a detached working tree)
$ fwdup create mybackup
Initialized empty Git repository in /Users/shazow/projects/fwdup/mybackup/

$ # Start choosing things to back up
$ # FIXME: Use `fwdup-enter` instead somehow. Right now it's exceptionally sad.
$ export GIT_DIR=$PWD/mybackup
$ cd ~
$ fwdup add .vimrc
[master 3c8f005] Importing: .vimrc
 6 files changed, 11 insertions(+), 10 deletions(-)
 create mode 100644 .vimrc
$ fwdup manifest
.vimrc

$ # Now we can push to some remote that we have a bare git repo on, and it's backed up.
$ # FIXME: Need to add a fwdup command for this too. Also one for restoring.
```


## Ideas for the future

- A better frontend for this, of course.
- More documentation for a complete story, including creating a backup, replicating it, restoring from a remote, setting up a cron, etc.
- A database of common config files people want to back up that live in strange places, namely various applications.
- Some kind of plugin for backing up installed-applications state and restoring it accordingly. For example, with homebrew, I manually maintain `brew list > brew.manifest` which I `cat brew.manifest | xargs brew install` when I need to restore. Would be swell if there was a plugin that detected homebrew and did these kinds of things for me.
- Some kind of integration with `git-annex` for larger files?
