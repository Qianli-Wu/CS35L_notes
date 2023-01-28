

# Winter 2022

# CS 35L

# Discussion 1D

# Week 3

## Table of Contents

* Python 
* Regex 
* Kahoot!



## Python

![](https://www.python.org/static/img/python-logo@2x.png)



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

  * Last week I was doing my Haskell homework on Emacs
    * And I installed a `haskell-mode`
  * Emacs has a built-in `python-mode`
    * Syntax highlighting
    * Indentation
    * ...






### Quote from my MATH 164 Professor Dr. Gleizer's shirt

$$
\text{I have } \ e^{\pi i} + 1 \text { friends}
$$





```python
>>> import cmath
>>> cmath.e ** (cmath.pi * complex(0,1)) + 1       # hopefully 0?
```





## argparse

* It is a package for Python3
* Similar with `optparse`
* Reference: https://docs.python.org/3/library/argparse.html



##### Creating a Parser

* The first step in using the [`argparse`](https://docs.python.org/3/library/argparse.html#module-argparse) is creating an [`ArgumentParser`](https://docs.python.org/3/library/argparse.html#argparse.ArgumentParser) object:

```python
import argparse
parser = argparse.ArgumentParser(description='Process some integers.')
```



##### Adding Arguments

```python
parser.add_argument('--sum', dest='accumulate', action='store_const',
                     const=sum, default=max,
                     help='sum the integers (default: find the max)')
parser.add_argument('-r', '--repeat', action="store_true", help = "output lines can be repeated")
```



##### Parsing arguments

```python
args = parser.parse_args()
```

```shell
$ python shuf.py -i 1-10
```



* a simple [`Namespace`](https://docs.python.org/3/library/argparse.html#argparse.Namespace) object will be built up from attributes parsed out of the command line



```python
>>> args
Namespace(accumulate=<built-in function max>, repeat=False)
```

##### Done!



##### Example

* Used in Deep Learning
* Part of the Pytorch MNIST Example:

```python
def main():
    # Create a Parser
    parser = argparse.ArgumentParser(description='PyTorch MNIST Example')
    # Add Arguments
    parser.add_argument('--epochs', type=int, default=14, metavar='N',
                        help='number of epochs to train (default: 14)')
    parser.add_argument('--lr', type=float, default=1.0, metavar='LR',
                        help='learning rate (default: 1.0)')
    parser.add_argument('--no-cuda', action='store_true', default=False,
                        help='disables CUDA training')
    parser.add_argument('--no-mps', action='store_true', default=False,
                        help='disables macOS GPU training')
    parser.add_argument('--seed', type=int, default=1, metavar='S',
                        help='random seed (default: 1)')
    # Parsing Arguments
    args = parser.parse_args()
    
    # Body
    use_cuda = not args.no_cuda and torch.cuda.is_available()
    use_mps = not args.no_mps and torch.backends.mps.is_available()

    torch.manual_seed(args.seed)
```





## Structural Pattern Matching?

* I'm **not** going to cover it this time

  * ~~because I forget most of it~~

* Learn how to learn things quickly 

  * read docs and tutorials 
    * https://peps.python.org/pep-0636/
    * https://docs.python.org/3/library/argparse.html

  

## tips

* **Divide and Conquer**

  1. arguments can be parsed correctly

  2. manage input

     * different cases, right?

       <details>     
       <summary>What might be useful?</summary>     
       <p style="color: red"> structural pattern matching (only in Python 3.10) </p>
       </details>
  
  3. Shuffle
  
  4. manage output
  
* **Read the documents and examples**

* Good luck!





## Regular Expression

>  Reference: 
>
> ​	https://cheatography.com/davechild/cheat-sheets/regular-expressions/
>
> ​	Yuxing's Slide in Winter 2022



* `grep` has two modes:
  1. basic 
  2. extended (with option -E) `grep -E`



##### Anchors (basic)

* `^` Start of the string
  * `^bash` matches `bash_profile` but not `I like bash`
* `$` End of the string
  * `shell$` matches `bash shell` but not `shell scripting	`
* ... 

google is your friend if you are interested in learning more



##### Quantifiers (basic)

* `*` 0 or more
  * `bash*` matches `bas`, `bash`, `bashhhhhhhhh`



##### Quantifiers (extended)

* `+` 1 or more
  * `bash*` matches `bash`, `bashhh`, but not `bas`
* `?` 0 or 1
  * `bash*` matches `bas`, `bash`, but not `bashhh`
* `{3}` exactly 3
  * `bash{3}` matches `bashhh`
* `{3,}` 3 or more
  * `bash{3,}` matches `bashhh`, `bashhhhhhhhhh`, ...
* `{1,3}` 1, 2, or 3
  * `bash{1,3}` matches `bash`, `bashh`, and `bashhh`

 

##### Groups and Ranges (basic)

* `.` any single character (except newline `\n`)
  * `s.t` matches `sit`, `sat`, `set`, ....
* `[]` any signle character contained
  * `[abc]` matches `a`, `b`, or `c`
  * `[a-z]` matches any letter from `a` to `z`
  * `[0-9A-Za-z]` matches any number from 0-9 and any letter

* `[^a]` any single character that is **NOT** a
  * Caret inside a brackets means not
  * `[^0-9]` means no number



##### Groups and ranges (extended)

* `()` group

  * `a(bc)*` matches `a`, `abc`, `abcbc`, ... but not `abbc`

* `(a|b)` a or b

  * `(abc|def)` matches `abc`, `def`

  * ```shell
    $ grep -E '(abc|def)' RET 
    ```



##### Escape

* `\` add it to the front of metacharacters to escape

  | ^    | [    | .    | $    |
  | ---- | ---- | ---- | ---- |
  | {    | *    | (    | \    |
  | +    | )    | \|   | ?    |
  | <    | >    |      |      |



##### Example of Regex in real life

* In your project, you may want users to input valid phone numbers

  * 10-digit, ...

  

  * <form action="/action_page.php">
      <label for="phone">Enter a phone number:</label><br><br>
      <input type="tel" id="phone" name="phone" placeholder="123-45-678" pattern="[0-9]{3}-[0-9]{2}-[0-9]{3}" required><br><br>
      <small>Format: 123-45-678</small><br><br>
      <button>
        submit
      </button>
    </form>

  * `^(\+\d{1,2}\s)?\(?\d{3}\)?[\s.-]\d{3}[\s.-]\d{4}$`

  * ```scss
    123-456-7890
    (123) 456-7890
    123 456 7890
    123.456.7890
    +91 (123) 456-7890
    ```



* **Email address**?
* https://www.bruintrade.com/signup



> Week 3 Regex worksheet

```
Write a basic regular expression that causes grep to match lines ending in the characters ‘dog’.

It should match:

‘bulldog’
‘smol dog’
‘hotdog’


It should not match:

‘doge’
‘dogecoin’
‘doggo’
‘woof dogs’
‘sinnoh remakes’

dog$   <-- Answer
```



```
Write a basic regular expression that checks whether or not a vowel is present

[aeiou]          <-- Solution1
[aeiou]\|y       <-- Solution2
```



```
Write a basic regular expression that causes grep to match lines solely consisting of alphabetical characters (A-Za-z) and digit characters (0-9), where no alphabetical characters appear before digit characters.

e.g.: 123abc

^[0-9][A-Za-z]$                <-- it will only match a single number/letter
^[0-9]*[A-Za-z]*$              <-- Correct
^[0-9]*.[A-Za-z]*$             <-- it will match any other symbol like $
^[[:digit:]]*[[:alpha:]]*$     <-- Correct
```



```
Write an extended regular expression that causes grep -E to match lines that either contain at least one digit or the string “flower”. It should be as short as possible. The optimal solution is 12 characters long. (If you like this sort of thing, check out code golfing!)
```



`([0-9]|flower)` <-- Correct!

\[0-9f](lower)?           <-- Will match a single `f`

(0-9|flower)              <-- Will only match `0-9` instead of a single number

`[0-9] | (flower)` <-- Optimal Solution!!!



