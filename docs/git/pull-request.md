# Test Pull Request Locally

## Create a local branch from pull request ID

Fetch the reference to the pull request based on its ID number, creating a new branch in the process.

```bash
git fetch origin pull/ID/head:<branch-name>
```

Switch to the new branch based on this pull request:

```bash
[master] $ git checkout <branch-name>
```

At this point, you can do anything you want with this branch. You can run some local tests, or merge other branches into it, including master. Make modifications as you see fit! When you're ready
you can push this new branch up or merge to `master` branch.

## Test a pull request by command line instructions

If you do not want to use the merge button or an automatic merge cannot be performed, you can perform a manual merge on the command line.

Step 1: From your project repository, check out a new branch and test the changes.

```bash
git checkout -b bug-fix-from-pr master
git pull https://github.com/<other-user>/repo.git bug-fix
```

Step 2: Merge the changes and update on GitHub.

```bash
git checkout master
git merge --no-ff bug-fix-from-pr
git push origin master
```
