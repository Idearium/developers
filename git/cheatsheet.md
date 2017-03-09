# Idearium Git cheat sheet

## `git show-branch`

Shows commits across branches making it easy to visualise which commits exist in which branches.

## `git show {commit}`

Shows the commit message and a diff of the commit compared to the previous commit.

## `git log --pretty=oneline --abbrev-commit --name-status`

Outputs the short hash of each commit, along with the comment and list of changes made to the files in the commit.

## `git checkout -b {name} && git push -u origin {name}`

Creates a local branch and then pushes it to the origin repository.

## `git branch -D {name} && git push origin :{name}`

Deletes a local branch then removes it from the origin repository too.

## `git reset --hard {commit}`

Resets the repository to the specific commit hash, discarding all commits after that.

## `git reset --hard origin/master`

Resets the repository to the state of the master branch on the origin.

## `git reset --soft {commit}`

Resets the repository to the speicific commit hash, but keeps the changes to the files.

## `git diftool --cached`

Uses your configured diffing application to show the staged changes.
