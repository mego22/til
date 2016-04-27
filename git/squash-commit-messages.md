# Sqaushing commit messages
This was stolen from [Stephen Ball](http://rakeroutes.com/blog/deliberate-git/) :+1:

1. git log -> copy commit hash from the last commit previous to your work beginning
2. git rebase -i HASH
3. Change first pick to reword or r
4. Change the rest of the picks to fix or f so they get squashed; I tend to copy the list of commits to reference when writing my update
5. Save the changes
6. Change the top line to an appropriate commit title
7. Write a good paragraph/sentence explaining the work that was done
8. Save changes
9. Do a git force push up to your branch
10. Check branch to make sure all is well
