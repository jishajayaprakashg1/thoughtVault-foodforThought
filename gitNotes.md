************************************************************************************************************************************

# GIT : Global Information Tracker: 
- GIT : is a version control system that tracks your file.
- Online platform like GITHUB/GITLAB is used for collaboration and storing code on cloud.
  
************************************************************************************************************************************
### Steps
- Step1: Install GIT
  ```
  * Download GIT from official website: https://gitforwindows.org/
  * can also use **brew install git** for MAC
  ```
- Step2: Open a new empty folder in VSCode. Initialise GIT to make it a GIT repository so that the files in it will be tracked.
  ```
  git init
  ```
- Step3: Configure GIT and tell GIT who you are
   Configurations:
    - Local ( configurations applicable only to the repository )
    - Global ( configurations applicable at the user's OS level )
    - System ( configurations applicable across different machines )

  ```
  git config --global user.name ""
  git config --global user.email  ""
  ```
### If you want to rename the default branch
  ```
  //Renames your current Git branch to main
  git branch -m main

  //If you want to rename a specific branch:
  git branch -m old-branch-name main
  ```

 - Step4: To check the changes made in the repo
```
git status
```

### GIT development environment sections:
_3 main areas: working directory (has all the project folders along with the git folder, here is where the user, adds, modifies or removes files), 
staging area(contains info of what will go in the next commit to the local repository) 
and the local repository (contains metadata and object database for the project)._

- Step5: Move the untracked files from working directory to staging area
  ```
  git add .
  OR
  git add fileName
  ```

- Step6: Move files from staging area to the local repository
  ```
  git commit -m  "message"
  ```

  to view the commit
  ```
  git log
  OR
  git log --oneline
  ```
  _what happens ewhen we make a commit?
  ```
  Commit Object
  Checksum: daa26

  points to
  Tree Object
  Checksum: caa26

  points to both files, where blob is file content
  file1 blob           fil21 blob
  Checksum: aaa26      Checksum: baa26
  ```

- Step7: Move the files from local repository to remote repository
  Create a remote repository in GITHUB for example. Copy HTTPS URL.
  You can also copy the SSH URL
  ```
  git remote add origin remoteRepositoryURL

  There is no branch in remote repo that corresponds to the local repo branch, so the command git push will fail, use below command:
  git push --set-upstream origin main
  OR
  git push -u origin main
  ```

- Step8: SSH: Secure Shell Key :  are two files one has private key and other has public key residing in the local system.
private key : authorises you to push and pull code
public key : authenticates with GITHUB

PAT: Personal Access Token : create for tools that need authentication

Suppose you want to use SSH protocol for transfer of data to and from remote repository, you will need a public/private key pair
  Create new SSH key
  ```
  ssh-keygen -t ed25519 -C "your_email@example.com"
  ```
  Save the private and public keys that have been generated.
  to copy the public key use below command for mac machine:
  ```
  pbcopy < ~/.ssh/id_ed25519.pub
  ```
  Go to the GITHUB account--> Settings --> (Account Setting) --> SSH and GPG keys, Add New SSH Key. Now the SSH key is linked to the GITHUB account and it can be used to transfer data from local to remote.

- Step9: For collaboration, team mate must have GIT installed in their system, then the repo can be cloned.
  ```
  // to view the configurations
  git config --list
  ```
  CLONE the project
  ```
  //copy either HTTPS or SSH URL, this will be the remoteRepositoryURL
  git clone remoteRepositoryURL 
  ```
  _Team mate can proceed with moving files from working directory to staging area to local repository
  If any file has to be ignored on push, add the fileName in the .gitignore file._

  If you forgot what changes were done to the file, To view the changes done in the working directory use command:
  ```
  //before staging the changes
  git diff

  //after staging the changes
  git diff --staged
  ```
  
  _Note: if command is git commit
  and default editor is VIM
  Press **i** to enter edit mode
  Type the commit message
  Press: **esc:wq** to write and quit_

  git log    _to view all the commits_
  git push    _all commits will be pushed to remote repo_

### Lifecycle of status of files in GIT
- Stage1: create a file in working directory, it is : **untracked**
- Stage2: Move it to staging area: it becomes: **staged**
- When we make a commit the staged file is stored in a snapshot and it becomes: **unmodified**
- When we edit this unmodified file it becomes: **modified**
- files can be : untracked or tracked
- tracked files can be : unmodified, modified or staged

### Now if person A has made changes to the local repo while person B has pushed new changes to main
Person A: has done changes to files, then staged and committed it, while doing push it fails so now run
```
git pull --rebase
```
post this git push will succeed

### Branching in GIT
In the above case both team members had write access to remote main branch it is called trunk based development.
All team members must not be provided write access to the main it can mess up the main branch.

 _what happens ewhen we make a commit?
  ```
  Commit Object
  Checksum: daa26

  points to
  Tree Object
  Checksum: caa26

  points to both files, where blob is file content
  file1 blob           fil21 blob
  Checksum: aaa26      Checksum: baa26
  ```

_Commits will point to it's previous commits_ : C1 <-- C2 <-- C3

_Branches are pointers to commits which we can move around._
```
git branch
OR
git branch --list

to view the commits on this branch
git log
```

_to create a new branch_
```
git branch -b branchName
```
           
            branchName
               |
               |
C1 <-- C2 <-- C3
              
              |
              main
              
_Now how does GIT know which branch we are on?_ using a pointer called : HEAD : which points to the current branch

             HEAD
               |
          branchName
               |
C1 <-- C2 <-- C3
              
               |
              main

_to switch branch_
```
git checkout branchNAme
OR
git switch branchNAme
```

### stashing
_To save the changes made in the working directory_
```
git stash

git shash list
```

_Currently person A is working on branchName, person A wants to create a newBranch, for this HEAD has to move from branchName to main to newBranch_
```
git checkout main
git branch newBranch
git checkout newBranch
```
_Make changes to files_
```
git status
git diff
git add .
git commit -m "message"
git push -u origin newBranch
```
_Changes are pushed to the remote newBranch, this needs to be merged to main_
- For this create a PR. Go to GITHUB repo, Click on Code in GITHUB. Select newBranch, Click on Pull request.
- Select a reviewer, add description, add a reviewer and click on create pull request.
- Reviewer and add comments and ask to modify the file or APPROVE it
- It can then be merged with 
```
git checkout main
git pull
```

### Reapplying stashed commits
```
git checkout branchName

git stash list

git stash pop ( removes the topmost stash from list and applies it to working tree)
OR
git stash apply (applies the topmost stash to the working tree but does not delete it from the list)
OT
git stash pop --index
```

### Merging, rebasing and cherry-picking

- Merge : combine changes of your branch with another, basically combines histories.
- Rebase : add your branch commits on top of another branch commits, hence linear history is maintained but don't do it if on the same 
 branch many developers are working.

```
Before:
       D ── E   feature
      /
A ── B ── C     main


git switch main
git merge feature
       D ── E
      /       \
A ── B ── C ── M


git switch feature
git rebase main
A ── B ── C ── D' ── E'

Since, new commits are created, these commits will not be present in remote hence git push will throw error, use command:
git push --force

but in case local snapshot gets pushed to remote even if remote repo has changes from other collaborators so use, command
git push --force-with-lease
```

### Fast forward merge
```
//this will show the commits present on main which are missing on devBranch:
git log devBranch..main


          main
          | 
A ── B ── C 
     |
     D
     |
    Head

In Fast forward merge :as it is linear path from tip of the current branch to target branch, GIT simply moves the pointer ahead.

         main
          | 
A ── B ── C
          |
          D
          |
        Head
```

### Cherry-picking
branches: testBranchA with two commits, testBranchB, need to move one commit from testBranchA to testBranchB
```
git checkout testBranchB
git log testBranchB..testBranchA
copy the required commitId

git cherry-pick commitId
```
cherry-pick creates a duplicate commit
To deploy a hot fix we can go for cherry-pick.

### Merge conflicts
_Merge conflict occurs when same file or same lines of code are modified in main and dev branch
GIT will not understand which changes have to be kept, hence human intervention is required._

### Amend
_Say a new file is added then you do git add, git commit. Then you modify an existing file and do git add, git commit.
In this case two commits will be created but you want only one commit with both changes. So instead of git commit use command:
```
git commit --amend
```

### Removing changes from staging area and working directory
_To discard changes made to file or maintain the old version of the file_

_To move file from staging area to working directory_
```
git restore --staged fileName
```

_To move file from working directory_
```
git restore fileName
```

### reset command
_reset moves my branch to previous commit_

Supports multiple modes:
git reset --soft HEAD~1   (move the branch and stage the changes)
git reset --mixed HEAD~1  OR git reset HEAD~1   (move the branch and unstage the changes)
git reset --hard HEAD~1   (move the branch and discard the changes)

### reverting commits
```
git log

git revert commitId
A new commit will be created after this

git push
```

### GIT workflows
- Centralised workflow : there is a shared repository, multiple contributors have access to read and write from it.
- Integration manager workflow : There is a Blessed repository to which the integration manager has access.
  Every contributor will have their own copy of the blessed repository.
  They can read from blessed repo but not write into it.
  Contributor will write to their own public repo which are forks of the blessed repository.
  Integration manager pulls from forks and pushes to blessed repository.
- Dictator and Lieutenants: it has a dictator and multiple lieutenants.
  lieutenants pull from contributors public repo, dictator pulls form lieutenants and pushes to the blessed repo.
************************************************************************************************************************************

git show (show all the history)

git branch
git branch -d branchName (deletes from the local)
git push --delete origin branchName (deletes from the remote)


Older multi purpose command : checkout
git checkout main (switch to main branch)
git checkout -b feature (create and switch to new branch called feature)
git checkout -- file.txt  (restore file)

Newer commands focussing on branch : switch
git switch main
git switch -c feature


gitignore.io (to get templates)
.gitignore (will keep the project clean)



************************************************************************************************************************************


