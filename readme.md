# ReadMe file for Learning Git and Github 

## Create a repository 
1. cd to folder that you wish to create as a git repository 
 
2. Initialize the folder as an empty git repo
```
git init
```
this directory contains now a hidden .git folder that lets GIT track the repo. 

3. You can view the hidden .git folder: 
```bash
ls -la
```
4. You can check the status of your repo and files 
```
git status 
```

## Add files to the staging environment to store the state of files
1. You can add one file to the staging environment
```
git add fileName.extension 
```
Check the status of your repo (git status)

2. You can add all the files inside your repo folder
``` 
git add .
```
3. You can unstage a file
```
git rm --cached <fileName>
```
Or you can unstage all files recursively
```
git rm --cached -r .
```

## Committing files 
1. Commit all staged files. The -m is used to add a description to your commit 
```
git commit -m "revision one" 
```





