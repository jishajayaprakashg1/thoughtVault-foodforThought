# Database : Replication v/s Sharding
- To scale Reads go for Replication: here one DB will be primary and rest will be a replica of this primary and all will have the same data.
Easier to implement and revert.
- To scale Writes do sharding: DB is split into multiple small DBs to distribute the load, storage, requests.
Usually sharding is combined with replaction.

# Docker v/s Kubernetes
- Earlier (before docker) : Developer writes the code, installs the dependecnies, tests it,
  prepares deployment artifacts, install all dependencies and requirements with same versions on another server where you want to deploy your application.
- Now (after docker) : dev writes the code, builds a docker image and deploys it as a container.

The application developed in your system will work fine, when you try to run on a different system errors might occur as the env of both systems are different,
you can put your application, configs and all related dependencies in a container,
and run that container in different systems. This is called containerisation.
Docker is used for it.

Docker image is created in docker, it contains the application along with it's, libraries, configs etc.
when the image is run, container starts in which the application runs.

To handle multiple requests, multiple containers will be required which have to be managed, scaled and recover, which is done by kubernetes.
Kubernetes is a container orchestrator.

# CI-CD
Continuous Integration :
- developer pushes the code, pipeline starts to execute, code is build ( is the process of converting human-readable source code (written in languages like 
TypeScript, Java, or C++) into an executable, optimized, or machine-readable format that a computer or runtime environment can actually run.)
- Then the unit/integrations tests are run, broken code must not be promoted, hence, if the tests fail, pipeline fails.
- If tests pass then application is packaged and docker image is created which is stored in the container resgistry.

Continuous Delivery: Sanity is done on staging env(prod like env) and code is deployed into production

The flow: 
- code push
- build
- test
- package
- registry
- staging
- production

# GIT : Global Information Tracker: 
- GIT : is a version control system that tracks your file.
- Online platform like GITHUB/GITLAB is used for collaboration and storing code on cloud.

* Commands to push changes to empty repo in GITHUB, First log in to the GITHUB repo and create an empty repository.

Go to VS code:
git init
git config --global user.name ""
git config --global user.email  ""
git add .
git commit -m "initial commit"
git remote add origin <GitHub project url>
git push -u origin master

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

git restore file.txt  (to discard changes made to file or maintain the old version of the file)

gitignore.io (to get templates)
.gitignore (will keep the project clean)

reset moves my branch to previous commit
git reset --soft HEAD~1   (move the branch and stage the changes)
git reset --mixed HEAD~1  (move the branch and unstage the changes)
git reset --hard HEAD~1   (move the branch and discard the changes)


SSH: Secure Shell Key :  are two files one has private key and other has public key residing in the local system.
private key : authorises you to push and pull code
public key : authenticates with GITHUB

PAT: Personal Access Token : create for tools that need authentication

Merge : combine changes of your branch with another, basically combines histories
Rebase : add your branch commits on top of another branch commits

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





