# ReadMe file for Learning Git and Github 
Author: [Frederic Abdou](http://fredericabdou.com)

Learn how to write md files: 
[link1](https://guides.github.com/features/mastering-markdown/)
[link2](https://help.github.com/articles/basic-writing-and-formatting-syntax/#quoting-code)
[link3](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
[link4](https://daringfireball.net/projects/markdown/syntax)


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
5. Before adding files to the staging environment, you can discard any changes made to these files beforehand
```
git checkout --<file> 
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
or
```
git add --all
```

3. You can delete a file from staging 
```
git rm --cached <fileName>
```
Or you can unstage all files recursively
```
git rm --cached -r .
```
4. You can completely unstage a file
``` 
git reset HEAD <file> 
```
Or you can unstage all files recursively
```
git reset HEAD .
```

## Committing files 
1. Commit all staged files. The -m is used to add a comment to your commit. Whe can get back to this commit point in time later on. 
```
git commit -m "revision one" 
```
2. Check your commits log. 
```
git log
```

## Deletig files

1. Run git status and make sure that everything is clean
2. Method 1: 

    2.1. Manually delete the file

    2.2. You can checkout the file to revert it back 

    2.3. Alternatively you can add the deleted file into the staging environment (git add). You can undo the staging with git reset HEAD

    2.4. Finally you can commit your staging 

3. Method 2:

    3.1. You can directly delete the file and move it directly to staging by using the following command: (we are combining here the manual deletion and the manual adding to stage environment)
    ```
    git rm <file> 
    ```
    Alternatively you can delete all files in the folder with: 
    ```
    git rm .
    ```
    
    3.2. You can undo the staging with git reset HEAD. You can checkout the file to revert it back. 
   
    3.3. Finally you can commit your staging 



## Managing your log
1. Check all of your commits in the log.
```
git log
```
2. You can go to a desired commit in time. Notice if you go to a previous commit, you will enter a detached head state, which is by default a branch created by git. In this state you will only see commits up to your selected commit. You can do experimental changes and mess around with your project etc., and then you can go back to your original set of commits without messing with anything else. Think of it as an alternate reality that starts at the commit that you checkout. 
```
git checkout <commit-hash-value>
```
you can see that now you have the master branch and the head detached branch 
```
git branch
```

3. You can retain what you're doing in the death head state area as another branch, after modifying it and playing around
```
git checkout -b <new-branch-name>
```
Alternatively you can ignore all of the changes and switch back to the master branch
```
git checkout master 
```
if you wish in the future to retain your last modified head detached branch, you can save the first part of your hash commit, and then create another branch refering to the head detached branch
```
git branch <new-branch-name> <first-hash-value-of-commit>
```

## Controlling state with branches 

1. create a new branch
```
git branch <branch_name> 
```
2. list all the branches
``` 
git branch
```
3. Switch to a branch
``` 
git checkout <branch-name>
```
## Merging branches

The following code will merge an external branch to the branch that i am currently in 
```
git merge <external_branch_name>
``` 
## Change name of the branch
```
git branch -m <orig_branch_name> <new_branch_name>
```

## Remove a branch 
```
git branch -D <branch_name> 
```
## Github 

1. clone a github repo 
```
git clone github-url.git
```

2. get to a certain branch of the cloned repo: 

First, check all the downloaded branches (the ones in red are not visible. Only the master branch is)
```
git branch -a
```

Then after opting for the desired branch, pull that branch and name it and put inside a folder that you also name
```
git checkout -b name-of-branch-to-pullOut origin/new-folder-name-for-branch
```
3. Get all the branches at once from the github repo 
First create a directory for the repo 
```
mkdir repo_name
```

Then cd to that directory. 
Then make a mirror of that repo. In the next code, the space .git after the url means that we are copying the invisible git folder that keeps track of everything of the project on github:
``` 
git clone --mirror github-url.git .git
```
Then, we should switch that bare repo that we just created to a regular repo. So we should the following command still inside our created repo folder 
```
git config --bool core.bare false
```

Then finally, we should do a hard reset that grabs everything inside that folder and create all the branches and make it look like a normal repository. 

``` 
git reset --hard 
```

4. Download directly a desired branch from a github repo 
```
git clone -b branch_name repo_url.git
```
If we basically dont want the downloaded project as a github repo, we can simply delete the .git folder
```
rm -dfr .git
```

