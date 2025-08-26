# repo-replacement-test

This is a test of a procedure to delete a file from a GitHub repository's history. It involves replacing the repository with a duplicate which doesn't have the file in any form, including old cached commits on GitHub's server.

[This GitHub article](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository) outlines the generally recommended procedure, but it involves asking GitHub support to scrub pull requests' references to old commits, which has the following uncertainties:

- GitHub support may or may not grant the request, depending on whether they think the need for deletion is valid.

- I wasn't able to confirm what exactly GitHub support would do; would they redact certain words/metadata in each pull request, or would they delete the pull request threads in their entirety?

## Step 1: first repo

- Create repo `repo-replacement-test`; make it public, so that we can test whether GitHub forces a delay before reclaiming a public repo name

- Create and merge pull requests
    
    - PR 1: Add README (or edit if already auto-created)
    - PR 2: Edit README and add config.json, in same commit
    - PR 3: Edit README and edit config.json, in separate commits
    - PR 4: Delete config.json
    - PR 5: Edit README

- Clone the repo locally at the latest version

## Step 2: second repo

- [Duplicate](https://docs.github.com/en/repositories/creating-and-managing-repositories/duplicating-a-repository) repo-replacement-test, without the PRs, to repo-replacement-test-temp

- Clone repo-replacement-test-temp locally
- Locally, run git-filter-repo on repo-replacement-test-temp to delete config.json from its history: `python path/to/git-filter-repo --sensitive-data-removal --invert-paths --path config.json`
- Force-push local to remote for repo-replacement-test-temp: `git push --force --mirror origin`

## Step 3: rename

- Rename repo-replacement-test to repo-replacement-test-original; now the repo can be privated or deleted

- Rename repo-replacement-test-temp to repo-replacement-test; see if GitHub forces any delay before this can be done

## Step 4: check for PR number conflicts

- Create a new PR in repo-replacement-test. If it ends up being PR #1, then go back to check the older "merge pull request #1" commit. See if GitHub makes the text "#1" link to the new PR #1.
