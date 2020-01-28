# Aprendia
A collection of random thoughts and resources. Very much a WIP! 

## [Git](/git)

## [Frontend](/frontend)

## [Backend](/backend)

## Personal Project(s)

## Deployment Steps 
* Push your changes to GitHub, open a PR. You can also open a "draft" PR if needed.
* Check your "review app" on Heroku if needed. 
* Request a review. 
* Ensure that no one else is currently deploying/waiting for staging to build, coordinating as needed. 
* Announce your intent to deploy to staging if needed. 
* Once your PR is approved and all test pass, merge your changes into master by "squash" commiting. 
* Wait for staging to deploy (tests pass, build finished).
* You can probably delete your local branch now. Your remote branch should have been deleted automatically after merging to master.
* Once staging is built, deploy to production using the #deployment Slack channel (i.e., not from Heroku GUI).
* Monitor for errors in Slack. It takes up to ~15-20min for your changes to propogate in prod after a successful deployment. 
* Celebrate! 🎉

