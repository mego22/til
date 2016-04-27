# Cherry pick
## cherry pick from master to branch
```bash
git checkout master
git fetch; git merge --ff-only origin/master
git checkout BRANCH
git cherry-pick -m 1 <MR>
```
