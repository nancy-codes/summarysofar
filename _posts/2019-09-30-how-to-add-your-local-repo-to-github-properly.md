---
layout: post
title: How to add your local repo to GitHub properly
date: 2019-09-30 21:14 -0600
---
After playing around with git for a couple of months, I should have known better the first step of getting my project up and running. Turned out that I didn't. That's not okay, so I decided to write about the proper way of linking a local and remote repo together -- I won't make this mistake again!

But first, let me describe my erroneous workflow.

1. Create a new Rails project. Running the following command created a new directory called `my_project`.
```
# inside my project folder
$ rails new my_project -T -d postgresql --api
```

2. Run `git init` to add version control functionality.

3. Visit my GitHub account and create a new repo with the same project name, `my_project`, initializing with a README (this was part of the problem!).

4. Run the following command:
```
$ git remote add origin remote_repository_URL
```

4. Then I checked out to a new branch called `setup`, since my work pertained to installing gems and creating folder structures. Then I did git add, commit, and push these new changes to GitHub.

I did see a colored flash message of a new PR on GitHub. When I opened it though, I got a weird message:

```
There isn't anything to compare.

master and setup are entirely different commit histories.
```

What?! I thought my local repo and remote repo in GitHub were in sync with each other. What went wrong?

After googling, I realized that my workflow was a bit out of order. So here is the proper way to do it ([github help page](https://help.github.com/en/articles/adding-an-existing-project-to-github-using-the-command-line)).


1. Create a new project on your local repo, and `git init` it.
2. `git add` all recent changes and `git commit` them as "Initial commit".
3. Create a new repo on GitHub, WITHOUT README. Depending on whether `[] Initialize with README` is checked or not, you'll be redirected to different pages. If unchecked, you will see a box with the header called `Quick setup` on top of the page.
4. Back in Terminal, `git remote add origin remote_repository_URL`.
5. Push the changes in local repo to GitHub, `git push -u origin master`.

This above routine should be your second nature. Practice it early and often so that you won't be hindered by initial setup issues.
