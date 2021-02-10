---
title: "Git Recipes - Collaboration"
date: 2021-02-09T20:40:00-00:00
categories:
  - blog
tags:
  - coding
  - open
  - git
  - collaboration
---

# Keys

| Key or symbol    | Interpretation |
| ---------------  | -------------- |
| <...>            | Placeholder with possible formatting hints. You can use whatever name you want or appropriate, however, the same placeholder corresponds to the same item in this document. |
| project          | Centrally stored (e.g. on GitHub/GitLab), collectively developped repository you have forked. |
| default          | The main branch of the *project*. It is usually called `master`. |
| local            | A copy of a fork of the *project* on your computer obtained via [git clone](https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-clone). |
| feature          | Certain coding task, e.g. recitifying an issue or enhancing/adding functionality to the *project*. |
| remoterepository | Link to another fork of the *project* via [git remote](https://www.atlassian.com/git/tutorials/syncing). |
| remoteuser       | Another user also developping the *project* through his/her fork. |
| remotebranch     | A branch in the *remotuser*'s repository. |
| review           | Evaluate and modify a pull request (if needed). |


# Use cases

## Add link to another fork repository
Linking forks to your local repository allows you to pull commits from or push to that fork stored on GitHub/GitLab. When you clone a repository, the link `original` is created automatically. Sometimes, you may want to add further links for the use cases mentioned below.
#### You can add link to the project:
```bash
git remote add <project> <https://github.com/group/project.git>
git remote update
```
#### You can also add link to another fork of the project:
```bash
git remote add <remoteuser> <https://github.com/remoteuser/project.git>
git remote update
```

## Extend the project with a feature
1. Make sure that there is a [link to the *project*](#you-can-add-link-to-the-project)
2. Create a new local branch based on the *default* branch of the project to collect commits for the *feature*
```bash
git checkout -b <feature> <project>/<default>
```
3. Edit and [commit](https://www.atlassian.com/git/tutorials/saving-changes/git-commit)
4. [Push](https://www.atlassian.com/git/tutorials/syncing/git-push) the *feature* branch to your fork 
```bash
git push -u origin <feature>
```
5. Create pull request from *feature* branch of your fork to *defaut* branch of the *project*

## Review pull request
Reviewing pull requests is an essential part of collaboration. Here you download the updated code, test it, and send recommendations to the submitter so that (s)he can incorporate them into his/her repository (and automatically the pull request, as well).
1. Make sure that there is a [link to the *remoteuser*'s fork of project](#you-can-also-add-link-to-another-fork-of-the-project)
2. Retrieve the pull request by checking out the *remotebranch* from where the PR had been submitted
```bash
git checkout -b <review> <remoteuser>/<remotebranch>
```
3. Edit, [commit](https://www.atlassian.com/git/tutorials/saving-changes/git-commit), and [push](https://www.atlassian.com/git/tutorials/syncing/git-push) the *review* branch to your fork 
```bash
git push -u origin <review>
```
4. Create pull request from *review* branch of your fork to *remotebranch* of the *remoteuser*/*project*
