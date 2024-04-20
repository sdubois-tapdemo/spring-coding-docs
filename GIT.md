# GIT


[Think Like (a) Git](https://think-like-a-git.net/)
(Think Like a Git)[https://think-like-a-git.net/]


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
4. Are you happy with the result?
   If YES: Move your real branch forward to where the test_merge branch is.
   ```
   git checkout master            ## Switch to ^master' and merge 'test_merge' into it
   git merge test_merge           ## Complete the merge on master if all is fine
   ```

   If NO: Delete the test_merge branch.
   ```
   git checkout master
   git branch -D test_merge      ## Delete the test_merge
   ```

### Savepoint Pattern
1. Make sure you're on the right branch and that you have a clean working state.
   ```
   git checkout master            ## Go to the 'master' branch
   git status                     ## Verify you are on 'master' and have a clean state
   ```
2. Create a new branch to use as a savepoint, but don't switch to it.
   ```
   git branch savepoint           ## Create 'savepoint' branch
   git status                     ## We should be still on 'master' branch
   ```
3. Do the merge.
   ```
   git merge spiffy_new_feature   ## Merge 'spiffy_new_feature' into 'savepoint'
   ```
   If you want to abort the merge at this point, type
   ```
   git reset --hard
   ```
4. Are you happy with the result?
   If YES: Move your real branch forward to where the test_merge branch is.
   ```
   git branch -d savepoint        
   ```

   If NO: Delete the test_merge branch.
   ```
   git reset --hard savepoint     ## Replace 'master' with 'savepoint'
   git branch -d savepoint        ## If you want to clean up, you can now delete the savepoint
   ```





## GitX
```
brew install gitx
```
