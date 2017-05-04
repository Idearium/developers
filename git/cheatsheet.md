# Idearium Git cheat sheet

## `git show-branch`

Shows commits across branches making it easy to visualise which commits exist in which branches.

## `git show {commit}`

Shows the commit message and a diff of the commit compared to the previous commit.

## `git log --pretty=oneline --abbrev-commit --name-status`

Outputs the short hash of each commit, along with the comment and list of changes made to the files in the commit.

## `git checkout -b {name} && git push -u origin {name}`

Creates a local branch and then pushes it to the origin repository.

## `git checkout -b {name} origin/{name}`

Creates a local branch from existing remote branch with tracking.

## `git branch -D {name} && git push origin :{name}`

Deletes a local branch then removes it from the origin repository too.

## `git reset --hard {commit}`

Resets the repository to the specific commit hash, discarding all commits after that.

## `git reset --hard origin/master`

Resets the repository to the state of the master branch on the origin.

## `git reset --soft {commit}`

Resets the repository to the speicific commit hash, but keeps the changes to the files.

## `git difftool --cached`

Uses your configured diffing application to show the staged changes.

## `git fetch --all`

Perform a git fetch, and include all remotes that are configured on your local repository.

## `git pull --rebase`

Use this when you're pulling in remote changes, to a branch that has unreleased commits. It will ensure your commits remain on top.

## `git commit --amend -m "{new commit message here}"`

Amends the last commit message, and creates a new commit. Be aware that it creates a new commit, and therefore take into consideration remote branches as you may need to force push.

## `git stash save -u "{optional message here}"`

Stash the changes in current branch including untracked files.
