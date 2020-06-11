# `pull` updates from a directory
## Motivation
Like most pieces of software, `pull` was built to solve a specific kind of
problem.  Basically, when you're backing up or restoring data, you run into two
kinds of issues:
- accidental deletion (e.g. from `rsync --delete`)
- and accidental overwriting (e.g. from `rsync`).

> These issues get exacerbated when backing up/restoring between mediums with
> different directory hierarchies (e.g. between partial and full hierarchies).

Oh, and `pull` supports subpath preservation: so you can pull `src/a/b/c` to
`./a/b/c` with relative ease:
```
echo a/b/c >> .pull.lst
pull src
```

## Requirements
- `rsync`
- `sh`

## Examples
Pull updates to `./target` from `src`:
```
echo target >> .pull.lst
pull src
```

Pull updates to `./target` from `src`, excluding `src/target/too-big-for-dest`:
```
echo target >> .pull.lst
echo too-big-for-dest >> .pull-nopull.lst
pull src
```

Pull updates to `./target` from `src`, but keep `./target/must-stay` even if
it's not in `src/target`:
```
echo target >> .pull.lst
echo must-stay >> .pull-nodelete.lst
pull src
```

