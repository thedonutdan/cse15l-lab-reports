# Lab 1 - File Systems

First command: `cd` 
We will run the cd command three times. First with a directory as an argument, second with a file as an argument, and
third with no argument.  
**`cd` with a directory as an argument**
Output:  
```
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$ cd ..
[user@sahara ~]$ cd lecture1/messages
[user@sahara ~/lecture1/messages]$ cd ~
[user@sahara ~]$ cd messages
bash: cd: messages: No such file or directory
```
In this example we can see that providing "lecture1" as an argument changes the working directory to "lecture1" and the same for "lecture1/messages" changing the working directory to "messages." However, when an invalid path is entered, an error is returned.  

**`cd` with a file as an argument**  
Output:  
```
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
[user@sahara ~/lecture1]$ cd Hello.java
bash: cd: Hello.java: Not a directory
```
Here we can see that using a filename as an argument for the cd command results in an error as cd will
only accept directories as arguments.  

**cd with no arguments**  
Output:  
```
[user@sahara ~/lecture1/messages]$ cd
[user@sahara ~]$ 
```
Here we can see cd returning the working directory to the home directory when no arguments are provided.  

Second Command: `ls`  
We will again run the `ls` command three times. One time with a directory as an argument, one time with a filename as an argument, and one time with no arguments.
**ls with a directory as an argument**  
Output:  
```
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
[user@sahara ~]$ ls messages
ls: cannot access 'messages': No such file or directory
```
Here we an see ls listing the contents of directories as long as their path is valid and presenting an error when the command cannot find the directory.  

**ls with a filename as an argument**  
Output:  
```

```

