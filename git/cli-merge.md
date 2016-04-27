# Merge from CLI
1. `git checkout master`
2. `git fetch`
3. `git merge --ff-only origin/master`
4. `git checkout BRANCH`
5. `git rebase master`
6. If conflicts, resolve and git rebase --continue. Do not push.
7. `git push origin/BRANCH -f`
8. `git checkout master`
9. `git merge --no-ff BRANCH`
10. `git push origin/master`
