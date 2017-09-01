# 10. Git 基础及风格指南

Date: 11/04/2017

## Status

Accepted

## Context

We use git and GitHub in different ways, it’s emergency to teach team members with the git basics and style guide we will use.

## Decision

### git basics

1. setup ssh keys ([https://github.com/settings/keys][1]) or GUI;
2. clone repo into local system: `git clone git@github.com:huifenqi/django-project-skeleton.git`;
3. files store in three stages:
	![][image-1]
	1. `Working Directory`: holds the actual files;
	2. `Index`: staging area which store your changed files;
	3. `HEAD`: points to the last commit you've made.
4. `Working Directory` -\> `Index`: `git add <filename>` or `git add *`;
5. `Index` -\> `HEAD`: `git commit -m "Commit message"`;
6. push updates to Github: `git push origin master`;
7. create branch: `git checkout -b feature/x`
	![][image-2]
8. push branch to Github and others can see: `git push origin <branch_name>`;
9. sync local with Github: `git pull`;
10. make a new tag: `git tag <tag_name>`;
11. show history: `git log`;
12. show changes: `git diff <previous_commit_hash>`;
13. others: `git status`, `git branch`, `git tag`, etc.

### git style guide

#### Branches

* Choose short and descriptive names: [https://github.com/agis-/git-style-guide#branches][2];
* Use dashes to separate words.

#### Commits

* Each commit should be a single logical change. Don't make several logical changes in one commit;

#### Messages

* when writing a commit message, think about what you would need to know if you run across the commit in a year from now.

### Refs

* [http://rogerdudler.github.io/git-guide/index.html][3]
* [https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html][4]
* [https://github.com/agis-/git-style-guide][5]

## Consequences

Make sure everyone follow the guide, check the Github feeds often.

[1]:	https://github.com/settings/keys
[2]:	https://github.com/agis-/git-style-guide#branches
[3]:	http://rogerdudler.github.io/git-guide/index.html
[4]:	https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html
[5]:	https://github.com/agis-/git-style-guide

[image-1]:	files/file-stages.png
[image-2]:	files/branches.png