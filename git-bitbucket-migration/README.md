Goal
Currently application code is staged into GitHub repository and the requirement is to migrate the code to Bit Bucket repository.

Pre-Requisites
Github Repo: https://github.com/dptrealtime/java-login-app.git
Create two Bitbucket  accounts to follow the best practices (Developer1 & Developer2 accounts)
Create private Bitbucket repository and add Developer1 and Developer2 as collaborators. 
Migration
Clone GitHub repository
Clone Bitbucket repository as Developer1
Migrate the code from Github repository (local master) to Bitbucket repository (local master)
Follow branching strategy and commit the code to “feature” branch of Bitbucket repository.
Raise Pull Request to merge the code from Feature branch to Master branch and add Developer2 as reviewer.
Login to Bitbucket as Developer2 then approve and merge the PR using “no fast forward”  merge strategy.
Verification
Verify that the code is now showing in the Bitbucket repo.
Note: Explore various other options to migrate the code from Github to Bitbucket and add the possibilities in the comments.