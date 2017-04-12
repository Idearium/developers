# Smart Commits

This integration between Jira and Github allows you to transition, log time and comment on issues from your git commit. It reduces the need to double handle issues, it also displays all the branch, pull release and commit data on the issue in Jira.

## Transition

| Description | Transitions issue to a particular workflow state. |
| Syntax | '<ignored text> <ISSUE_KEY> <ignored text> #<transition_name> <comment_string>' |
| Example | 'FB-99 #close Fixed this today' |

**Possible transitions**

- Open (backlog, Idearium)
- To-do (backlog, RAS)
- Selected for development
- In progress
- Resolved
- Done
- Closed

## Comment

| Description | Add a comment to an issue. |
| Syntax | '<ignored text> <ISSUE_KEY> <ignored text> #comment <comment_string>' |
| Example | 'FB-90 Added new logo' |

## Log time

| Description | Log time against an issue issue. |
| Syntax | '<ignored text> <ISSUE_KEY> <ignored text> #time <value>w <value>d <value>h <value>m <comment_string>' |
| Example | 'FB-34 #time 1w 2d 4h 30m Total work logged' |

## Advanced commits

You can also do more complex things like use;

- Multiple commands on a single issue
- Multiple commands over multiple lines on a single issue
- A single command on multiple issues
- Multiple command on multiple issues

Here is a more detailed breakdown of [smart commits](https://confluence.atlassian.com/bitbucket/processing-jira-software-issues-with-smart-commit-messages-298979931.html).
