# repo-replacement-test

This is a test of a procedure to delete a file from a GitHub repository's history. It involves replacing the repository with a duplicate which doesn't have the file in any form, including old cached commits on GitHub's server.

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
