# Version Control

### Motivation

* Alternatives - You **won't lose** your code by accident
* we want from any system keep track of software system
  * it allows you to **keep historical versions** of the code, for easy reverting, comparison and investigation.

### Version control needs

* **history** of each project (backups for operators)
* planned **future** of each project (incomplete / wrong)



**DevOps**: Developers (write code) + Opeartors (管理员)

### Backups 

(from Ops viewpoint)

##### strategy: copy all the data once a day

* pros: 
  * simple  
* *cons*:
  * a lot excess work -- most data don't change
  * forget to do it
  * lose up to a day's work
  * need time to copy data, either:
    1. lose access while copying
    2. copy is not self-consistent

##### failure model

* flash drive fails completely
  * Annulized Faliure Rate (0.2% - 2.5%)
* flash drive fails partially (e.g., one block doesn't work)
* delete data by mistake (e.g. ```rm -rf /*```)
* trash data by mistake (e.g. changed a little bit of file)
* an outside attacter deletes/trashes files
* an insider deletes/trashes files

### What to back up?

* contents of files 
* metadata 
  * ```ls -l``` output, e.g. author, data, links
  * ```mant``` output, file system info
* backup units  ==  blocks (e.g. 8KB) 
* only backup changed blocks ( **incremental backup** )
  * save effort
  * save time
  * restores more cost

##### Do we need to back up every change?

* No - some changes aren't that important
* e.g. files in ```/tmp/*```
  * temperatory files generated

##### When do we reclaim backed-up storage?





##### How to do backups cheaply?

* do them less often
* do them to a cheaper, slower device
* remote backup service
* incremental backups

### Incremental backups

* **block oriented**: 

  * Old Version: 

    | OLD  | b1   | b2   | b3   | ...  |      |      |      | b8   | B9   |
    | :--- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |

  * New Version: 

    | NEW  |      | b2 new staff |      |      |      |      |      | b8 new staff |      |
    | :--- | ---- | :----------: | ---- | ---- | ---- | ---- | ---- | :----------: | ---- |

  * Representation of delta: 

    |  2   | new content |
    | :--: | :---------: |
    |  8   | new content |

  * NEW - OLD = a delta

  * store changes blocks and their contents

* **stream / text oriented ** :

  * New Version: 

    | NEW  |      | inserted line |      |      |      |      |      | changed line |      |
    | :--- | ---- | :-----------: | ---- | ---- | ---- | ---- | ---- | :----------: | ---- |

  * Block oriented *won't work* since after insertion every block after that line is changed

  * Representation of delta 

    * insert line 27  ``` line 27: ... ```
    * changes lines 100, 101  ``` line 100: ... ```
    * Delet line ...

  * can fit ```sed``` edit script

##### Other Optimization

* **Deduplication**
  * ``` cp a b```  copy ```a``` and writing to ```b```
  * **Copy-on-write** -- create a linke ```b``` points to ```a```'s data, pretend there's a copy
    * After someone changes ```a``` or ```b``` , make a late copy like ```cp a b```.
  * *cons*: if the user make copy because worrying the flash will collapse

* **Compression**
  * ```$ gzip < a > b```
  * *pros*: save space (smaller)
  * *cons*: longer to backup and recover
* **Multiplexing**
* single backup device to backup losts of pieces of data

* **Staging**
  * more backup devices that are bigger and slower 
    * like (RAM - flash - drive)

  * **Automated Data Grooming**
    * have a program automatically delete files (or move to another backup device)


##### Other issues of Backups

* **Encryption**
  * slower, consuming CPU time
  * good reason to do so: resist attacks? 
* **How do you know your backups work?**
  * test backups occationally
  * **checksum**
    * as you make a copy of data, also copy a short checksum
    * store checksum in another device
    * whenever use backup, make sure it matches the checksum



# File Systems with versioning

### Traditional

* simple: automatic, programmer won't worry about it
* Apps decide when there's a new version (e.g. whenever close, creates a new version)
* Used in traditional opearting system like ITS, TENEX, OpenVMS
  * ```foo.c;1```
  * ```foo.c;2```
  * ....
* Has 32767 versions max
* has data grooming - clean older files

### **Snapshot**

<img src="https://i.stack.imgur.com/Arh8o.png" style="zoom:80%;" />

* filesystem design allows for cheap snapshot of entire filesystem

* idea: all files are immutable

* SeasNET is using this strategy
  * ```cd .snapshot```
  * ```ls -l```
  * ```cd 2022-02-03```

* No updates allowed, cannot modify history



# Source Code Version Control

* ('backup for source code' ++)

* More efficient than file versioning
* more *useful* than file versioning

##### **Useful Features**:

* keep old versions indefinitely (so expensive to develop and small source code)
* record metadata, too 
  * e.g. Who made the change / When the change is made / regular file or symbolic link?
* file renaming (important in special case of metadata change)
* metadata about version control system
  * e.g. can I name a particular version v.2.33.0
* **atomic changes** to multiple part of the system
  * all or nothing, no intermediate stage
* Hooks (ability to modify how version control system works)
  * e.g. pre-commit hook - check over changes when commit to ensure following proper style rules
  * a program written by you or others
  * e.g. post-commit hook 
  * makes version control system tailorable

##### More Features

* navigation and visualization feature
  * be able to see what's the history looks like
* signed commits 
  * trust the security of project 
* format conversion
  * e.g. windows system use CR-LF ```\r\n```  while Liunx and MacOS use LF ```\n``` for newlines. 



# History of Version Control System (VCS)

> Reading: VCS history [[English](https://www.red-gate.com/blog/database-devops/history-of-version-control)] [[Chinese](http://www.zhuda6.com/new/61abbb92e1f24435844c59469198acce.html)] 



### [1972 - SCCS Source Code Control System](https://en.wikipedia.org/wiki/Source_Code_Control_System)

* Each source file F had a version file , has checksum but no encryption or compression


| metadata |      | ...  | beta^2 | beta^1 | s.data.txt |
| -------- | ---- | ---- | ------ | ------ | ---------- |

* local user + single file, retrive a file O(size(F)) 



### [1982 - RCS Revision Control System (free software)](https://en.wikipedia.org/wiki/Revision_Control_System)

* right before metadata, there's a copy of most recent copy of F

* Then, the difference of copy with previous version

* Then , the difference between previous version and earlier version, recursively.

* **cons**: It's more expensive to retrieve older version

* **pros**: It's cheaper to retrieve most recent version

  | metadata | copy of F_n | diff F_n and F_{n-1} | diff F_n-1 and F_n-2 | diff.... |      |
  | -------- | ----------- | -------------------- | -------------------- | -------- | ---- |

* ```$ diff A B >B-A.diff```

  * Compute B - A, show differences between new file B and old file A

* ```$ patch A < B-A.diff```

  * Generate a file, which is A + (B-A), which is old file + the difference with new file

* ```$ patch - R B <B-A.diff```

  * Generate a file, which is B - (B-A), which is new file - the difference with new file

  


### [1989 - CVS Concurrent Version System](https://www.nongnu.org/cvs/)

* RCS front end, second generation
* Support single commits that can change multiple files.
* **client-server model**, centralized
* **issues**:  scaling (based on RCS) - thousands of clients  | 1 server that must stay up



### [1998 - Bitkeeper](http://www.bitkeeper.org)

 (linux development switchent)

* SCCS + distributed Version Control System
* not open source at first so replace by git



### [2005 - Git](https://git-scm.com)

* replacement for Linux development switc
* dirtributed *version control* system built atop a distributed *file* system (POSIX)
  * history of project
  * planned future of project ( index | staging area | cache )
* ```$ git clone ... ``` make a copy of history of project and checkout working files from latest versio

> **Error Correction Code RAM (ECC RAM in bank system)**
>
> * correct single-bit error
> * detect 2-bit error by checksum

##### Which source files belong in version control?

* Automatically-generated source file
  * **pros**: people can just type 'make'
  * **cons**: git history too much
* Bootstrapping process
  * Put minimum source files that can generate all source files
  * a file called 'bootstrap', which connect these course files with all source file
* './configure'
  * generates platform-dependent configuration
  * Do 'bootstrap' in one machine and 'config' in another machine
* './gitignore'
  * Do not add files to git 

* ##### git commands

  * ```git ls-files	``` 
    * shows files under version control
  * ```git add``` 
    * add file F to the (index | staging area | cache)  - plan for next commit



# Git

##### start

```shell
$ git clone # clones existing repository + creates working file & empty index
$ git init # creates a new repo
$ git reset --hard HEAD # reset working tree as HEAD (works when only .git directory exists)
```

### Viewing the Commit History

##### show difference

```shell
$ git diff # working files - (repository + index)
$ git diff --staged (or --cached)  # compare index files with last committed files
$ git diff foo.c bar.h  # only show differences for these files
$ git diff A..B  # assuming A & B are commmit IDs
# if there's a collision in commit name and file name:
$ git diff A -- F  # look at the commit A and focus on difference in file F
```

##### show history

```shell
$ git log  # output the entire history of the project
$ git log A..B  # limits and logs between commit A and commit B
$ git log -p
$ git log --stat
$ git log --oneline
$ git log --pretty=format:"%h - %an, %ar : %s"
$ git log --oneline --decorate --graph --all
$ git log -S<string> # Look for differences that change the number of occurrences of the specified string (i.e. addition/deletion) in a file.

$ git reflog # full history no matter witch branch you are (records when the tips of branches and other references were updated in the local repository)
```

```shell
$ git show HEAD   # git log + git diff
$ git show A..B 
```

- **Commit expressions**
  - `A^`   A's parent
  - `A^^^^^ `, `HEAD~3`
  - `HEAD`   most recent commit
  - `name `   named commit
  - `A^!`    $\equiv$  `A^..A ` the difference between A's parent and A

```shell
$ git status # reminds you of what you're up to
```

```shell
$ git grep PATTERN  # =  grep PATTERN $(git ls-files)
```

##### Configuration

```shell
$ git config -l # list configuration from .git/config (in current directory) and ~/.gitconfig (global) and other files
$ git config --global user.name "Qianli Wu"
$ git config --global user.email qianliwu@g.ucla.edu 
```

##### Trace Contribution

```shell
$ git blame FILE  # see who contributed what in a FILE
$ git blame A -- FILE
```

```shell
$ git bisect # figure out who introduced the bug, narrowing the problem down
# specify a test case (any shell command), run it between good commit and bad commit in Binary Search O(logN)
$ git bisect HEAD # HEAD is bad
$ git bisect v27 # v27 is good
$ git bisect run make check  # "make check" can be any shell command
# problem1: GGBGGBBBGGBB  # bad versions happen mixed with good versions
# problem2: different branches, one good and one bad
```



### Git Branching

- a lightweight *movable* pointer to a commit (move the pointer for every new commit)
- Branching means you diverge from the main line of development and continue to do work without messing with that main line.
- More detailed explaination in notes for `week 5_git.md`

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

##### Branch operations

```shell
$ git fetch  # copy remote repository into ours (into a separate area)
# git fetch only update remote branch (e.g. origin/main)
$ git merge origin/master  

$ git checkout main # checkout to main branch
$ git merge <branch name> # look at common ancester A, then do a 3-way diff
$ git merge <parent1> <parent2> <parent3> ...  # can merge with multiple parents

$ git pull   # git fetch + git merge
# some philosophy: you should never pull to avoid merges; it depends on how you worried about merge (languages like C/C++ not good for merge)
```

```shell
$ diff3 -m O A N # Other(O), Common-Ancester(A), New-Version(N)
# !!! Can't assume other parts without conflicts are good
```

##### Tag

- also a lightweight pointer to a commit

- branches are movable tags

- Used for *important* commits

- `git tag [-a] <tag> [-m <tag message>] [<commit id>]`

- ```sh
  $ git tag -a v13 -m "Our best release!" <COMMMIT ID> # annotated tag, heavier weight tag (message)
  $ git tag v13 <COMMIT ID> # 
  $ git tag # list all tags
  $ git tag -l PATTERN  # show tags contains pattern
  $ git push origin v13  # push the tag v13 to public repository
  $ git tag -s -a v13 -m "Greatest version"  # sign this tag with my GPG key (public/private key)
  ```

-  Signing tags helps very much for distributing your software securely to your users.

- For developers, they can verify nothing malicious got introduced in a git commit

##### Commit

- Avoid changing history, especially in public repository: other developers may rely on it. 

```shell
$ git fetch # make sure the copy of upstream is up-to-date
$ git rebase origin/main  # like a merge
```

- cons: lying about history, **never do it in published repository**
- pros: has a much simpler history, a long straight line
- better for small staff (rebase than merge)

###### How to "edit" an older commit? Dangerous!!!

```{shell}
$ git rebase -i (other branch) # -i = interactive;
edit 68e342 ... # make some changes to previous commit 68e342, then git add, then git rebase --continue
reword 68e342  # change the commit message for commit 68e342
```

* Only Edit History in Repo that is not shared

* Aside: **Change History**

  ```shell
  $ git commit --amend    # Change most recent Git commit message
  ```


##### Stashing

* Work in progress

  ```shell
  $ git stash <save "save message"> # save the working image, with some message
  $ git stash list # check existed stashes
  $ git stash pop # reapply previously stashed changes, remove stashed changes
  $ git stash apply <ID> # reapply but keep stashed files
  $ git stash show # view a summary of a stash 
  $ git stash clear # delete all stash
  $ git stash drop stash@{1} # drop the second stash
  ```

* Alternetive (control the history)

  ```shell
  $ git diff > my.diff  # store difference in a file my.diff
  $ git checkout main  # switch working in main branch
  [edit....commit]
  $ git checkout p  # check back to older version
  $ patch -p1 < my.diff  # restore the progress
  ```

  ```sh
  $ diff A B >B-A.diff
  $ patch <A-B.diff. # edit A to make it look like B, A = A + (A-B.diff) == B
  ```



# Git Internals

* **plumbing** - low level stuff implementors care about  `e.g. git cat-file <file hash id>`
* **porcelain** - beauty treatment: *user-friendly* interface.  `e.g. git rebase`



### `./git` subdirectories:

1. `branches/` useless now
2. `config` configuration
3. `HEAD` head branch, which branch the current HEAD at? directory to another file
4. `hooks`/ specifies well-know
   - where creating your own porcelain (self-defined user-friendly commands)
5. `index` represent the next change
6. `info/exclude` things you don't want to pay attention to, like `.gitignore` but not in repository
7. `logs/` records when branch trips were updated
8. `objects/` files added to git repository
   - at first it stores all files compressed by zlib with name 40 bit hash
   - However, size too big for object and too many files under single directory
   - Thus, store first 2 digits as folder name, thus divides the number of files by 256
   - `git clone` will create a read-only hard links to those history files in repository, thus very cheap
9. `pack-ref` what all the names of commits, (tags)
10. `refs` not optimized version of `pack-ref`

* **Like POSIX file system, multiple pointers to a file (hardlink)**
  * like a virtual file system implemented above traditional file system, like VPN in network
  * `git hash-object` provides a bunch of bytes and it returns SHA-1 checksum of it
    * SHA-1 designed to be **reliable**, secure
    * it's really expensive to have different string to hash same SHA-1 value
    * attacker will have great trouble pretending other message was sent instead of the original
    
    


### Git Internal Structure

* `git cat-file` , `HEAD^{tree}`
* `git unpdate-index`  add a file to index
* `git write-tree` write a tree for what's in index
* `git commit-tree TREEID -p PARENT_COMMITID` commit a tree, they type commit message
* SHA_1 prevents cycling in git internal (commit graphs are DAG)
* Git cannot compress **jpeg** like file very well, but we can store them somewhere else and sore pointers to them


##### Bolb

* an git object (e.g. a file)

##### Tree 

* directory, maps names to other objects (other trees and bolbs)

  * (mode) octal number: file type (100: regularfile, 040: directory) + default permissions (644 rw for users an r for others)

  * type 

  * commit id

  * Name

##### Commit 

*  labeled object, containing **commit** **message** + **times** + **tree** **object** + ...



# Compression

* Objects are represented in compressed form

* Ways compression is done  **zlib $$ \approx $$ gzip**

* compression quality (the ratio between compressed and original file)

* performance (CPU time)

* zlib/gzip compression ideas:



### Huffman coding

* proved to be optimal for its problem

![](https://upload.wikimedia.org/wikipedia/commons/8/82/Huffman_tree_2.svg)

* Assume input is a sequence of symbols from a finit set (bytes 0-255)
* output is a bit string, each bit represents some bytes in input
  * common symbols with shortest bit
  * rarely used symbols with longer bits

##### Problem

* more prone to data crush: if a bit in output is incorrect, then if may affect many others behind it. 

* Can't figure out what's the last character since it can only read from front to end to decode

  

##### classic haffman coding

* compressor + decompressor know tree structure in advance
* zlib computes the tree on the fly
  * after each input symbol, the compressor updates its tree
  * the decompressor knows this
  
  

### Dictionary coding

* requires more memory, can use a lot of RAM
  * Sliding window approach
    * remove older words if the dictionary size is too much
* dictionaries won't be saved
  * decopression is relatively cheap O(N)
  * compression is expensive O($$N^2$$)
* fixed
  * the compressor and decopressor shares a dictionary of common words
  * assign each words an index, can add whitespace behind a word to reduce compressed size
  * Only works for specific, pre-defined language, e.g., English
* **adaptive dictionary compression**
  * when decoder encourters letter triplets or entire words that are not yet in the dictionary, then it adds them

* Zlib: **adaptive dictionary compression + huffman coding**

