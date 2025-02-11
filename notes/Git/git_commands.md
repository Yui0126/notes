

## Git branch

Fetch remote branch
```
git fetch origin <branch name>
```


Create a local branch and switch to the branch

```
git checkout -b <branch name> 
```

Set an upstream branch 
```
git push -u origin <branch name>
```

Delete local branch
```
git branch --delete <branchname>
```
To force delete,
```
git branch -D <branchname>
```

When you need to pull from main and merge it into your local branch

first go to main and fetch latest changes
```
git checkout main
git fetch
git pull
```
then checkout to local branch you want to work with
```
git checkout <branchname>
```
then merge changes into your branch
```
git merge main
```
then push the changes into your remote branchname if necessary.
```
git push
```