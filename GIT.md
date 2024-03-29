# GIT

## Problems

### Problem

When I created a PR, I realized one of the commits belonged to another branch, so it had to be removed from the PR. [delete commits]

### Solution

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

### Problem

Save temporal changes in GIT and load them later.

### Solution =>

1. Stash the changes.

   ```bash
   git stash -m <comment>
   ```

2. Load the changes.

   ```bash
   # To see the available stashs
   git stash list
   # To apply the stash and delete it later
   git stash pop stash@{id}
   # To apply the stash and keep it
   git stash apply stash@{id}
   ```

### Problem

Run something when creating a commit. In this case, linting the code.

### Solution

1. Install husky and lint-staged.

   ```bash
   npm i husky lint-staged
   ```

2. Create a `.huskyrc.js` file with the hooks to run.

   ```javascript
   module.exports = {
     hooks: {
       'pre-commit': 'lint-staged',
     },
   };
   ```

3. Create a `lintstagedrc.js` file with:

   ```javascript
   module.exports = {
     // executed script depending on the file to be commited.
     'src/**/*.ts': ['npm run lint:ts'],
     'src/**/*.tsx': ['npm run lint:tsx'],
   };
   ```

4. Define the scripts from the previous step in `package.json`.

   ```json
   {
     "scripts": {
       "lint:ts": "eslint . --ext .ts",
       "lint:tsx": "eslint . --ext .tsx"
     }
   }
   ```

## Concepts

### Interactive rebase

It serves mostly for cleaning up local commit history. It shouldn't be used with remotes, because it will re-write the commits (hashes will change).

1. Determine the base commit (how far in history we want to go). For this, we could either give the commit hash, or count the number of commits.

```bash
git rebase -i HEAD~3 #This means until the 3rd commit including the head
```

Then we are gonna get a text-editor (tool for vs-code) in which we define what we want to do to each commit.

- squash will combine the selected commit with the previous one

### Reflog
![image info](./images/reflog.png)


![image info](./images/reflog2.png)

With reflog we get the history of executed actions. We could then execute a reset to go before we messed up everything, which includes deleting branches and commits.