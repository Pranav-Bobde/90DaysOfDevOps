##Basic

###Check Files Modified
-git status

###Add
-git add <file-name> 
-git add .

###Commit
-git commit -m “commit message”
-git commit -am “commit message”

git log

###Reset

-git reset <file-name>

-git reset HEAD~1

-git reset —hard HEAD~1

-git reset <commit-hash>

###Push
-git push origin main
-git push -u origin main

###Pull 

-git pull origin main
-git pull -u origin main

###Remote
-git remote -v
-git remote add <remote-name> <remote-url>

###Branch

-git branch

-git checkout -b <branch-name>

-git checkout <branch-name>

###Merge
-git merge <branch-name>

###Abort

-git merge abort

-git rebase abort

###Reflog

-git reflog

-git branch <branch-name> <hash-code> 
-> generates a branch with the state of the head’s hash code
