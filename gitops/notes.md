# Git crash course

## env setup
connection to the servers:  
* for odd numbered student names: **```ssh <username>@94.252.36.233 -p 2201```**  
* for even numbered student names: **```ssh <username>@94.252.36.233 -p 2202```**  

* [x] student1
* [x] student2
* [x] student3
* [x] student4
* [x] student5
* [ ] student6
* [ ] student7

## curated list of resources
* [Git immersion](https://gitimmersion.com/)
* [Git SCM](http://git-scm.com/doc) <-- part of the 5% of websites not in https 😨

## CRASH COURSE

### Intro

1. Linus,again !  
   At the beginning, Git was for Linux kernel devs ...  
   very geek, then ...  
2. First goal: version control (history tracking)  
   version = series of changes  
   * importance of atomicity of the changes  
   * within the version, there are data and metadata  
   * the history is not necessary linear  
   
3. Second goal: Collaboration
4. Third goal: DevOps

### use git locally

1. create a directory *studentx_repo1* in your home folder
2. inside that directory, run: ```git init```
3. with *ls -a*, notice a .git subdirectory has been created ; it contains your history  
4. ```touch test.py```
5. edit test.py with the following simple content:  
   >print('Hello World!)
6. ```git status```
6. ```git add test.py```
7. ```git status```
8. ```git commit -m 'init'```  
   (here, git will complain, follow the instructions on the screen to set a user and an email, you can set it to whatever values)  
10. ```git status``` 
11. For curious --> Noticed the hash just after the commit message ? check again the .git folder  
12. ```git log```
13. From now on, if we modify test.py, git will notice it:  
    change the content by adding another line of code:   
    >name=input('Whats ur name, Sir?)  
14. `git status`
15. ```git commit -m 'some more content' -a```
16. ```git log --oneline``` 
17. One of the advantages of using an VCS is the ability to revert to a previous version of a file:  
    Lets say our file changes:  
    >print('Hello Pythonists!')
    
    and we dont want that change anymore, in fact we want to go back to the latest version:  
    `git diff test.py`   
    `git checkout .`  
18. Tags 
    ```
    git log --oneline
    git tag rust_version 987a1d4
    git log --oneline
    ```
    you can remove with `git tag -d ... `
19. Now suppose we want to work on a feature separately  
    `git checkout -b dev`   
    `git branch`   
    Do quite some changes, add files, etc ...
20. Dev is done. Question: how do you sync your changes with the main branch ?  
    Two choices:  
    * **rebase**
    * **merge**  
    ```
    git checkout master
    git merge dev
    ```
    Or
    ```
    git checkout master
    git rebase dev
    ```
21. REBASE vs MERGE  
    in your repository, create a bunch of files in dev branch, then in master branch as well:  
    ```
    git checkout dev
    touch test.c
    git add test.c
    git commit -m 'adding a c file'
    git checkout master
    touch test.yml
    git add test.yml
    git commit -m 'adding yaml file'
    git checkout dev
    touch test.txt
    git add .
    git commit -m 'adding text file'
    git checkout master
    ```
    Now run: **`git log --graph --oneline`** 
    It shows how your two branches are organized.  
    Let's do a **merge**: **`git merge dev`**
    Run again: **`git log --graph --oneline`**    
    
    Create another bunch of files:  
    ```
    git checkout dev
    touch test.rs
    git add test.rs
    git commit -m 'adding rust file'
    git checkout master
    touch test.md
    git add test.md
    git commit -m 'adding markdown file'
    git checkout dev
    touch test.doc
    git add .
    git commit -m 'adding doc file'
    git checkout master
    ```
    Now run: **`git log --graph --oneline`** 
    It shows how your two branches are organized.  
    Let's do a **rebase**: **`git rebase dev`**
    Run again: **`git log --graph --oneline`**    
    
    What are your conclusions ?  
    
22. Manipulate the history   

    You can change the order of your revisions, delete them or even change their contents.  
    For e.g. to work on the last 4 commits of our master branch:  
    `git rebase -i HEAD~4`  
    (Prior to this command, you can set the EDITOR variable: `export EDITOR=vi` - otherwise the default editor is nano -)
    The previous command opens an editor where subcommands are available to manipulate the selected commits.  
    
23. Revert a commit  

    `git log --oneline`
    `git revert c4cdce1`  

### Collaborate with git  

1. Clone  
   Recall git is a distributed system.  
   We can then have multiple copies of the history at multiple locations.  
   clone is the command to do such a copy.  
   
   **clone locally:**  
   `git clone studentx_repo1 studentx_repo2` 
   **clone via ssh:**  
   e.g. from kvm-host-1:  
   `git clone ssh://studenty@kvm-host-2/home/studenty_repo1/ studenty_repo1`   
   
   **!!! ATTENTION**: by default git will pull the current remote branch (the one where the HEAD points)  
   Though, other branches (if they exist) metadata are also present in the cloned repo: `git branch -a` 
 
2. Remotes  
   after a clone, "remotes" are automatically set.  
   They represent the distant repos your local cloned repos refer to.  
   `git remote -v`  
   By default, those remotes are called **origin**  
   e.g. **`git checkout origin/qa`** will checkout the remote branch qa on the distant repo  
   
3. Fetch and Pull    
   Fetch pulls metadata from a distant repo you are connected to.  
   Pull pulls data from a distant repo you are connected to.  
   In other words, only pull actually updates the local repo with the contents of the remote repo.  
   
> **EXERCISE**   
> You are studentx on kvm-host-1. There is a studentx_bis (password = studentx_bis) on kvm-host-2.    
> Or You are studenty on kvm-host-2. Then there is also a studenty_bis (password = studenty_bis) on kvm-host-1.  
> student\*\_bis has a repo called countries in his home directory.  
> * Your task is to clone the dev branch of the countries repo into a local repository called pays and ensure all contents are present locally.  
> *You can log as student*_bis and explore the contents of the countries repo to compare and see if your previous clone operation was successful.  
> *If that's the case, you should normally have 5 countries files: togo, ghana, kenya, luxembourg and benin.  
> *However, there is still a missing file: the one for cameroon  
> Why is it not present in the clone repo ? Fix the issue so that the file appears in your local repo pays.  


     
       

