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

## Requiring a specific team for PR approvals

[.github/workflows/required-approvers.yaml](.github/workflows/required-approvers.yaml) gives you more fine-grained control over who is required to approve a PR before it can be merged. It will fail a GitHub check if the PR does not have at least 2 approvers from the specified group. This provides additional protections outside of the typical Codeowners
required approvals.

**A use case for this would be:**

* You want team *Alpha* and team *Beta* to both be codeowners and you want at least 1 person from each team to approve every PR.
* GitHub branch protection rules allows you to set the number of `Required approving reviews` to 2 and set `Require review from Code Owners`
* The problem is, a PR can get approved for merge by 2 members of *Alpha* without *Beta* ever approving.

This GitHub action allows you to require approvals from each team explicitly.

**NOTE** Actions triggered from a `pull_request_review` does not update a PR status check, so it is difficult to use this as a PR gate. See <https://github.community/t5/GitHub-Actions/pull-request-review-doesn-t-update-PR-status-checks/td-p/43186>.

You will need to manually re-run this check (or update the PR) for the PR check to update after a PR has been approved

### Secrets

* `TEAM_SLUG_REQUIRED_APPROVERS`: GitHub team slug within the owner's org. At least 2 members of this group will be required to approve a PR
* `ORG_GITHUB_TOKEN`: Github Access Token with `read:org` access, to look up members of team. See <https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line>
asd
