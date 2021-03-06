#GitHub cheat sheet


Remote repository holds files on GitHub server.

Local repository consists of the Working Directory, the Staging Area and the Git Directory.



####clone the remote repository and set the URL
```
git clone git://github.com/pyer/[repo]
git remote set-url origin git@github.com:pyer/[repo]
```

####show remote repository and URL
```
git remote -v
```

####show local repository status
```
git status
```

####show commit history with file names
```
git log --name-status --oneline
```

####show commit history of a single file
```
git log --name-status --oneline -- [file_name]
```

####show a single file from  specific revision
```
git show [commit_id]:[file_name]
```

####show differences between working directory and staging area
```
git diff
```

####show differences between staging area and last commit
```
git diff --staged
```

####add modified file to staging area
```
git add [file]
```

####replace modified file by last commited one
```
git checkout [file]
```

####commit changes to Git directory
```
git commit -m "+ comment"
```

####add staging area changes to the last commit
```
git commit --amend
```

####update remote repository
```
git push
```

####update local repository
```
git pull
```
