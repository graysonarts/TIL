---
tags: [ dev/cli, dev/cli/git ]
date: 2022-07-01
title: Reduce PR friction with git config
---
```
git config --global push.default current
```

This tells git to push the current branch to the name name branch on the remote.

```
git config --global push.autoSetupRemote true
```

This tells git to automatically set the upstream tracking branch to the "starting point" of the branch. In the github pull-request scenario this means you no longer need to do:

```
git push --set-upstream origin branch-name
```


> [!NOTE]
> If you use `git-town` to manage your repositories, this causes the automatic pruning of deleted branches on `origin` to not work.