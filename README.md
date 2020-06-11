# `pull` updates from a directory
## Motivation
Like most pieces of software, `pull` was built to solve a specific kind of
problem.  Basically, when you're backing up or restoring data, you run into two
kinds of issues:
- accidental deletion (e.g. from `rsync --delete`)
- and accidental overwriting (e.g. from `rsync`).

> These issues get exacerbated when backing up/restoring between mediums with
> different directory hierarchies (e.g. between partial and full hierarchies).

## Requirements
- `rsync`
- `sh`

## Examples
Pull updates from `/mnt/src`:
`pull /mnt/src`

Pull updates from `/mnt/src`, excluding a `/mnt/src/too-big-for-dest`:
```
echo too-big-for-dest >> .pull-nopull.lst
pull /mnt/src
```

Pull updates from `/mnt/src`, but keep the `./must-stay` inode even if it's not
in `/mnt/src`:
```
echo must-stay >> .pull-nodelete.lst
pull /mnt/src
```

