Lab 1 - File Systems

First command: cd 
We will run the cd command three times. First with a directory as an argument, second with a file as an argument, and
third with no argument.  
**cd with a directory as an argument**
Output:  
```
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$ cd ..
[user@sahara ~]$ cd lecture1/messages
[user@sahara ~/lecture1/messages]$ cd ~
[user@sahara ~]$ cd messages
bash: cd: messages: No such file or directory
```
Here we can see that when we use a directory with a valid path cd will change the working directory to
the directory given in the command argument. If we target something without a valid path, however, the 
command will result in an error as it cannot find the specified directory.  

**cd with a file as an argument**  
Output:  
```

```
Here we can see that using a filename as an argument for the cd command results in an error.
