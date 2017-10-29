# GIT Essential Training 

## Limitations
This tutorial is best suited for Unix and Linux environments. 

## Prerequisites
- Knowledge in bash scripting. 
- Unix, Linux or Windows environment. 

For Windows environment you need to install bash on your machine. One common way to do it is to install GIT on your windows machine and use GITBASH. 

## What is GIT?
GIT is a version control system (VCS) or a source code management (SCM), so it basically keep track of changes in your files. 

## Configuring GIT
### System configuration
This type of configuration is applied to every user on the computer. 

The system configuration is inside the following file:
```
/etc/gitconfig 
```
You can manually edit the above file or perform a system configuration via GIT: 
```
git config --system
```
Nothing to configure here yet.

### User configuration
These Configurations apply to a specific user on your machine.

User configuration path: 

```
~/.gitconfig
```
You can manually edit the above file or perform a user configuration via GIT: 

```
git config --global 
```
Examples of user configurations: 

```
git config --global user.name "frederic"
git config --global user.email "frederic@example.com" 
git config --global color.ui true
```

location: 
```
cd ~/
cat .gitconfig
```

### Project configurations
Configurations that are applied only to a specific project 

its inside: 
```
my_project/.git/config
```
to perform a config: 
```
git config
```

### Check your configs
```
Ex1: git config --list
Ex2: git config user.name 
```
## GIT auto-completion 
```
cd ~ 
curl -OL https://github.com/git/git/raw/master/contrib/completion/git-completion.bash
mv ~/git-completion.bash ~/.git-completion.bash
vim ~/.bashrc
```
then add the following in .bashrc (NB: on mac it might be .bash_profile)

```
#GIT AUTO-COMPLETION (ADDED BY Frederic) 
if [ -f ~/.git-completion.bash ]; then
        source ~/.git-completion.bash
fi

```

## Git Help
```
git help
```

to move page: space or "f" for forward and "b" for backwards. When done, press "q" to quit. 

To check a specific command, for instance log: 
```
git help log 
```
or 

```
man git-log
```

## Initializing a GIT repository 
```
cd repo_folder
git init
```
After initializing a repo we can see a new hidden folder created inside the directory which is responsible for GIT tracking. 
```
ls -la 

--OUTPUT--
/repo_folder/.git/
```

So consequently if we want to remove GIT from our project we simply delete that .git/ folder. 

Go to .git folder
```
cd .git/
ls -la

--OUTPUT--
HEAD
branches
config
description
hooks
info
objects
refs
```
Don't mess around these files! The only file that you might edit it manually is the config file which is for our project level config, but generally you want to use git commands to config your project level configs. 

## Perform your first commit 
You should perform your first commit in order to tell GIT to track changes.  

```
cd my-project
vim example.html (put some dummy data inside any type of file and save)
git add . 
git commit -m "Initial Commit" 
```

"git add ." tells git to add all changes that have been made to the entire project.

Worflow: make changes => add the changes => commit the changes to the repository with a message


## Commit message best practices 
- Short sinle-line summary (less then 50 charac) 
- Optionally followed by a blank line and a more complete description. And keep those additional line to less than 72 characters. 
- Write commit messages in present tense, not in the past tense. 
example: "fix bug" or "fixes bug" NOT "FIXED BUG"
- if you want to use to use bullet points to describe what happened you can use asterisks. 
- can add "ticket tracking numbers" from bugs or support requests
- can develop shorthand for your ogranization e.g: [css,jss], bugfix:
- be clear and descriptive, example : "Add missing > in project section of HTML" 

## Viewing the commit log 
```
git log 
```
limit the number of commits that are returned to us
```
git log -n 10

---OUTPUT---
output top 10 recent commits 
```
you can also output according to dates 
```
git log --since=2017-01-01
git log --until=2017-01-01
```
you can also list by author
```
git log --author="author_name"
```
you can also use grep
```
git log --grep="Commit_name" 
```

## GIT Concepts and Architecture 
GIT uses the three-tree architecture. 
1st tree: repository tree
2nd tree: staging index tree 
3rd tree: working tree

"git add file_name..." adds file(s) from working tree to staging index tree
"git commit" pushes file(s) or set of changes (can refer to 1 or more files, so they are snapshots of changes) from staging index tree to repository tree

NB: We can revert these changes and go backwards. 

We can deduce that we can make changes to ten different files in our working copy. And then we can say, all right, I am ready to make a commit, but I don't want to commit all ten of those, I just want to commit five of these as one changed set. So what I am going to do is I am going to put those on the staging index, add them to the staging index, get those five files ready to go, and as soon as I am satisfied that they are ready, now I will commit those five files in one changed set to the repository.

The other five files are still saved in my working tree, but they never got added to the staging index or to the repository. They are sitting there waiting for me to make another commit, to stage those changes and then commit them to the repository.

## HEAD pointer
Git maintains a reference variable called HEAD. And we call this variable a pointer, because its purpose is to reference, or point to, a specific commit in the repository as we make new commits the pointer is going to change or move to point to a new commit. HEAD always points to the tip of the current branch in our repository. Now this has to do with our repository, not our staging index, or our working directory, we're talking just about the repository the commits that we've actually made to the repository by checking them in.

Another way to think of it is the last state of our repository or what was last checked out, and because it's where the repository left off or the last state, you can also say that the HEAD points to the parent of the next commit or it's where commit writing is going to take place.

HEAD always points to the tip of the currently checked out branch from the repository.

## Making Changes to files
### Git Status
``` 
git status
```
Git status is going to report back to us the difference between our working directory, the staging index, and the repository. It's going to let us know, what is the status between those three different trees.

### Adding files to our GIT repository 
create 1 or more files. 
add these untracked files to the staging directory (or index)
```
git add file_name 
```

then commit 
```
git commit -m "Adding first file to project" 
```
its gonna what's in my staging index. 

if we do a git log we can view our commits in a reverse chronological order
``` 
git log 
```

to add a folder (all files and subfolders inside that folder)
```
git add folder_name/
```
nb: the * is optional : git add folder_name/* 

### Editing files
if you change a file and run a git status you will see changes that are not staged. 
So you can add these changes to the staging directory 
``` 
git add modified_file 
```
then commit those changes
```
git commit -m "new_changes" 
```
### Viewing changes with diff (between working directory and repository)
I'd like us to take a look at how we can see what changes have been made before we make a decision about whether to commit those to the repository.

```
git diff
```
git diff will compare what's in the repository (the version that HEAD is pointing at) vs what's in our working directory.

the version in the repository is the one with the minuses and what's in the new version is what has pluses 

now if we have changes to more than one file git diff will list the differences in all files. I can optionally chose to see the changes in one specific file: 
```
git diff file_name 
```
to view changes side by side: 
```
git diff --color-words file_name 
```

### Viewing only staged changes
We view the changes between the staging index and the repository. 
```
git diff --staged 
``` 
### Deleting files 
case 1: we are manually deleting a file : 
by running get status we see a deleted file 

so if we want to remove this file from the repo we need to run the following to stage the deletion: 

```
git rm file_to_delete
```
then we need to commit our deletion
```
git commit -m "message"
```

case2: let GIT delete the file
i can directly run 
```
git rm file_to_delete
```
which will do the delete for us and add the file to the staging directory. 

then i do a commit like in case 1 
``` 
git commit -m "message"
```

the difference between case 1 and case 2 is that in case 2 the file is completely deleted from the PC. In case 1 i can manually remove to trash can. 

### Moving and renaming files 
case 1: 
I can manually rename a file 
then i should run the following 

``` 
git add renamed_file 
git rm old_file 
```
automatically GIT will know that it's a rename. 

then commit that change. 

case2: let GIT rename it for us and add it to the staging index all in one step
``` 
git mv old_file new_file 
```

to move and rename a file at the same time and adding to staging directory: 
```
git mv file_to_move dest_directory/new_name_file 
```

## Undoing Changes

### Undoing working directory changes 
After making unwanted changes in the working enviroment, we want the repository version back. We want the version that Git has saved for us to be restored. It's using that version to compare when it does the diff. What we're going to do say, "Git, go back to the repository, get that version, and check it out for me and replace what I have in my working directory with it." And to do that, we use the git checkout command. You could say git checkout index.html (if the modified file for instance is index.html). 
 
In the next code, we are staying on the same branch and getting the required file (to make it look exactly like the one in the repository)
```
git checkout -- file_name.extension
```

In the next code we are only switching branches 
```
git checkout branch_name
```
I think in a lot of cases that will work. However, the thing about checkout is that it's used for more than one purpose. It's also used for working with branches. Because what checkout does is go to the repository, get the named thing that I've gave you, and make my working directory look like that. That's what it does. So if that named thing is a branch, it brings the branch down. If that named thing is the file, it brings the file down.


### Unstaging files
```
git reset HEAD <file>...
```
### Amending commits 
Here we are undoing changes in the repository itself. 

We can use the amend option with commit in order to edit our very last commit, the commit that the HEAD still points to.

after doing some changes in a file
``` 
git add file_name
```
then amend
```
git commit --amend -m "message" 
```
NB: i can directly use the last statement to change the comment of the commit. 

You can see that every time. Even if we just change the message, the dates that we've made the commit, everything changes, and so the SHA changes as well. That's why we only have the ability to amend the most recent commit, the one that HEAD points to.

### Retrieving old versions

We need to make changes to older commits, the best advice is to make new commits, commits that undo what was done in those older commits. Not only does it maintain the data integrity of Git, but then the log file also accurately reflects the changes that were made over time.

We can checkout the commit SHA hash value directly. 

```
get checkout HASH_VALUE -- file_name 
```
we can omit (-- file_name) to revert to the comit. 

When we checkout a file it puts it in the staging area. 

### Reverting a commit
```
git revert HASH_VALUE_COMMIT
```
### Using reset to undo many commits
get reset will let us move the HEAD pointer to a certain point and record and override what came after that. 

--soft: does not change staging index or working directory
```
get reset --soft HASH_VALUE_COMMIT
```
--mixed (default): changes staging index to match the repository, but does not change the working directory 
```
get reset --mixed HASH_VALUE_COMMIT
```

--hard: changes staging index and working directory to match repository 
```
get reset --hard HASH_VALUE_COMMIT
```
### Removing untracked files 
Removing files that you dont need to track and you dont need your working directory. 

testing clean: 
```
git clean -n 
```

forced clean: 
```
git clean -f
```
NB: if any file is in staging directory, it won't be removed 


## Ignoring files

### Using .gitignore files 
location: 
```
project/.gitignore
```
synthax: 
- very basic regular expressions 
- ignore all files in a directory with trailing slash "/" 
- "#" for comments 
- "!" for negation => it means NOT to ignore!! 

Create the file with vim or any other text editor and save it as ".gitignore"

```
cd project_directory
vim .gitignore
```
then add all the files or extensions that you want to ignore

Example: 

tmp.txt

*.php 

images/

.DS_Store 

*.zip

*.gz

log/*.log

log/*.log.[0-9]

assets/videos

!assets/videos/tour_*.mp4

Then commit your .gitignore file.

### Understanding what to ignore 
- compiled source code 
- packages and compressed files 
- logs and databases (files that change often)  
- operating system generated files 
- user-uploaded asssets (images, PDFs, videos) 

CHECK the following: 
[link1](https://help.github.com/articles/ignoring-files) 
[link2](https://github.com/github/gitignore) 
 
### Ignoring files globally 
- ignore files in all repositories
- settings not tracked in repository 
- user-specific instead of repository-specific (so it will only work on my machine, so we don't have to share those with other) 

create the .gitignore file: 
```
cd ~
vim .gitignore_global 
```
Examples: 
<ul>
    <li>.DS_Store</li>
    <li>.Trashes</li>
    <li>.Spotlight-V100</li> 
</ul>

then add it to gitconfig file 
```
git config --global core.excludesfile ~/.gitignore_global
```

### Ignoring tracked files 
If a file is already commited to the repository. 

```
vim project_directory/.gitignore
```
Add this already commited file name to gitignore. We see that it won't work. 

So we should tell GIT to remove and untrack this file: 
```
git rm --cached exampleFile1.extension
```
but this will completely remove the file 

If we want to keep the file in the repository for other people to download but we just want to ignore changes to that file that happen after that (example in the case of a log file, we want to have a placeholder for the log file that everyone can have but we don't necessarily want to have changes to that log file) 

So we do the following: 
```
git rm --cached exampleFile1.extension1
```
The previous command will remove the file from the staging index (not from the repository), this will cause the file to stop being tracked. It will be in the repo and in the working directory, so it will just take it out of the staging index. 

Finally do a commit. 

### Tracking empty directories 
By default, GIT does not track empty directories. That's because GIT is designed to be a FILE tracking system. 

So the trick here is to create a small tiny file in the empty directory that you wish to keep track of. Lately people by convention are naming that file .gitkeep 

Example of creating a .gitkeep file with no contents in it 
```
touch folder_to_track/.gitkeep
```
Finally you can add and commit that folder. GIT will recognize that folder. 

## Navigating the commit tree 
### Referencing commits
We will start off by introducing a new concept in Git called tree-ish. By definition a tree in GIT is the structure of files in the Git repository. It's similar to a directory in your file system. In Git, tree-ish means something that references part of the tree. It's ish because what that something is can vary widely.

Tree-ish is an important term to know, because it does show up in the Git documentation. You will be looking up how to use a command, and it will tell you that you can pass in a tree-ish as an argument to that command. Now in its simplest terms, a tree-ish is a reference to a commit because that commit then in turn references the tree, the Git repository and all the files that are in there at that point. So if you have a hard time thinking about all the things that a tree-ish can be, the simplest version is that it's just something that points out a commit.

So how can you reference a commit? The easiest way to do it is to use the SHA-1 hash, to use the entire 40 character string in order to reference the commit. Git will always know which commit we mean because each one of those 40 character strings is unique, and as a side note, if you were wondering, how Git make sure that all those are unique, it doesn't, but the odds of it not being unique are astronomical.

The other way we have seen that we can refer to a commit is using a shortened version of that hash. We don't have to have the whole thing,we can just use a portion of it, and because those numbers are so unique, Git can use that small portion and still find the object that we were looking for.

And we have also seen that we can reference a commit by using the HEAD pointer. The HEAD pointer remember always points to the commit that's at the tip of the currently checked out branch.

We can also use a branch reference. If we use a branch reference, then we are referring to the tip of the branch. Now it doesn't have to be the currently checked out branch, it can be a branch that's not checked out. 

We also can use a tag reference.

And the last way that we can refer to commits is by using any one of these methods and then referring to that object's ancestry. 
To reference to the parent commit we use the carrot symbol "^". 
Examples: 
HEAD^, ac4378f37^, master^ 

We can also use a tilda "~". So we can designate the number of generations that we want to go backwards from the referenced commit. 

<b>Examples:</b> 

HEAD~1 (NB: its the same as HEAD~)

HEAD~2 (its the same as HEAD^^)

### Exploring tree listings 
to list a tree, we use git ls-tree and that after that we pass it a treeish

Example1: 
```
git ls-tree HEAD
```
In example 1: that will point to the tip of the currently checkout branch and it will return the list of files at that point. 

Example2:
```
git ls-tree master 
```

Example 3: 
```
git ls-tree master assets/
```
Example 3 will show us all the files inside the assets directory 

Example4: 
```
git ls-tree master^ assets/
```
Example 4 will show us the assets directory in its previous state (in its previous commit) 

You can that the types of listings are either a BLOB or a Tree. A tree is a directory. We can for instance take the SHA of that tree and pass it as a treeish to git ls-tree

for instance:
```
git ls-tree 437gf78a78
``` 

### Getting more from the commit log 
```
git log --oneline
```

```
git log --oneline -3 (-4 etc...)
```
 
``` 
git log --since="2012-01-01" --until="3 days ago"
```

``` 
git log --author="frederic"
```
```
git log --grep="Reg_Expression_Example"
```
```
git log 2342hs..asc734 --oneline
```
```
git log c32da.. index.html
```
```
git log -p
```
```
git log --stat --summary
```
``` 
git log --format=oneline
git log --format=full
git log --format=fuller
git log --format=short
git log --format=raw
git log --format=email
git log --format=medium
```

```
git log --graph --online --all --decorate
```

### Viewing Commits 
```
git show TREEISH_Example
```
it will show me the changes for a single commit 

```
git show --format=oneline HEAD~3
```
### Comparing commits
We're comparing the state of the files in 2 directories (or trees). We can compare them over time. We can also compare branches

```
git diff 
```
gitt diff will return the changes that have been made between our working directory and the staging index. So it's all the things that can be put in our staging area. When add them into staging they wont show up in git diff so we should add another option to it: 
```
git diff --staged (or cached) 
```
git diff --staged will show us the difference between the staging index and the repository (or the HEAD, where the HEAD pointer is pointing). 

if we pass a SHA that references a commit to git diff it will show us the difference between our working directory and the directory at the point in time that the commit was made. 

Example:
```
git diff c0392na
```
We can also pass in a specific file only 
Example: 
```
git diff c0392na index.html
```
we can also pass a range between 2 commits SHAs
```
git diff 328nda..238ja
```
we can also add to it a file
```
git diff 328nda..238ja index.html
```
other examples:
```
git diff 328nda..HEAD^^ index.html
```
```
git diff --stat --summary 328nda..HEAD
```
```
git diff -b 328nda..HEAD (-b is the same as --ignore-space-change)
```
```
git diff -b 328nda..HEAD (-w is the same as --ignore-all-change)
```

## Branching
- In GIT branches are cheap (easy to work with). 

- Branches will let you try new ideas and test. 

- Branches can let you isolate features or sections of work. 

- Fast context switching: When we create branches we're still going to have just one working directory. All the files that we're working with will still be in that same project folder that we've been in before. But when we switch branches, Git is going to do fast context switching. It's going to take all of the files and folders that are in our working directory and make them match what's in the branch. It will swap out the two sets of changes.

### Viewing and creating branches
To view branches 
```
git branch
```
the * near the branch = currently checked out branch. 

Check the following HEAD file on your system:
```
cat .git/HEAD
ls -la .git/refs/heads
cat .git/refs/heads/master 
```

So cat .git/HEAD, and inside there what that file contains is a reference to one of the branches, because HEAD always points to the tip of a branch. So the HEAD says all right, here is the branch that I'm on now, and then we can go in that folder to find out what the actual tip is. I can do ls -la .git/refs/HEADs, let's just do that, let's not do master, and we'll see a directory listing of all the branches that are listed there.

When we add new branches this is where they show up, it adds a new reference in the HEADs folder. And if we take a look at what's in that, .git/refs/heads /master, you can see that that contains the SHA that points to a commit, that is the tip of the current branch —oneline, so there it is. So you can see that it points to this one right here. So now that we have a good foundation for what's going on with our existing branch, let's try creating a new branch. We do that with the git branch command again, but this time, we just provide the name of the new branch.

To create a branch
```
git branch new_branch_name
```

### Switching branches 

To switch (checkout) to a branch
``` 
git checkout branch_name 
```
What the checkout command does is it tells Git to go and get the latest version of the branch and to make our working directory look exactly like it. 

### Create and switch branch at the same time
```
git checkout -b new_branch_name
```
if we use this command we can create a new out of the branch that we previously checked out. It doesn't necessarily need to be the master branch. 

### Switching branches with uncommited changes 
3 options to resolve that case: 
- Discard the changes 
- Commit the changes 
- Stash the changes (put them aside and save them)

NB: if we add a file we can normally checkout without any conflict. The only conflict arises when we are facing a loss of data while swtiching branches. 

### Comparing branches 
Get the difference between the tip or HEAD (snapshot aka commit) of branch1 and the tip of branch2
```
git diff OldStatebranch1..NewStatebranch2
```
Example 2: 
```
git diff --color-words OldStatebranch1..NewStatebranch2
```
so here we are passing a treeish. So for instance we can compare any 2 treeishes :

```
git diff --color-words branch1..branch2^
```
A cool trick: Find out whether a branch completely contains another branch or not, in other words, everything in one branch has been merged to the second branch: 

```
git branch --merged
```

### Renaming branches
```
git branch -m branch_old branch_new  
```
or 

```
git branch --move branch_old branch_new  
```

### Deleting branches 
```
git branch -d branch_to_delete  
```
or

```
git branch --delete branch_to_delete 
```

NOTE: we should get off the branch that we want to delete before deleting. 

NOTE: -d will only delete the branch if its fully merged to another branch. If you want to delete that branch anyway you should use -D instead : 
```
git branch -D branch_to_delete 
```

### Configuring the command prompt to show the branch 
For Mac and Linux prerequisites: the autocompletion should be installed. 

in ~/bashrc file edit the following to : 
```
#GIT AUTO-COMPLETION (ADDED BY FREDERIC ABDOU) 
if [ -f ~/.git-completion.bash ]; then
        source ~/.git-completion.bash
        export PS1='\W$(__git_ps1 "($s)") > '
fi 
```
Alternatively you can temporarily enable that feature by cd to your project and running the same script: 
```
export PS1='\W$(__git_ps1 "($s)") > '
```
But once you close the terminal the script won't be active. 

## Merging branches 
The first step is that we want to make sure that we checkout the branch that things are being merged into, the receiver.

Example of merging changes from one branch to master branch which is the receiving branch 
```
git checkout master
git merge branch_to_merge 
```
We can make sure that the merge successfully occured: 
```
git diff master..branch_to_merge

OUTPUT: there should be no differences
```
Another way to make sure that a branch is merged into a master branch for instance is to checkout to master and then write the following: 
```
git branch --merged

OUTPUT: it will output all the branches that are merged to master. So master includes all of these branches 
```

### Fast-forward merges vs True merges 
fast-forward: 
```
git merge --ff-only branch_name
git merge --ff-no branch_name
```
Now there are a couple of options with merge that are related to the fast-forward. The first is the no-ff option so that would be git merge —no-ff and then whatever branch you were trying to merge. The no-ff option forces Git to create a merge commit anyway. It says, don't do a fast-forward, make a new commit with the commit message anyway. And the main reason you'd want to do this is if you wanted some kind of documentation of the fact that you did do this merge.

You didn't want it to just quietly do it, you wanted it to sort of make some noise in your git log. The other option you should know about is the ff-only option. Don't get those confused, no-ff says don't do a fast-forward, ff-only says do the merge only if you can do a fast-forward. If you can't do a fast- forward merge, then just abort. Don't try and do it at all just exit. So we won't do either one of those now, but those are useful options to know. All right, so now as a contrast, let's try an example of a true merge or a non-fast-forward merge.

### Merge conflicts
git marks the merge conflicts for you in your working directory files. 

How to resolve conflicts: 
- abort merge 
- resolve conflicts manually (check the file) 
- use merge tools 

### strategies to reduce merge conflicts
- keep lines short 
- keep commits small and focused 
- merge often 

## Stashing changes
The stash is a place where we can store changes temporarily without having to commit them to the repository. It's a lot like putting something into a drawer to save it for later. The stash is not part of the repository, the staging index or the working directory, it's a special fourth area in Git, separate from the others. 

And the things that we put into it aren't commits, but they're a lot like commits, they work in a very similar way. They're still a snapshot of the changes that we were in the process of making, just like a commit is. But they dont have a SHA associated with them.

```
git stash save "changed example"
```

Viewing stash changes

To view all stashes:
```
git stash list
```
NB: the stash is available all the time, even if you switch branches 

To view a specific stash: 
```
git stash show  stash@{0} 

A more elaborated: git stash show -p stash@{0}
0 is the stash number 
```
Retrieve stash changes: 
git stash apply does remove the change from the stash, it just applies it to my working directory
```
git stash apply stash@{STASH_NUMBER}
```

whereas git stash pop removes the change from the stash
```
git stash pop stash@{STASH_NUMBER}
```

Deleting stash changes: 
```
git stash drop @stash@{STASH_NUMBER} 
```
Delete all the stashes at once in the stash list: 
```
git stash clear
```

## Remotes (Github)
The remote server is actually a GIT repository. 

So generally speaking, the process that you go through when you're working with a remote, is that you'll do your commits locally, then you'll fetch the latest from the remote server, get your origin branch in sync, then merge any of the new work you did into what just came down from the server and then push the result back up to the remote server. 

### Setting a github account 
First create a repo on github. 

Then push to that repo: 
```
git remote add origin (NB: origin can be named anything you want) https://github.com/repo.git
git push -u origin master
```
### Adding a remote repository 
We now need to tell our local repository information about where it can find the remote. 

1) go to the root of your project directory 
2) check if there is any remotes (list of remotes): 
```
git remote
```
It will give us the list of aliases (names)of already created remotes. 

To view more details: 
```
git remote -v
```

3) add a remote
```
git remote add <alias> <url>
```

GIT stores these remotes in the config file of your project: 
```
cat .git/config
```

4) remove a remote 
```
git remote rm <remote_alias>
```
### Pushing a branch to a corresponding branch in the remote server
```
git push -u <alias_remote> <a_branch>
```
the -u is used for branch tracking 

to see the remote branches: 
```
git branch -r
```
to see both the remote and local branches: 
```
git branch -a 
```


### Cloning a remote repo 
```
git clone <url.git> <OPTIONAL_rename_repo>
``` 
you can clone a specified branch 
```
git clone -b <branchName> <url.git> <OPTIONAL_rename_repo>
```
### Tracking remote branches 
If we don't do git push with the -u option, it does not track any remote branch. All it does is push our code up there, and that's it. It doesn't keep any kind of reference that this is the branch there we're going to be working with in the future. The -u option says push it up there, and also make a note of the fact because we're going to be coming back and working with this branch frequently.

When we did a git clone to create our lynda_ version, it does track the remote branch, and we can see that tracking here, git/config. You can see that our branch master is set up to track the refs/heads/master that's on origin.

if you ever end up with a branch that's not tracking, and you want to make it tracking, then you have three choices. Either you can come in and add change it manually in the .git/config file, or you can use the git config commands. It's git config branch and then whatever the branch name is. In this case, it would be non_tracking remote and then the name of the remote, origin, and then you would do the same thing for the option for merge refs/heads/master.

```
git config branch.BRANCH_NAME.remote REMOTE_ALIAS
git config branch.BRANCH_NAME.merge refs/heads/master 
```
```
git branch --set-upstream BRANCH_NAME REMOTE_NAME/BRANCH_NAME
```

### Pushing changes to a remote repository 
```
git push ALIAS_REMOTE BRANCH_NAME
```
we can simply say 
```
git push
```
if it's already a tracking branch


### Fetching changes from a remot repository 
Remember a fetch is what synchronizes origin/ master with whatever is on the remote repository.

Origin/master doesn't automatically reflect what's on the remote repository, we have to tell Git that we want it to do a sync between the two. 

```
git fetch ALIAS_REMOTE
```
```
git log BRANCH_NAME
```

### Merging in fetched changes 
```
git merge origin/master
```

when we do a merge, we are merging with origin/master.

Our local version, that's where we are merging in, we are not going back up to GitHub to see what's there. So when we do a merge, we always want to make sure we do a fetch first. Fetch, then merge.
 
### Checking out remote branches
remote branches are exactly like regular branches with one exception, and that's that we can't check them out. That makes sense because Git stays in control of that remote branch so it can make sure it always stays in sync with what's in the remote repository. It doesn't want us getting in the way.

But since it is just like every other branch, we can create a branch from it that we can then work with

After that we can tell it where we want the new branch to come from, the starting point of this branch. Now in the past, we just used the default for that which is HEAD, which points to the tip of the current branch master. But you can specify other things here. You can specify a particular commit or we can specify origin/BRANCH_NAME

```
git branch NEW_BRANCH origin/BRANCH_NAME
```

### Deleting a remote branch 
```
git push origin :Branch_Name
```
or 
``` 
git push origin --delete branch_name
```

### Collaboration Workflow Example
User1: 
```
git checkout master
git fetch 
git merge origin/master
git checkout -b feedback_form 
git add feedback.html
git commit -m "Add customer feedback form"
git fetch 
git push -u origin feedback_form 
```

User2: 
```
git checkout master
git fetch 
git branch -r
git merge origin/master 
git checkout -b feedback_form origin/feedback_form 
git log
git show dasf374682 
git commit -am "Add tour selector to feedback form"
git fetch 
git push 
```

User1: 
```
git fetch 
git log -p feedback_form..origin/feedback_form
git merge origin/feedback_form 
git checkout master
git fetch
git merge origin/master
git merge feedback_form (or origin/feedback_form)
git push 
```

## Tools and Next Steps
### Setting up aliases for common commands 
```
git config --global alias.st "status"
git config --global alias.logg "log --graph --decorate --oneline --abbrev-commit --all"
```
### Using SSH keys for remote login 
1st method: setup password caching in a keychain(check github documentation) ONLY WORKS ON A MAC
2nd method: use ssh keys (check github documentation) 

### Exploring GUIs
- gitweb : https://git-scm.com/docs/gitweb
- gitx, github, sourcetree, tower, smartgit, gitbox 

### GIT hosting
GIT hosting companies: 
- github
- bitbucket 
- gitorious 

GIT self hosting: 
- gitlab
- gitolite 
