# Intro

Given two directories, hashes each files contents, and renames any matching
files in the target dir to the file with the same name in the source dir.

In the following example:
```
t/123 - contents are "abc"
t/321 - contents are "ABC"
t2/foo - contents are "ABC"
t2/bar - contents are "abc"
```

`hash-rename t/ t2/ ` would rename `t2/foo` to `t2/321` and `t2/bar` to
`t2/123`.

There are checks to prevent overwriting file with the same hash.

hash-rename won't recurse into subdirs of the source and target directories.

## Use Case

I wrote this script to help fix a problem where I had `BROKEN~1.MP4` names on a
network device, but correct names on a local device. I could have re-rsync'ed
the files over, but this was a fun exercise. And it at least saved the trouble
of writing the files over the network a second time. The script still has to
read the whole file over the network, so no big savings unless there is some
asymmetry in bandwith and/or metering on your network connection that the script
can take advantage of.

## Setup

A `cpanfile` is present, so if you have `cpanm` installed, you can pull down the
dependencies easily:

`cpanm -l local --installdeps .`

And you can use `local::lib` in perl to make use of the modules in the `local`
dir.
