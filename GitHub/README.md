#GitHub cheat sheet


Remote repository holds files on GitHub server.

Local repository consists of the Working Directory, the Staging Area and the Git Directory.



####clone the remote repository and set the URL
```
git clone git://github.com/pyer/[repo]
git remote set-url origin git@github.com:pyer/[repo]
```

####show local repository status
```
git status
```

####show commit logs with file names
```
git log --name-status --oneline
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

####update remote repository
```
git push
```

####update local repository
```
git pull
```
