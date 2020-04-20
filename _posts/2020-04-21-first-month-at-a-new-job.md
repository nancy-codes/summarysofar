---
layout: post
title: First month at a new job
date: 2020-04-21 00:36 +0900
---
It has been a month since I started a new job as a backend developer in South Korea.

First, it is a great delight working with those who know how to use giphy generously. My fellow colleagues have a good sense of choosing the most amusing giphy. And I'm just amazed at their blazingly fast, reflexive skills while trying to hold my laugh silently.

Second thing that's intrigued me the most is a bewildering array of abbreviations. I guess developers in general are fond of aliasing any word into less than five letters. It's quick and exclusive. It took me a while, took me an intentional practice to get the hang of my company's lingo. And now, these abbreviations are cached in my memory; and I don't want to call these words by their full names.

In the span of a month, I have committed some embarrassing mistakes. My thoughtless questions have conclusively demonstrated a lack of depth in requisite knowledge to do my job well. At times, my "contributions" seemed like an odd voice into an otherwise harmonious a cappella.

BUT again, I am amazed by my coworkers' unparalleled kindness. They swallow their unpleasant surprises and show me how to perform tasks properly like a good teacher. I'm just grateful to be part of this team, who challenge me to develop not just coding skills but empathy toward other developers.

In this post, I will quickly share a couple of things that I've learned through mistakes.

1. Spend some time reading through slack channels. Threads are rich source of information where you'd learn the most about your company lingo (more than Google). Garner keywords from the thread first, and then do research.

2. Pick up simple tasks that you know how to do. Personally, the process of writing tests for missing spec helped me get familiar with the existing schema and grasp the data flow. Rspec-ing might seem tedious, but it will reveal hidden links between models that were once concealed from you!

3. Learn use cases of `git rebase`: one to organize your commits and another to keep your feature branch void of merge conflicts with the master branch.

  - **Scenario 1.** You made 5 commits in your feature branch. They are fragmented and verbose. Before you push the changes to remote branch, squash them into a single commit by:

  ```
  $ git rebase -i HEAD~5
  ```
  - A new page will pop up, showing 5 lines of previous commits prefixed by `pick`. The first one is the most recent one, which you want to keep it as is. Since you want to join these 5 commits into one, the next 4 lines need to be modified, by changing the prefix from `pick` to `squash` (or simply `s`). Once you save these changes, then another page will pop up to ask you to modify the commit messages. There will be five of them, but you can delete or comment them out and write a new one.

  - **Scenario 2.**  You are working on a feature branch locally. Meanwhile, the remote master branch had several merges. Your feature branch should be aware of these changes; that is, it should be rebased to this updated master. Inaction on your part will invite merge conflicts in near future, so regularly check the status of the remote master branch.

  ```
  $ git checkout master
  $ git fetch
  $ git checkout <your_feature_branch>
  $ git rebase origin/master
  (fix conflicts if they exist)
  $ git push -f origin <your_feature_branch> # don't forget the f (force) push!
  ```

And lastly, keep writing, to remind your forgetful self and inform your awesome colleagues.
