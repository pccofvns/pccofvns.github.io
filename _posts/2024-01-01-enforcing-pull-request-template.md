---
layout: post
title: "Best Practices: Enforcing Pull Request Template"
date: 2018-09-12
---

## Overview

Maintaining consistency and adherence to best practices is crucial in software development, especially when the codebase is old, and collaborating on projects with multiple contributors. In this particular scenario, we’re solving following problems:

**Ensuring that the code changes contain relevant information**
We need to make sure that there is enough information about the code change so that it can be traced to some requirement/defect so that everyone can understand what was done and why. It is also required that we describe the reason and impact of all the changes for other teams like QA.

**Avoid manual repetition of information on multiple platforms**
It would've sufficed to link the pull request to some Issue Key of issue tracking tools (say JIRA). However, some details are required to be put in the pull request so that when someone looking into commit logs, they don’t have to go to the issue tracker for each commit to find the relevant details which should've been in the commit in the first place. Putting details in JIRA also creates a need to validate the relevant details. Since, there would be some overlap of the details that are written in the pull request and what is there in JIRA; developer aren’t too keen to put those details again in JIRA. In our case GitHub and JIRA are not integrated. The Management, QA and non Engineering Teams are more keen to have all relevant details in the JIRA. I personally like to have all the possible details related to code change, its impact, and tests executed on the pull request itself so that it helps with Code Review process. 

All cross-functional teams agreed upon a pull request template, that contains minimum basic information needed for both Pull Request, and JIRA.

### Automating the Process and ensuring adherence.

The task is to ensure that this whole process is automated and there is no lapse.

#### Create a pull request template

1. Create file named [pull_request_template.md](https://gist.githubusercontent.com/pccofvns/a02fd59870d78da437bf7a57211f930d/raw/a27bdd73b1963a0cf480b820c09d0bf233d4fa2b/pull_request_template.md)
```
## Description of Changes
### RCA
<!--- Root Cause Analysis. The title of the story shall be enough in case the changes are related to a user story -->
### Code Changes
<!--- Describe the code changes done to implement the story or to fix the defect-->
### Impact Analysis
<!--- Describe the impact of this change on other modules and/features -->
## Issue ticket number(s)
JIRA-0000
## Tests
- [ ] This the detail of the first test case that you've run. You can add more below.
```
2. Place this file in an appropriate place, which is the `.github` directory inside the repository, or the organisation wide `.github` repository. Now every time a pull request is created, the pull request details would be pre populated with this content for the developer to fill.

### Create a script to validate the Pull Request Validate

Since I wanted to this pull request template to be used across all my repositories, it would make sense to keep such validation script in some common place. 

1. Create a GitHub repository say `scripts`.
2. Inside this repo, create a file to parse with Github pull request title and body as below
   {% gist e4d7a60733c782d3e175560da461d0b9 gh_pull_request_linter.py %}
3. A `requirements.txt` file at the same location to install dependencies as below:
   ```
   requests==2.32.3
   urllib3==1.26.19
   ```

### Create GitHub action to validate pull requests

Say you want to use the pull request validation in a this scripts repo, where you’ve this aforementioned `pull_request_template.md` inside `.github` directory.

1. Create a folder `workflows` inside this `.github` directory (if it doesn’t exist already)
2. Create a file `pull_request_lint.yml` as below:
   {% gist 7bc7c2af93b1b172567fc65f24430be9 gha_pr_lint.yml %}

### Create branch protection rules to ensure that this workflow must pass before a Pull Request can be merged

While the action will itself run when a PR is created targeting `main` branch. You can update it to suit your needs.

Final structure of scripts repo:

```
scripts
├── .github
│   ├── pull_request_template.md
│   └── workflows
│		└── pull_request_lint.yml
├── requirements.txt
├── gh_pull_request_linter.py
```

## Working Examples

You can visit my `[pccofvns/scripts](https://github.com/pccofvns/scripts)` repo for working example. To use the same pr lint process in other repos, see `[pccofvns/takshashila](https://github.com/pccofvns/scripts)` repo. 