

# Winter 2023

# CS 35L

# Discussion 1D

# Week 4



## React Workshop (Assignment 3 & Final Project) 

* **Date**: Fed 08 (Next Wednesday)
* **Time**: 6-8pm
* **Location**: TBD





## Midterm

* on Feb 09 (next Thursday)
* will be challenging
* probably easier than sample midterms, those are open computer





> Questions from Practice Midterm II

1. (1 min.) What is **one** main difference between a `hard link` and a `symbolic link`?

<details>     
  <summary>Answer</summary>     
  <p style="color: red"> Both point to a file, but hard links increment a file’s reference count whereas symbolic links do not. </p>
Other answers (not a complete list) include:
A file is deleted only when all hard links to it are deleted/deleting symbolic links does not affect the underlying file
A symbolic link can become dangling if the underlying file is deleted
</details>



5. (10 min.) Consider the shell command being executed on a device named “ubun3” by user “groot”:

```
ubun3:~/zoo-wee-mama groot$ a b < c | ./d > e
```

​	**a.** (2 mins.) What program(s) is/are being executed by the command?





​	**b.** (3 mins.) For each program you listed above, where will the shell look to find their executables?





​	**c.** (2 mins.) For each program you listed above, how many arguments is each being invoked with? What is the value of each argument?





```ba
ubun3:~/zoo-wee-mama groot$ a b < c | ./d > e
```

​	**d.** (2 mins.) What standard input does each program you listed above receive (if any)?



​	**e.** (1 min.) Where is the standard output of the above command written to?



​	**f.** Assume you are the owner of `d`, the following command is executed:

```shell
$ chmod 640 d
```

​	What will happen if you run `a b < c | ./d > e` again?

<details>     
  <summary>Explanation:</summary>     
  <table style="width:100%">
  <tr>
    <th>Owner</th>
    <th>Group</th>
    <th>Other</th>
  </tr>
  <tr>
    <td><mark style="color: red">read</mark>, <mark style="color: red">write</mark>, execute</td>
    <td><mark style="color: red">read</mark>, write, execute</td>
    <td>read, write, execute</td>
  </tr>
  <tr>
    <td>6</td>
    <td>4</td>
    <td>0</td>
  </tr>
  <tr>
    <td>110</td>
    <td>100</td>
    <td>000</td>
  </tr>
</table>
</details>







4. (20 mins.) Internet Protocol version 4 (IPv4) is a core protocol that is used to uniquely address devices with networking capabilities. It performs routing, which is the task of forwarding packets (chunks of data, like text messages, streaming videos, and literally everything else sent over the Internet) from one device to another.

   An IPv4 address typically looks like: [0-255].[0-255].[0-255].[0-255], where [0-255] is a decimal number from 0 to 255 inclusive. The periods are literal and separate the four numbers. Examples of valid addresses include:

   ​	127.0.0.1

   ​	192.168.0.255

   ​	32.45.8.21



​	**a.** (6 min.) Write an extended regular expression that only matches numbers between 0 and 255. It should not match numbers like “02” or “095”.

<details>     
  <summary>Answer</summary>     
  <p style="color: red"> ^([0-9])|([1-9][0-9])|(1[0-9][0-9])|(2[0-4][0-9])|(25[0-5])$
 </p>
</details>



​	**b.** (2 mins.) Write an extended regular expression that matches IPv4 addresses.

<details>     
  <summary>Answer</summary>     
  <p style="color: red"> ^(([0-9])|([1-9][0-9])|(1[0-9][0-9])|(2[0-4][0-9])|(25[0-5])\.){3}([0-9])|([1-9][0-9])|(1[0-9][0-9])|(2[0-4][0-9])|(25[0-5])$
 </p>
</details>





### Tips:

1. Print Assignment 1, 2, and 3
2. Get [emacs reference card](https://www.gnu.org/software/emacs/refcards/pdf/refcard.pdf) and [regular expression cheatsheet](https://cheatography.com/davechild/cheat-sheets/regular-expressions/)
3. Get failiar with [sed](https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/) and [awk](https://www.gnu.org/software/gawk/manual/gawk.html)
4. Make sure you understand the concepts related to client-server apps
5. (If time permits) Review **ALL** Lecture Recordings and take notes





## Next Week?

* Git
