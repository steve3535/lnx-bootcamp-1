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
14. ```git status``
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
    
     
       

