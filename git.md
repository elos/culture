Git
===

Commits
-------

Commit messages should be less that brief and succinct (less than 80 characters).

Only write your commit messages in the present tense. Lower case.

i.e., "add the ability to create a user"

This is the only correct format, past tense is never needed. Anything without an action verb is to vague.
Think about applying changsets (commits) as actions, each commit changes your in a particular way.

When more information is needed, supply it in the details of the commmit messages as bullets. Always cap at three bullets

i.e.,

    ```vim

      add ability to create a user

       * I needed to rework the database connection for this
       * Still need to do proper error handling
       * Will think more about live updates
    ```

Your commits will never be so incomplete, else they certainly only exist on a separate branch.

Branching
---------

Always work in a branch. The convention is to name the branch:

  `<github_username>/<feature>`

Rebase aggresively.

Creating a new branch:

  ```bash
     git checkout -b <branch_name>
  ```

Switching between branches:

   ```bash
     git checkout <branch_name>
   ```

Deleting Branches:

   ```bash
     git branch -D <branch_name>
   ```

Rebasing
--------

Rebasing is the elos engineer's replacement for merges. Merges are sloppy, uncoordinated, and reproduce diff history.

Rebasing is especially useful for development on branches.

When you checkout a new branch from master, the split of the commit history occurs at the current HEAD of the master branch (the most recent commit).

Over time, as you work on another branch, master can move forward as others add commits, and your branch will become stale (n commits behind master).

Rebasing takes your commits applied sense the initial checkout, re-checks out master at it's curren HEAD, and then applies your changesets sequentially to the new state of the master branch.

Benefits
  * Keeps commit history clean
  * Allows for problem solving of conflicts on a per-commit basis
  * Keeps your feature branches up to date, and prevents the punctual interruptions of "Merged master into <branch_name>" commits

Rebasing a branch on master:

  ```bash
    git rebase origin/master
  ```

Interactive rebases are especially useful:

  ```bash
    git rebase -i origin/master
  ```

You will be presented with different options, among them squashing commits together, discarding commits, and fixing commit messages.

Interactive rebasing contributes to the goal of clean commit history, and effective merges to master. Your commit behavior can be frequent on the separate branch, and you can distill the essential progress upon rebase.

Rebase aggresively against master when working on separate branches.

Merging to Master
----------------

The only merging you will ever do will be to the master branch. Always use the `--ff-only` flag

 1. rebase your branch on master (interactively to clean up your commit history)
    ```bash
      git fetch origin/master
      git rebase -i origin/master
    ```
 2. checkout your local master branch, make sure it is up to date with origin/master as well
    ```bash
      git checkout master
      git pull origin master
    ```
 3. now you can _merge_ your commits, using --ff-only (fast-forward only)
    ```bash
      git merge <branch_name> --ff-only
    ```

Fast forward merges fast-forward master to the HEAD of your branch. Effectively the counterpart of a rebase.

This merge requires no merge commit, and does not reproduce change sets, as it only applies all your commits on the feature branch sequentially to master.
