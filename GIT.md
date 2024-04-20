# GIT

(Think Like (a) Git)[https://think-like-a-git.net/]


```
# Visualize the Git history
git log --oneline --all
git log --oneline --all --graph
```

## Git Commit
### Ammend
Back when I used Subversion, the only thing to be done about this was to add the new change in another commit. Often, I'd wind up with three or four versions in my history. The first one would say "add feature X", and the next several would have messages like "oops, found typo" or "bugfix" or "forgot to run tests".
This keeps all of your related changes bundled together in one commit, so you can understand it more quickly when you're reviewing it later.
```
git commit --amend
```

## Git References
### local branch reference
Local branch references are specific to a single repository: your local one. Commands that affect local branch references include commit, merge, rebase, and reset.

### Remote branch references
Remote branch references are also specific to a single repository, but one that's previously been defined as a remote. Commands that affect remote branch references include fetch and push.
(The pull command is a special case: it combines fetch and either a merge or a rebase, depending on how you've got Git configured.)

### Tag references
Tag references are basically like branch references that never move. Once you've created a tag, it will never change (unless you explicitly update it using the --force option). This behavior makes them useful for marking specific versions of a software package, or marking exactly what got deployed to a production server on a particular date. As of this writing, I only know of one command that affects tags. As you might guess, it's tag.

## Git Merge
- Use the Scout pattern if you're still unclear on exactly what git merge does, or if you think it's likely that you'll decide to back out of the merge.
- Use the Savepoint pattern if you're pretty sure what you want to do, but just want to leave yourself an undo button in case things get too messy.
### Scout pattern

1. Make sure you're on the right branch and that you have a clean working state.
   ```
   git checkout master            ## Go to the 'master' branch
   git status                     ## Verify you are on 'master' and have a clean state
   ```
2. Create a new branch (I often name it test_merge) and switch to it.
   ```
   git checkout -b test_merge     ## Create 'test_merge' branch
   ```
3. Do the merge.
   ```
   git merge spiffy_new_feature   ## Merge 'spiffy_new_feature' into 'test_merge'
   ```
   If you want to abort the merge at this point, type
   ```
   git reset --hard 
   ```
4. Switch to your visualizer and predict how its view will change when you refresh it.
5. Refresh your visualizer and see whether your prediction was correct.
5. Are you happy with the result?
7. If YES: Move your real branch forward to where the test_merge branch is.
8. If NO: Delete the test_merge branch.








if you want to test merge the new_feature branch into the master
```
git checkout master            ## Go to the 'master' branch
git status                     ## Verify you are on 'master' and have a clean state 
git checkout -b test_merge     ## Create 'test_merge' branch
git merge spiffy_new_feature   ## Merge 'spiffy_new_feature' into 'test_merge'
git reset --hard               ## Abort the merge if there are conflicts that can not be resolced

## Complete the merge on master if all is fine
git checkout master
git merge test_merge

## Drop the test_merge branch
git checkout master
git branch -D test_merge
```
### Savepoint pattern

## GitX
```
brew install gitx
```
