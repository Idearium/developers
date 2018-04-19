# Smart Commits

This integration between Jira and Github allows you to transition and comment on issues from your git commit. It reduces the need to double handle issues, it also displays all the branch, pull release and commit data on the issue in Jira.

## Structuring a commit message

Here is a basic example of a smart commit that would be entered into terminal: 

`git commit -m "Moved to using async/await for asynchronous speed FB-99 #resolved Resolves the issue which was some blocking code."`

This commit will add a message against the commit (as usual). The reference to FB-99 will then transition the issue to resolved. The text after the issue transition is a comment string and will be added to the Jira issue as a comment.

## Why use smart commits

Smart commits are useful because they automatically add and update data in Jira. This would otherwise require at least two actions;

1. A commit
2. An action in Jira e.g. transitioning an issue or adding a comment, or both.

## When to use a smart commit

Smart commits are most useful when you need to commit code and update Jira as a result of that commit. For a standard commit e.g. before lunch when you want to ensure your code is safe but you are not ready for any further actions, you do not need to use a smart commit.

Scenarios in which you would use a smart commit are;

1. When you are submitting a PR (as this might require leaving a comment for testing and transitioning the issue to verify)
2. When you are reviewing a PR (for issue transitioning or adding comments)

Please be careful when using smart commits, that you are 100% certain everything is good to go, ensure you have done your code review first.

## Transition

Smart commit can transition issues across the board, this is most useful when raising PRs (to go from in progress to verify, using #resolved), reviewing PRs (to go from verify to done, using #done) PRs or when starting a new issue (to go from to do to in progress, using #selected).

| Description | Syntax | Example |
| ----------- | ------ | ------- |
| Transitions issue to a particular workflow state. | `<ignored text> <ISSUE_KEY> <ignored text> #<transition_name> <comment_string>` | `git commit -m "audio now working regardless of time active in the app FB-99 #close bug fixed, please use IE10 for testing"` |

**Possible transitions**

Below are the transitions Idearium use in Jira. As an example if you are raising a PR you would transition from 'in progress' to 'verify' using #resolved.

| Jira Column | Workflow Status | Commit Syntax |
| ----------- | --------------- | ------------- |
| Backlog | Open (Idearium) To-do (RAS) | #open or #to-do |
| To do | Selected for development | #selected |
| In progress | In progress | #in or #in-progress |
| Verfiy | Resolved | #resolved |
| Done | Done | #done |

For transitions that have two words, like in-progress, you need only type the first e.g. #in.

## Comment

Smart commits can add comments to issues in Jira, this is useful in the situation of providing testing notes or feedback on a PR.

| Description | Syntax | Example |
| ----------- | ------ | ------- |
| Add a comment to an issue. | `<ignored text> <ISSUE_KEY> <ignored text> #comment <comment_string>` | `git commit -m "completed the addition of the new logo FB-90 #comment Please do a hard refresh to see the updates"` |

## Advanced commits

You can also do more complex things like use;

- Multiple commands on a single issue
- Multiple commands over multiple lines on a single issue
- A single command on multiple issues
- Multiple command on multiple issues

Here is a more detailed breakdown of [smart commits](https://confluence.atlassian.com/bitbucket/processing-jira-software-issues-with-smart-commit-messages-298979931.html).
