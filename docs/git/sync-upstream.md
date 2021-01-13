# Sync Upstream Repository

Setup an upstream repository:

```bash
git remote add upstream https://github.com/otheruser/repo.git
```

Fetch updates from upstream:

```bash
git fetch upstream
# or fetch all
git fetch --all
```

Sync local `master` branch with upstream `master` branch.

```bash
git checkout master
git merge upstream/master
```
