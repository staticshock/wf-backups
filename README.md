You can keep daily Workflowy backups in a git repo, I guess
===========================================================

Then you can probably dissect them with git magic? I don't know, it sounds
pretty risky. Better not do it.

Usage
-----

Clone this repo and run `./import`.

It doesn't take any parameters. It checks out a new orphaned branch (backups,)
and dedicates a unique commit to each successive backup. Backups are expected
to be found under ~/Dropbox/Apps/WorkFlowy, in the Data and History subfolders.

Subsequent invocations of `./import` will commit only newer backups.

The script uses hardlinks, so the repo should be on the same file system as the
backups.

Very scholarly research
-----------------------

```sh
$ du -hs ~/Dropbox/Apps/WorkFlowy
242M    ~/Dropbox/Apps/WorkFlowy

$ tar czf archive.tgz ~/Dropbox/Apps/WorkFlowy 2>/dev/null
$ du -hs archive.tgz
90M archive.tgz

$ git clone https://github.com/staticshock/wf-backups
$ cd wf-backups
$ ./import >/dev/null 2>&1
$ du -hs
2.3M    .
```

Seems to work.
