fwdup
=====

This is super-duper experimental, use at your own risk. It is fun, though.

Here's what it looks like:

```
$ export PATH="$PWD/bin:$PATH"

$ fwdup
Usage: /Users/shazow/projects/fwdup/bin/fwdup COMMAND

Where COMMAND is one of:
  add
  create
  enter
  manifest
  purge

$ fwdup create mybackup
Initialized empty Git repository in /Users/shazow/projects/fwdup/mybackup/

$ export GIT_DIR=$PWD/mybackup  # TODO: Use `fwdup-enter` instead somehow.

$ cd ~

$ fwdup add .vimrc
[master 3c8f005] Importing: .vimrc
 6 files changed, 11 insertions(+), 10 deletions(-)
 create mode 100644 .vimrc

$ fwdup manifest
.vimrc
```
