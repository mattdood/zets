---
path: '/2023/2/complex-sed-replace-with-dry-run-testing-to-make-sweeping-repository-changes-20230201114726'
title: 'complex sed replace with dry run testing to make sweeping repository changes'
date: '20230201114726'
category: 'bash'
tags: ['linux', 'bash', 'sed', 'tip']
---

# complex sed replace with dry run testing to make sweeping repository changes
Recently I came across a need to make sweeping repository changes across many repos
and thought that `sed` would be the best way to accomplish this.

I used a few references for learning how to do a `dry run` (print the change but don't execute it)
as well as doing a recursive call with the `sed` replacement on specific file types.

### References
- [Testing recursive sed search and replace](https://unix.stackexchange.com/questions/113746/test-recursive-sed-search-and-replace-before-running)
- [Using the find command to search multiple filenames](https://www.tecmint.com/linux-find-command-to-search-multiple-filenames-extensions/)

## Breaking down the sed call
There are a few components to the `sed` call that I settled on, with 2 separate
commands that do different things.

### Dry runs with `find`
In this command we utilize a few separate options to accomplish our goal.

```bash
find . -type f -name '*.<my file extension>' -readable -writable -exec sed -n 's/<search string>/<replace string>/gp' {} \;
```

The output of this will illustrate the exact changes that would take place.

#### Options
1. `p` - option at the end of our `'s/search 1/replace 1/gp'` ensures we're printing.
1. `-n` - a "--quiet" execution

### Running the actual `sed`
To remove the `dry run` portion of the above we take out `p` and change `-n` to `-i`.

```bash
find . -type f -name '*.<my file extension>' -readable -writable -exec sed -i 's/<search string>/<replace string>/g' {} \;
```

#### Options
1. `-i` - Change "in place"

### Dry runs with `grep` interactivity
Below we use grep to find (interactively) our changes. This is doing effectively the
same thing as what we did above, just using `grep` to find the lines themselves
and piping the lines returned to our `sed`.

```bash
grep -rl --null "<search term>" | xargs -0 sed -e 's/<search term>/<replace term>/gp' | less
```

#### Options
1. `grep --null | xargs-0` - Terminates filenames by null-byte making it safe for
filenames with unutual characters

### Using `sed` with a backup file
In the following command we use a `.bak` extension to append to our files, this
allows us to verify our changes using the `diff` command.

```bash
grep -rl --null "<search term>" | xargs -0 sed -i.bak -e 's/<search term>/<replace term>/'
diff my-file.bak my-file
```

#### Options
1. `-i.bak` - Create a `.bak` of the same file to use as our "changed" file

