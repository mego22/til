# Sqaushing commit messages
This was stolen from [Stephen Ball](http://rakeroutes.com/blog/deliberate-git/) :+1:

1. Using git-log, copy commit hash from the last commit previous to your work beginning; `git log`
2. Rebas branch starting at the hash from step 1; `git rebase -i HASH`
3. Change first pick to reword or r.
4. Change the rest of the picks to fix or f so they get squashed; I tend to copy the list of commits to reference when writing my update
5. Save the changes.
6. Update the title appropriate commit title.
7. Write a good paragraph/sentence explaining the work that was done. Someone should be able to know what happened in this commit and how it affects the code base.
8. Save changes.
9. Do a git force push up to your branch; `git push -f origin/<BRANCH>`
10. Check branch your git webUI to make sure all is well.
