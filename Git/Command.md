# Command

To delete a remote branch

```Bash
git push -d origin <branch-name>
```

To delete a local branch

```Bash
git branch -d <branch-name>
```

## undo the last commit

`https://www.git-tower.com/learn/git/faq/undo-last-commit/`

`git reset --soft HEAD~1`

Reset will rewind your current HEAD branch to the specified revision. In our example above, we'd like to return to the one before the current revision - effectively making our last commit undone.

Note the --soft flag: this makes sure that the changes in undone revisions are preserved. After running the command, you'll find the changes as uncommitted local modifications in your working copy.

If you don't want to keep these changes, simply use the --hard flag. Be sure to only do this when you're sure you don't need these changes anymore.

`git reset --hard HEAD~1`

## Undoing Multiple Commits

The same technique allows you to return to any previous revision:

`git reset --hard 0ad5a7a6`

Always keep in mind, however, that using the reset command undoes all commits that came after the one you returned to.
