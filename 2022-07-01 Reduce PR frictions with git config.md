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
