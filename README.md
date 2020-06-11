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
Pull updates to `./target` from `/mnt/src`:
```
echo target >> .pull.lst
pull /mnt/src
```

Pull updates to `./target` from `/mnt/src`, excluding
`/mnt/src/target/too-big-for-dest`:
```
echo target >> .pull.lst
echo too-big-for-dest >> .pull-nopull.lst
pull /mnt/src
```

Pull updates to `./target` from `/mnt/src`, but keep `./target/must-stay` even
if it's not in `/mnt/src/target`:
```
echo target >> .pull.lst
echo must-stay >> .pull-nodelete.lst
pull /mnt/src
```

