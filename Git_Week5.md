# Fall 2022

# CS 35L

# Discussion 1E

# Week 5



## Git

> Reference: [Pro Git 2nd Edition](https://git-scm.com/book/en/v2) 



* Berfore we start, please make sure you have installed Git

* If you haven't done so, it's OK

* Follow the instructions here:

  > https://git-scm.com/book/en/v2/Getting-Started-Installing-Git



##### Customize your Git Environment

* `git config`: set configuration variables

  ```mermaid
  flowchart LR
  		1(config) -->|override| 2("~./gitconfig")
  		2 -->|override| 3("[path]/etc/gitconfig")	
  ```

  

  * `[path]/etc/gitconfig` file: Contains values applied to every user on the system

    * use `git config` with option `--system` to change this file

    

  * `~/.gitconfig` file: Values specific personally to you, the user

    * use option `global` to write to this file

    

  * `config` file in the Git directory

    * use option `local` to write to this file



* First thing you should do: identidy yourself:

  ```bash
    $ git config --global user.name "Qianli Wu"
    $ git config --global user.email qianliwu@g.ucla.edu
  ```



> Worksheet Problem

1. [Make a private GitHub repository](https://github.com/new) titled “cs35l-assignments”.
2. Clone your newly created repository to your own computer.
3. Create an “assignment3/” directory. 
4. Put your related assignment 3 work in this directory. 
5. Commit it and push it to GitHub.
6. Clone your “cs35l-assignments” directory on SEASnet.
7. <span style="color:red"> [Optional] </span> How do you create a local repository and add it to Github?









## Git Branching



```mermaid
%%{init: { 'logLevel': 'debug', 'theme': 'base', 'gitGraph': {'showBranches': true, 'showCommitLabel':true, 'mainBranchName': 'main'}} }%%
      gitGraph
        commit id:"7049aca"
        commit id:"b0075f2"
        commit id:"27c2939"
        branch week4
        commit
        checkout main
        commit
        checkout week4
        commit
        branch week5
        checkout week4
        commit
        checkout week5
        commit
        checkout main
        merge week4
        checkout week5
        commit
        commit
        checkout main
        merge week5
        commit
  
```

* Branching means you diverge from the main line of development and continue to do work without messing with that main line.

* Git branches is lightweight

  * branching operations can be done instantaneously

  * why?

  * <details>     
      <summary>Answer</summary>     
      <p style="color: red"> pointers
     </p>
    </details>



##### Create a branch

* `git branch testing`

![](https://git-scm.com/book/en/v2/images/two-branches.png)



* How does Git know what branch you’re currently on?

  <details>     
    <summary>Answer</summary>     
    <p style="color: red"> another pointer called HEAD
   </p>
  </details>







![](https://git-scm.com/book/en/v2/images/head-to-master.png)



##### Switching Branches

* `git checkout`

  ```bash
  $ git checkout testing
  ```

![](https://git-scm.com/book/en/v2/images/head-to-testing.png)

* If we do another commit:

```bash
$ touch test.txt
$ git commit -a -m 'made a change in testing branch'
```

![](https://git-scm.com/book/en/v2/images/advance-testing.png)



##### Create a branch and Switch to it

* `git checkout -b ${branch_name}`















* By default Git will create a branch called *master* when you create a new repository

  ```bash
  $ git config --global init.defaultBranch main
  ```

  * Set `main` as the default branch name

