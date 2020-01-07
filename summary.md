# Summary

## Preface

Recently I learnt git and markdown. This document is a summary of what I learnt. I want to practice markdown language and review what I learnt about git by writing this document. I will keep this document updated when I learn more about git and markdown. 
![study hard!](https://github.com/QianleLi/Markdown/image/study_hard.jpg)

## Git Basic

**There are three spaces in local, which is repository, index and workspace. Files can be added from workspace to index, commited from index to repository and checked out from repository to workspace.**
- Create a new repository  
`git init`  
`git clone [url]`
- add, remove and rename documents
```
git add [file1] [file2]
git add .
git rm [file1] [file2]
git mv [file-origin] [file-renamed]
```
- commit documents
`git commit -m [message]`  
if no new document is added, just update
`git commit -am [message]`
- check the info
```
git status
git log
git show [hash code]
```

**A remote repository can be cloned to be a local repository, it can also be pulled to update a local repository. A local repository can be pushed to be a remote repository.**
- update the remote/local repository
```
git remote add [shortname] [url]
git push [shortname] [branch]
git pull [shortname] [branch]
```

## Git Advance

- .gitignorefile
This file record exact documents or exact type of files that git ignores. So that `git status` does not show these files as not updated.   
In a .gitignore file, one line represents a file or one type of file that you want to ignore.  
For example:  
```
/image/     #ignore the directory
my_file     #ignore the file
 *.zip       #ignore all .zip files
!*.zip      #do not ignore all .zip files
```
If you have ignored a file or type of files in .gitignore, but you want to add them. Do this:  
`git add -f [filename]`  
If you want to check which line of .gitignore claim the rule that make one document be ignored, do this:  
`git check-ignore -v [filename]`  

- alias
By using alias you can make your work much faster.  
You can setup one alias by this:  
`git config --global alias.ci commit #You can input 'ci' instead of 'commit'`  
Or you can check or setup all alias in ~/.gitconfig file, you can see a section named alias and rules like this:  
```
    ci = commit
	st = status
	ad = add .
	br = branch -v
	hi = log --pretty=format: '%h %ad | %s%d [%an]' --graph --date=short
```

- Setup SSH 

*Create SSH key*  
`ssh-Keygen -t rsa -C "your-email-address"`  
*Find the key in `~/.ssh/id_rsa.pub` and copy the key, go to the **SSH and GPG keys** session in settings of github, click **New SSH key** and paste the key, done*  

- More git commands
```
git        #give a list of common sub-commands
git help -a   #give all sub-commands
git blame [filename]  #give the modify history of the file
git blame -L 100,110 [filename]  #give the 100~110 line(which is 10 lines) of modify history of the file
git clean -n  #give a list of untracked files
git clean -f  #delete those untracked files
git clean -xf  #git will delete all untracked files
git add -p    #you can add one file at several different times, you should search for more info, maybe I will update detail someday
```

- Commit messages
  * Each commit should based on one small feat, bug fix or improvement.
  * All programs of a unit test should be commit at the same time.
  * Programs with grammer issues should not be committed.
  * Non-related programs should not be committed together.
  * Suggested Format of Messages:
```
<type>(<scope>):<subject>     #required
   <blank line>
<body>                        #optional
   <blank line>
<footer>                      #optional
```
  * Type include: feat, fix, docs, style, refactor, test, chore
  * Subject include: change, modify, update
  * For more info you can check [I am sorry this is in Chinese](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)

- Check info and history
```
git show HEAD ~2    #Check two commits ahead
git show [hash code]
git log [filename]
git log -5    #Check all 5 history ahead
git log --oneline     #each history only show in oneline
git log --grep [keyword]   #only check keyword related history
git diff    #check the difference between workspace and index
git diff --cashed   #between index and last version that committed
git diff [hashcode1] [hashcode2]  #between two versions
git diff --cashed [hashcode]
git diff --cashed HEAD
```
- Reset
```
git reset HEAD   #withdraw the file from index to workspace
git reset HEAD --soft #from local repository to index
git reset HEAD --hard #back to last status
git push -f   #After use reset command, push the repository to the remote, strongly NOT recommanded
git commit --amend -m "message"  #make change to the last commit
git rebase -i HEAD~3   #use rabase order to change the past three commit history, you should search for more info.
```

**Notice that HEAD can be replaced by any [hashcode].**  
*If you cannot solve the problem occurs during rebasing, you can always use `git rebase --abort` to give up.*

- Tag
You can tag important commiments to make it easier for people to find it.
```
git tag [tagname]  #tag the last commitment
git tag [tagname] -m "message" #tag and add a messageto the tag
git tag [tagname] HEAD~4  #tag the exact 4th commitment ahead
git tag  #list all tag
git tag -d [tagname]  #delete the tag
git push [shortname] [tagname] #push the tag to the remote repository
```

- Git branch
Branches are created to help parallel development. 
```
git branch [branchname]   #create a branch
git checkout [branchname]  #change the working branch
git checkout -b [branchname]   #create and change to the branch
git branch -m [oldname] [newname]  #change branch name
```
When two branches merge, default method will use fast forward, you may search for more info.
```
git merge [branchname]  #merge to another branch
git merge [branchname] --no-ff   #merge without fast forward
```
