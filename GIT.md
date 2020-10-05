# GIT

**Problem** => When I created a PR, I realized one of the commits belonged to another branch, so it had to be removed from the PR. [delete commits]

**Solution** => 

1. Copy branch to a temporal one. 

   ```bash
   git checkout -b new_branch old_branch
   ```

2. Reset original branch to master (or main branch).

   ```bash
   # Switch to old_branch
   git checkout old_branch
   
   git reset <branch | master>
   ```

3. Add the desired commits to the old_branch (leaving the unwanted behind).

   ```bash
   git cherry-pick <commit_keyid>
   ```

