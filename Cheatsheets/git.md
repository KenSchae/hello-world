# Git Basics
 

## Configuration

```
git config --global diff.tool vscode
git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"
git config --global -e   /* May have to manually add LOCAL and REMOTE */
```
Content of .gitconfig file
```git 
[core]
	editor = code --wait
	autocrlf = true
[user]
	name = Ken Schaefer
	email = kenschae@outlook.com
[diff]
	tool = vscode
[difftool "vscode"]
	cmd = "code --wait --diff $LOCAL $REMOTE"
```

## Create a project
```
git init
``` 
The .git folder contains the repo
Removing this folder removes git

## Operations
Working Dir -> Staging Area -> Repo

Add files to the staging area
```
git add file2 file2
git add *.txt
git add .                       /*recursively add all files*/
```
Removing files from repo
```
git rm {filename}
```

Remove files from staging only "Unstaging". This will take the file out of staging but leave it in the code area.
```
git restore --staged {filename}
```

Commit files into the repo
```
git commit -m "documentation"
git commit                      /* Will open editor for long description */
```

Going from dev to staging to repo in one step
```
git commit -am "documentation"
```

Restoring files
```
git restore -options {filename}
```

## Administration
```
git status
```
Review code in staging before a commit
```
git diff --staged
git difftool --staged           /* launches configured tool */
```
View commit history
```
git log
git log --oneline               /* short list of commits */
git log --oneline --reverse     /* reverse order */
```

## Ignoring files
Create a file called .gitignore
- Enter list of files or folders to not include in repo
- Use # for comments in this file
- Add and commit the .gitignore file

If you place something in gitignore AFTER you have put it in the repo, adding it to gitignore will not remove it from the repo.

In this situation you need to remove the file/folder from the staging area. 
```
git rm --cached -r {name of file or folder}
```

## Clone a repo from the command line
Note: make sure you are one folder above where you want the repo
$ sudo git clone https://github.com/ehrisai/{​​​​​repositoryname}​​​​​.git
Use SSH to connect to repo
 
## Connect to your Git repos with SSH
https://docs.microsoft.com/en-us/azure/devops/repos/git/use-ssh-keys-to-authenticate?view=azure-devops 