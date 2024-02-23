# GitHub to BitBucket Migration

## Goal
The goal of this task is to migrate the application code from a GitHub repository to a Bitbucket repository.

## Pre-Requisites
- GitHub Repo: [https://github.com/dptrealtime/java-login-app.git](https://github.com/dptrealtime/java-login-app.git)
- Create two Bitbucket accounts to follow best practices (Developer1 & Developer2 accounts).
- Create a private Bitbucket repository and add Developer1 and Developer2 as collaborators.

## Migration
1. Clone the GitHub repository.
2. Clone the Bitbucket repository as Developer1.
3. Migrate the code from the GitHub repository (local master) to the Bitbucket repository (local master).
4. Follow a branching strategy and commit the code to a “feature” branch of the Bitbucket repository.
5. Raise a Pull Request to merge the code from the Feature branch to the Master branch and add Developer2 as a reviewer.
6. Login to Bitbucket as Developer2, then approve and merge the PR using the “no fast forward” merge strategy.

## Verification
- Verify that the code is now showing in the Bitbucket repository.
