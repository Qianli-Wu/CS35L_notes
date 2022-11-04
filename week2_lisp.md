







# Fall 2022

# CS 35L

# Discussion 1E

# Week 2





## ssh key pairs

* hopefully everyone can log in to SEASnet servers quickely 

* Still need passwords?
  * Check the access permissions for `.ssh` and `authorized_keys`
  * `ssh` 700 or ?
  * `authorized_keys` 644 or 600
  
  
  
  > May fail to connect SEASnet server now :(
  
  ```bash
  [classiwu@lnxsrv15 ~]$ ls -alh | grep '.ssh'
  drwxr-xr-x  2 classiwu class 4.0K Sep 29 22:44 .ssh
  
  [classiwu@lnxsrv15 ~]$ ls -alh .ssh | grep '*keys'
  -rw-r--r--  1 classiwu class   99 Sep 29 22:44 authorized_keys
  ```
  
  

* Still not working?
  * We can try to figure it out after the discussion, but what I will do is google it. :)





### Tip: alias

##### 	For Mac, Linux, and WSL users (idk how to use Windows Powershell)

* use `alias` to simplify command

* ```sh
  $ alias
  alias ll='ls -alF'
  alias vi='vim'
  ```

* Executing `$ ll` is equivalent to runing `$ls -alF`

* ##### Which command do you use most frequently?

* > go to terminal



##### 	Another Example: 

* ```sh
  $ alias ln15="ssh username@lnxsrv15.seas.ucla.edu"
  $ ln15
  *****************************************************************************
                      lnxsrv15.seas.ucla.edu RHEL 8
  *****************************************************************************
  
  	* User processes older than 36 hours will be cleaned up
  
  *****************************************************************************
  *****************************************************************************
  * SEASnet Computing Access                                                  *
  *                                                                           *
  * Priority is given both on the servers and in the student labs to those    *
  * students doing coursework. Computing support for research is provided by  *
  * each department.                                                          *
  *****************************************************************************
  * For assistance please contact help@seas.ucla.edu or call 206-6864.        *
  *****************************************************************************
  Activate the web console with: systemctl enable --now cockpit.socket
  
  Last login: Mon Oct  3 23:06:29 2022 from 172.28.136.203
  [classiwu@lnxsrv15 ~]$
  ```

* **Warning**: might be **DANGEROUS** ! 

* ```sh
  $ unalias ln15  # remove aliasing
  ```

* Make it *Permanent* 

  ```sh
  $ cd ~
  $ vim .bash_profile 
  ```



* ##### [Optional]:  '.bashrc' vs '.bash_profile'

* `.bash_profile`: run commands that should run only once, such as customizing the `$PATH` [environment variable](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/)

* `.bashrc`: put the commands that should run every time you launch a new shell

* Reference: https://linuxize.com/post/bashrc-vs-bash-profile/



## Start VS Code on Terminal

Reference: https://code.visualstudio.com/docs/setup/mac

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Visual_Studio_Code_1.35_icon.svg/2048px-Visual_Studio_Code_1.35_icon.svg.png" style="zoom:10%;" />

* Open your VS Code

* `Command + Shift + P`

* Type `shell` and hit `enter`

  ```haskell
  >shell
  ```

* Done!

##### Not Working?

* If you are using `bash`:

  ```bash
  cat << EOF >> ~/.bash_profile
  # Add Visual Studio Code (code)
  export PATH="\$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"
  EOF
  ```

* If you are using `zsh`

  ```zsh
  cat << EOF >> ~/.zprofile
  # Add Visual Studio Code (code)
  export PATH="\$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"
  EOF
  ```



##### Still Not Working?

* google it

* try troubleshoot by yourself

  



## ELisp

* Reference: https://www.gnu.org/software/emacs/manual/html_node/eintr/

<img src="https://download.logo.wine/logo/Emacs_Lisp/Emacs_Lisp-Logo.wine.png" alt="Elisp" style="zoom:15%;" />

***

##### Q: When will you learn Lisp again?

* CS 111 Operating System?
* CS 131 Programming Languages?
* CS 161 Artificial Intelligence? 
* CS 192 What is that? 

<details>     
  <summary>Answer</summary>     
  <p style="color: red"> CS 161 and CS 192 (maybe)! </p>
</details>


***

##### Q: When was Lisp developed?

* 1930s ?
* 1950s ? 
* 1980s ?
* 2010s ?

<details>     
  <summary> Answer</summary>     
  <p style="color: red">A: 1958 John McCarthy developed LISP, the first functional language </p>
</details>

***

##### [Optional] Definition of Pure Functions:

According to Prof. [Nachenberg](http://careynachenberg.weebly.com/)'s slide in CS 131:

* A function that has two properties:

  1. Given a specific input `x`, the function *always* returns the same output `y`. 
  2. It doesn't modify any data beyond initializing local variables required to compute its output.

* ```c++
  # Pure
  int f(int p){
    int q = 5 * p * p
    return q
  }
  ```

* ```c
  # Impure
  int z;
  int f(int p){
    return p * z++;
  }
  ```

  

***

##### [Optional] Functional languages:

* Only composite of functions

* Can't change variable state
  
  ```c++
  int f(int p) {
    p = p + 1    // NOT Allowed
    return p
  }
  ```
  
  * No for loops; Only recursions
  * Why?
  
  ```c
  for (int i = 0; i < 10; i++){
    ...  // i = 1    =>   i = 2    => ....  =>  i = 10
  }
  ```
  
* The order of execution is not important

  * What is a `Pure` function?

* You will learn more about it in **CS 131**



### Data types

##### Integer Type

```lisp
-1               ; The integer -1.
1                ; The integer 1.
1.               ; Also the integer 1.
+1               ; Also the integer 1.
```

* *fixnum*: small integers

  * Its range depends on your machine

  * Try use `M-:` to run ` (print most-positive-fixnum)` in Emacs

  * Challenge: How many bits needed? 

  * <details>     
      <summary>Answer</summary>     
      <p style="color: red"> (log most-positive-fixnum 2) </p>
    </details>

* *bignum*: large integers

  * can have arbitrary precision

  * Which *data structure* might be used?

  * <details>     
      <summary>Answer</summary>     
      <p style="color: red"> Linked List </p>
    </details>



##### Floating-point type

```lisp
1500.0         ;1500
+15e2          ;1500
15.0e+2        ;1500
+1500000e-3    ;1500
.15e4          ;1500
```



##### Character Type

```lisp
?Q ⇒ 81  ?q => 113
```

* A *character* in Emacs Lisp is nothing more than an integer. 



##### Symbol Type

```lisp
foo                 ; A symbol named ‘foo’.
FOO                 ; A symbol named ‘FOO’, different from ‘foo’.
1+                  ; A symbol named ‘1+’
                    ;   (not ‘+1’, which is an integer).
\+1                 ; A symbol named ‘+1’
                    ;   (not a very readable name).
\(*\ 1\ 2\)         ; A symbol named ‘(* 1 2)’ (a worse name).
```

* A *symbol* in GNU Emacs Lisp is an object with a name
* A symbol can serve as a 
  * variable
  * function name
  * ...
* Note: In Common Lisp, lower case letters are always folded to upper case, unless they are explicitly escaped. In Emacs Lisp, upper case and lower case letters are distinct.



###### List Type:

```lisp
(A 2 "A")            ; A list of three elements.
()                   ; A list of no elements (the empty list).
nil                  ; A list of no elements (the empty list).
("A ()")             ; A list of one element: the string "A ()".
(A ())               ; A list of two elements: A and the empty list.
(A nil)              ; Equivalent to the previous.
((A B C))            ; A list of one element
                     ;   (which is a list of three elements).
```

***

* ```lisp
  '(rose violet daisy buttercup)
  '(+2 2)
  ("white rose")
  ```
  
* or

* ```lisp
  '(rose
    violet
    daisy
    buttercup)
  ```

* The elements of this list are the names of the four different flowers, separated from each other by **whitespace** and surrounded by **parentheses**



###### Numbers in List

* ```lisp
  (+ 2 2) ; a list with a plus-sign, followed by two ‘2’s, each separated by whitespace.
  (+ 88 6)
  ```



###### List in List

* ```lisp
  '(this list has (a list inside of it))
  (+ 2 (+ 2 2)) 
  ```





* In Lisp, both **data** and **programs** are represented the same way



###### Evaluate List

* send you an error message
  * `Debugger entered--Lisp error: (invalid-function ...)`
* do nothing except return to you the list itself 
  * `'(rose violet daisy buttercup)`
* treat the first symbol in the list as a command to do something
  * `(+ 2 2)`

* ##### Key Binding to Evaluate: C-x C-e

* > go to terminal





##### Function Types

* Functions are also **Lisp objects**
* All functions are defined in terms of other functions, except for a few *primitive* functions that are written in C.
* They are written in C so we can easily run GNU Emacs on any computer that has sufficient power and can run C.
* A **lambda expression** can be called as a function even though it has **no name**;



###### Examples:

* `quote` returns object, without evaluating it

  ```lisp
  (quote (+ 2 2))
  '(+ 2 2)  ; equivalent
  ```

* `car` returns the first element in a list

  ```lisp
  (car '(rose violet daisy buttercup))
  ```

* `cdr` returns the rest of the list

  ```lisp
  (cdr '(rose violet daisy buttercup))
  (violet dasiy buttercup)
  ```

* `cons`  constructs lists

  ```lisp
  (cons 'I  '(like lisp))
  (cons (car '(rose violet daisy buttercup)) (cdr '(rose violet daisy buttercup)))
  ```

* `append` attaches one list to another

  ```lisp
  (append '(1 2 3 4) '(5 6 7 8))  ; (1 2 3 4 5 6 7 8)
  (cons '(1 2 3 4) '(5 6 7 8))    ; ((1 2 3 4) 5 6 7 8)
  ```





###### Exercise:

> Time to do Week 1 Worksheet

* What do the following Lisp expressions output, when evaluated?

```lisp
a. (quote (1 2 3))                    ;(1 2 3)
b. '(1 2 3)                           ;(1 2 3)
c. (list (+ 1 2) '(+ 1 2))            ;(3 (+ 1 2)
d. (cons (+ 1 2) '(3 4))              ;(3 3 4)
e. (+ 10 (car '(1 2 3)))              ; 11
f. (append ‘(1 2) ‘(3 4))             ; (1 2 3 4)
g. (reverse (append '(1 2) '(3 4)))   ; (4 3 2 1)
h. (cdddar (1 2 3 4 5 6 7))           ; error
```





###### How to define a function?

1. Function name.
2. A list of the arguments
3. [Optional] Documentation describing the function 
4. [Optional] An expression to make the function interactive
5. Body of the function

```lisp
(defun function-name (arguments…)
  "optional-documentation…"
  (interactive argument-passing-info)     ; optional
  body…)
```



###### Interactive?

* If a function is interactive, you can use it by typing `M-x` and then the `name of the function`
* Or by a key defined by you



```lisp
(defun multiply-by-thirty-five (number)
  "Multiply NUMBER by Thirty Five."
  (* 35 number))
```

* Non-interactive

* How to use this function?

  ```lisp
  (multiply-by-thirty-five 2)
  ```




###### Exercise

> Time to do our worksheet

Write a function called `is-even` that takes one argument and returns whether it is even.

1. Example: (is-even 4) should evaluate to t.
2. Example: (is-even 3) should evaluate to nil.

```lisp
;;; Solution
(defun is-even (number)
  "Return whether a number is even"
  (interactive "Return whether a number is even")
  (= (% number 2) 0))
```





###### Jargons in Emacs:

* *Point* is the current location of the cursor.
  * More precisely, on terminals where the cursor appears to be on top of a character, point is immediately before the character.
  * In Emacs Lisp, point is an integer. The first character in a buffer is number one, the second is number two, and so on.
  * The function `point` returns the current position of the cursor as a number
*  *Mark* is another position in the buffer.
  * Use C-SPC (`set-mark-command`) to set a mark
* *Region* is the part of the buffer between point and mark



###### save-excursion

* It saves the location of point, 
* executes the body of the function, 
* and then restores point to its previous position if its location was changed.
* `save-excursion` is often used to keep point in the location expected by the user.



```lisp
(defun what-line ()
  "Print the current buffer line number and narrowed line number of point."
  (interactive)
  (let ((start (point-min))
	(n (line-number-at-pos)))
    (if (= start 1)
	(message "Line %d" n)
      (save-excursion
	(save-restriction
	  (widen)
	  (message "line %d (narrowed line %d)"
		   (+ n (line-number-at-pos start) -1) n))))))
```



##### Tips:

* Get help `C-h f ${function name}`
* Explore Source Code







## Python

![](https://www.python.org/static/img/python-logo@2x.png)

### Installing

* Mac/Linux:

```bash
$ which python
$ which python3
```

* Windows:

```bash
$ where python
$ where python3.exe
```



* If you don't have Python installed: https://www.python.org/downloads/



### Version

```bash
$ python3 --version  # or
$ python3 -V   # or
```



### Conda

![](https://docs.conda.io/en/latest/_images/conda_logo.svg)

* Conda is an open source **package management** system and **environment management** system that runs on Windows, macOS, Linux and z/OS. Conda quickly *installs*, *runs* and *updates* packages and their dependencies.

* Reference: https://docs.conda.io/en/latest/

  

### Tools you can use

* **Terminal**

<img src="http://cdn.onlinewebfonts.com/svg/img_255394.png" style="zoom:15%;" />

* ##### Jupiter Notebook

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Jupyter_logo.svg/883px-Jupyter_logo.svg.png" style="zoom:20%;" />

* **PyCharm**

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/1d/PyCharm_Icon.svg/768px-PyCharm_Icon.svg.png" style="zoom:25%;" />

* **VS Code**

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Visual_Studio_Code_1.35_icon.svg/2048px-Visual_Studio_Code_1.35_icon.svg.png" style="zoom:10%;" />



* **Emacs**

<img src="https://download.logo.wine/logo/Emacs_Lisp/Emacs_Lisp-Logo.wine.png" alt="Elisp" style="zoom:15%;" />

### Quote from my MATH 164 Professor Dr. Gleizer's shirt

$$
\text{I have } \ e^{\pi i} + 1 \text { friends}
$$



```python
>>> import cmath
>>> cmath.e ** (cmath.pi * i) + 1       # hopefully 0?
```















> Sashwath Sundher, Assignment 6 Guide, Youtobe Videos



