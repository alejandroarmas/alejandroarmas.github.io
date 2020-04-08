---
layout: article
title: How to Submit Homework for ECS36B
tags: classwork
aside:
    toc: true
  
---



If you were anything like me, you were struggling a lot to submit your homework. Mainly since you had no idea what CSIF is and you have not coded anything in C before. Just follow along and you will be able to complete the homework assignment. In this tutorial I am using Ubuntu 18.04.4 LTS release and adding onto what Professor Wu has told us.


## Retrieving your files.


On your command line you will use these commands. You need to download git first. Git is one of many version control software systems that are extremely useful for developing software collaboratively. It is one of the most popular and many project files are held in online repositories such as github.com. To install, [follow this guide](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-18-04). Don't forget to make an account. We are using git simply to clone the class repository. 


```console

alejandro@Alejandro-Desktop:~/Documents$ git clone https://github.com/sfelixwu/ecs36b_s2020
alejandro@Alejandro-Desktop:~/Documents$ cd ecsb_s2020
alejandro@Alejandro-Desktop:~/Documents/ecsb_s2020$ ls
ecs36b_fake.txt             Makefile             socket_server_hw1.c
README.md                   socket_client_hw1.c
```

You should see these files present in whichever directory you chose to clone to. 


## What is a Makefile?

On inspection we see a file named Makefile in our directory. A type of file used to automate a set of tasks and compile a final executable binary according to the [reference](https://opensource.com/article/18/8/what-how-makefile) I will be following. If we open it we see the following code:

```console

# Makefile for HW1, ecs36b, s2020
#

CC = gcc
CFLAGS = -g -Wall -Wstrict-prototypes

# CFLAGS = -O3

# rules.
all: ecs36b_hw1_server ecs36b_hw1_client

#
#
socket_client_hw1.o:	socket_client_hw1.c
			$(CC) -c $(CFLAGS) socket_client_hw1.c

socket_server_hw1.o:	socket_server_hw1.c
			$(CC) -c $(CFLAGS) socket_server_hw1.c

ecs36b_hw1_server:	socket_server_hw1.o
			$(CC) -o ecs36b_hw1_server socket_server_hw1.o

ecs36b_hw1_client:	socket_client_hw1.o
			$(CC) -o ecs36b_hw1_client socket_client_hw1.o

clean:
	rm -f *.o *~ core ecs36b_hw1_server ecs36b_hw1_client

```

The typical syntax in your ```Makefile``` is the following. Recipes are the commands you would normally type in the command line, but because we want to automake the process of compiling, we do this. 
```console
target: prerequisites
<TAB> recipe

target: prerequisites
<TAB> recipe

target: prerequisites
<TAB> recipe
```

or as we see in our ```Makefile```. As you see, every target does not need a prerequisite or a recipe.

```console

all: ecs36b_hw1_server ecs36b_hw1_client

#
#
socket_client_hw1.o:	socket_client_hw1.c
			$(CC) -c $(CFLAGS) socket_client_hw1.c

socket_server_hw1.o:	socket_server_hw1.c
			$(CC) -c $(CFLAGS) socket_server_hw1.c

ecs36b_hw1_server:	socket_server_hw1.o
			$(CC) -o ecs36b_hw1_server socket_server_hw1.o

ecs36b_hw1_client:	socket_client_hw1.o
			$(CC) -o ecs36b_hw1_client socket_client_hw1.o

clean:
	rm -f *.o *~ core ecs36b_hw1_server ecs36b_hw1_client

```

When the make command is input, only the default goal i.e the first target is executed. Therefore projects typically have an **all** target as seen in our ```Makefile```, who's responsibility is to call other targets. By convention you do not make the **clean** a prerequisite for your **all** target.

In addition to this, you might have noticed that variables were defined in this ```Makefile```.

```console
CC = gcc
CFLAGS = -g -Wall -Wstrict-prototypes
```

What these lines of code do is replace every instance of CC with the ```gcc``` command and CFLAGS with ```-g -Wall -Wstrict-prototypes``` 

Let's say you wanted to call ```make socket_client_hw1.o``` in your terminal. 

i.e

```console
socket_client_hw1.o:	socket_client_hw1.c
			$(CC) -c $(CFLAGS) socket_client_hw1.c
```

Then your ```socket_client_hw1.o``` target in the Makefile would be called and it would use the ```socket_client_hw1.c``` sourcefile for the command ```gcc -c -g -Wall -Wstrict-prototypes socket_client_hw1.c```

Now you might be wondering... what in the world is this code executing?

## What is GCC?

GNU Compiler Collection (GCC) is a collection of libraries and compilers used for C, C++ and a variety of other programming collections. Many open source projects are compiled using GCC. 

Any human readable source code, is written programming language such as C, as the set of instructions to perform a specific task. A compiler then translates this human readable logic into an intermediate file type, called an object file. A linker will then combine multiple object files to create an executable file, which is typically what your finished program will look like.

```$ gcc -c [options] [source files]``` compiles source files without linking.

 ex. 

 ```console 
$ gcc -c -g -Wall -Wstrict-prototypes socket_client_hw1.c
```

- ```-g ``` flag generates debug information to be used by GDB debugger
- ```-Wall``` flag enables all compiler's warning messages. Convention is to always use this.
- ```-Wstrict-prototypes``` A flag ... which I'm not sure yet, but I will update soon!


Will essentially translate your human readable code into binary for the computer to understand. This command in particular compiles the C source code ```socket_client_hw1.c```into an object file ```socket_server_hw1.o```.    


```$ gcc [options] [source files] [object files] -o output file``` writes the build output to an output file.

 ex. 

 ```console 
$ gcc -o ecs36b_hw1_server socket_server_hw1.o

```

Will link the object file ```socket_server_hw1.o``` to create the executable ```ecs36b_hw1_server```



## Actually completing the Homework Assignment

Under the command-line terminal environment such as CSIF, please type “make” and two executables (your targets from the makefile code), ecs36b_hw1_client and ecs36_hw1_server, will be created. 

```console
alejandro@Alejandro-Desktop:~/Documents/ecsb_s2020$ make
alejandro@Alejandro-Desktop:~/Documents/ecsb_s2020$ ls
ecs36b_fake.txt                    hw1                  socket_client_hw1.o
ecs36b_hw1_client                  Makefile             socket_server_hw1.c
ecs36b_hw1_server                  README.md            socket_server_hw1.o
socket_client_hw1.c

```

For HW#1, the professor asks us to run the first program, ecs36b_hw1_client, to obtain information regarding your own student record via a JSON (Javascript Object Notation) format, from his server named Cyrus. And, you will need to store the JSON in a text file named [STUDENT ID].txt. And, you will just need to submit this file for this homework assignment.

More specifically, you will need to enter the following:

```console
alejandro@Alejandro-Desktop:~/Documents/ecsb_s2020$ ./ecs36b_hw1_client 169.237.6.102 95616 <your 9-digits student ID>

```

As an example, when I typed in the following:

```console

alejandro@Alejandro-Desktop:~/Documents/ecsb_s2020$  ./ecs36b_hw1_client 169.237.6.102 95616 XXXXXXXXX

```
I got:
```console
Hi, this is ecs36b_hw1 -- Tue Apr  7 13:34:35 2020
{"status": "successful", "name": "Armas, Alejandro", "sID": "XXXXXXXXX", "uID": "stayin", "session": "02", "time": "Tue Apr  7 13:34:35 2020", "ip address": "107.0.114.25", "port": "57106", "code": "1424268980"}
```

At this point, you have completed the homework assignment. You just need to turn it in. So lets get to that. 

## Homework Submission

You need to submit remotely to the [Computer Science Instructional Facility (CSIF)](http://csifdocs.cs.ucdavis.edu/about-us), which is located in the West wing of Kemper Hall on the basement level. The CSIF offer computer labs to UC Davis students either taking Computer Science course(s) or in the Computer Science/Computer Engineering field of study. 

Following instruction from [CSIF documentation](http://csifdocs.cs.ucdavis.edu/about-us/csif-general-faq#TOC-How-can-I-remotely-login-to-the-CSIF-computers-from-home-), and my command line again, since SSH, or Secure Shell is the protocol that CSIF uses for people who wish to log in remotely.

Out of the [list of computers](http://iceman.cs.ucdavis.edu/nagios3/cgi-bin/status.cgi?hostgroup=all) to choose from, I arbitrarily picked pc23 since it is a prime number. It really does not matter which one you select. 

If you remember from the JSON object from earlier, my uID is "Stayin". The command you use to connect to a single computer from the CSIF network is:

```console
ssh [username]@[hostname].cs.ucdavis.edu
```
In my case...

```console
alejandro@Alejandro-Desktop:~/Documents/ECS36B$ ssh stayin@pc23.cs.ucdavis.edu

```

You are now prompted with the following screen after submitting you Kerebos Credentials. 

```console
*
* Computer Science Instructional Facility
* Ubuntu 18.04.4 LTS
*

Hostname: pc23	Date: Tue Apr  7 17:18:23 PDT 2020
System Load:	0.15	IP Address:	
Memory Usage:	5.0%	System Uptime:	12:15 hours
Usage On /:	8%	Swap Usage:	0.0%
Local Users:	3	Processes:	273

*
* 09/17/2018 - home directories have been migrated to new space, to get your archived home directory, please see: http://ssg.cs.ucdavis.edu/news/csifnewhome
*

1 updates could not be installed automatically. For more details,
see /var/log/unattended-upgrades/unattended-upgrades.log

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

stayin@ad3.ucdavis.edu@pc23:~$ 
```


Now you will navigate the file system and 

- Create a subdirectory ecs36b_s2020, and then cd ecs36b_s2020.
- Create a subdirectory hw1, and then cd hw1.
- Edit the <your student ID>.txt file and copy/paste the JSON you receive from cyrus into this file.

```console

stayin@ad3.ucdavis.edu@pc23:~$ ls
stayin@ad3.ucdavis.edu@pc23:~$ mkdir ecs36b_s2020
stayin@ad3.ucdavis.edu@pc23:~$ ls
ecs36b_s2020
stayin@ad3.ucdavis.edu@pc23:~$ cd ecs36b_s2020/
stayin@ad3.ucdavis.edu@pc23:~/ecs36b_s2020$ mkdir hw1
stayin@ad3.ucdavis.edu@pc23:~/ecs36b_s2020$ cd hw1/
stayin@ad3.ucdavis.edu@pc23:~/ecs36b_s2020/hw1$ ls
stayin@ad3.ucdavis.edu@pc23:~/ecs36b_s2020/hw1$ vim [STUDENT ID].txt
```

Using Vim, a command line text editor, we are now creating a new file named [STUDENT ID].txt which we will store our JSON object from earlier. 

```vim
{"status": "successful", "name": "Armas, Alejandro", "sID": "XXXXXXXXX", "uID": "stayin", "session": "02", "time": "Tue Apr  7 13:34:35 2020", "ip address": "107.0.114.25", "port": "57106", "code": "1424268980"}

```
Now when not in insert mode, press :wq to save and quit. As you can see you just created a new textfile which you will submit. 

```console
stayin@ad3.ucdavis.edu@pc23:~/ecs36b_s2020/hw1$ ls
[STUDENT ID].txt
```

From the root directory you will now use the command "handin wjr ecs36b_hw1 FILENAME", to check if you successfully uploaded your assignment "ecs36b_hw1", use the command "handin wjr ecs36b_hw1"


```console
stayin@ad3.ucdavis.edu@pc23:~$ handin wjr ecs36b_hw1 ecs36b_s2020/hw1/[STUDENT ID].txt 
Submitting ecs36b_s2020/hw1/[STUDENT ID].txt... ok
stayin@ad3.ucdavis.edu@pc23:~$ handin wjr ecs36b_hw1
The following input files have been received:
Tue Apr  7 17:49:24 2020	212 bytes	[STUDENT ID].txt
stayin@ad3.ucdavis.edu@pc23:~$ 

```

To leave your ssh connection, use the command ```exit``` and your files will remain for the next time you make an SSH connection to this PC again.
```console
stayin@ad3.ucdavis.edu@pc23:~$ exit
```
