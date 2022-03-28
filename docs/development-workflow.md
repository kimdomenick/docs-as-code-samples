# Sample development workflow

**This is sample of a deployment workflow for a technical, developer audience**

NOTE: The links here are not pertinent to an actual development workflow.  
For instance, you'd never need to read about wine making to deploy code to
Github and create a release branch. Links are used solely as an example of how
to walk a reader through a complex workflow involving multiple, separate 
documents that should be reviewed in order. 


# Local development
Most development will begin with creating a feature branch locally.  Naming 
conventions for feature branches include the JIRA ticket number and a
short ticket description.

```bash
$ git checkout -b JIRA-ticket/My-short-ticket-description
```

Before starting any development, review the following docs:
* [Wine Making Made Easy][]

Review any other appropriate documentation related to the work you are doing.


# Deploying to a lower environment for QA
Once a feature branch is ready for the QA process, push the branch to the
appropriate lower environment for QA

Feature branches do not necessarily need to be pushed to all lower environments.
A typical development workflow might be:
Local => Testing => Production

A feature branch can be deployed to a lower environment by merging into the
local environment branch and pushing to that branch.

```bash
$ git checkout testing
$ git pull
$ git merge feature
$ git push
```

Deployments are monitored in two steps:
* [Wine Making Made Easy][]
* [Cheap Home Staging][]

## The QA/Testing process
Following deployment to a lower environment, review the following doc:
* [Cheap Home Staging][]


# Creating a PR
This step may happen in conjuction with a deployment to one of the lower
environments, as part of the QA process.  During QA, it is helpful to name the
PR with "WIP" in the title and tag it with the Work In Progress tag.  This will
prevent someone from prematurely assigning the PR and performing a code review.


# Production release and deployment
Production deployment is scheduled and coordinated through John Doe.  Contact
John for details.

**Once all PRs that should be included in the release are merged into the `main`
branch, proceed with the following tasks.**

## Determine release number
First check the CHANGELOG.md file to determine the next release.
Example:

The last release version was 1.21.12
The next minor release will be 1.21.13
The next major release will be 1.22.0

## In the terminal
1. Create a new release branch.
2. Manually make the changes needed to the CHANGELOG file.
3. Commit the changes and push branch to remote.

```bash
git checkout main
git pull
git checkout -b release/1.21.12
vi CHANGELOG.md
make edits and save
git commit -am "Add new release version to changelog"
git push -u origin release/1.21.12
```

## In the browser
Create a pull request from the new release branch and get it approved.
Wait until the build has completed, then merge it into `main`.
Manually add a new release in GitHub.


# Monitoring and troubleshooting deployments

## Open a support ticket
1. Go to host URL
2. Click the login link
3. Login with credentials or select an SSO provider
4. View the dashboard
5. Click the **Create a Ticket** button
6. Fill in the required fields
7. Await a response

NOTE: The host is very slow and may not respond immediately.  Allow 2-3 weeks
for a ticket update.  Check back regularly. 

See also:
[Cheap Home Staging][]


[Wine Making Made Easy]: /docs/wine-making-made-easy.md
[Cheap Home Staging]: /docs/cheap-home-staging.md
