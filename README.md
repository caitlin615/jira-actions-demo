# jira-actions-demo

## About

The GitHub Action workflows in this repo do the following

* When a new PR is opened, a new Jira ticket is created
* A comment is made on the PR with a link to the new Jira ticket
* When a PR is approved, a comment is made on the Jira ticket with the name of the user who approved it
* When the PR is merged, the Jira ticket is transitioned
* When the PR is closed without merging, the Jira ticket is also transitioned (this can be different or the same as if the PR is merged).

## Requirements

GitHub secrets:

* `JIRA_BASE_URL`: Your Jira cloud base url, like `https://example.jira.com`
* `JIRA_API_TOKEN`: API Token generated at <https://id.atlassian.com/manage-profile/security/api-tokens>. See [Jira Login GitHub action](https://github.com/marketplace/actions/jira-login)
* `JIRA_USER_EMAIL`: Email associated with API Token
* `JIRA_PROJECT_ID`: Project ID where Issues should be opened
* `JIRA_ISSUE_TYPE`: Jira issue type to use when creating new issue
* `JIRA_TRANSITION_CLOSE_MERGED`: Where to transition Issue when the PR is closed and merged.
* `JIRA_TRANSITION_CLOSE_UNMERGED`: Where to transition Issue when PR is closed _without_ merging.
