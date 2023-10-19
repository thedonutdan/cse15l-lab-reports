# Lab 1 - File Systems

First command: `cd`  
We will run the `cd` command three times. First with a directory as an argument, second with a file as an argument, and
third with no argument.  

**`cd` with a directory as an argument**

Output:  
```
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$
```
In this example our current working directory is home. When we call the `cd` command with `lecture1` as an argument we correctly change our working directory to `~/lecture1` without error.

**`cd` with a file as an argument**  
Output:  
```
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
[user@sahara ~/lecture1]$ cd Hello.java
bash: cd: Hello.java: Not a directory
```
Our current working directory for this example is `~/lecture1` and we can see that it contains some files and a folder. One of those files is `Hello.java` however, when we call `cd` with `Hello.java` as an argument we get a message informing us that `Hello.java` is not a directory. This is an error. `cd` requires a directory as it is designed to help us change our working directory.

**`cd` with no arguments**  
Output:  
```
[user@sahara ~/lecture1/messages]$ cd
[user@sahara ~]$ 
```
Our working directory is `~/lecture1/messages`. When we call `cd` with no arguments it returns us to the home directory. This is not an error at all as it is the expected behavior based on the documentation for `cd`.

Second Command: `ls`  
We will again run the `ls` command three times. One time with a directory as an argument, one time with a filename as an argument, and one time with no arguments.

**`ls` with a directory as an argument**  
Output:  
```
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
```
Our current working directory is `HOME`. When we use the `ls` command with a directory as an argument it lists the contents of the directory provided in the arguments. In `~/lecture1` we can see some files and another directory. This is not an error.

**`ls` with a filename as an argument**  
Output:  
```
[user@sahara ~/lecture1]$ ls Hello.java
Hello.java
```
The current working directory is `~/lecture1` Here we can see that when we give `ls` a valid filename as an argument the command will return the name of the file. This is not an error as the exit code given when we run this specific command is 0, indicating successful execution. 

**`ls` with no arguments**  
Output:  
```
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
```
The present working directory is `~/lecture1`. Here we can see that without arguments `ls` will print the contents of the present working directory. This is not an error and is actually the most common use of the command.

Third command: `cat`  
We will run the `cat` command three times. One with a directory as an argument, one with a filename as an argument, and one with no arguments.  

**`cat` with a directory as an argument**  
Output:  
```
[user@sahara ~/lecture1]$ cat messages
cat: messages: Is a directory
```
Our current working directory is `~/lecture1`. Calling `cat` with a directory as an argument returns an error, which we can know because the exit code is 1. `cat` does not have functionality revolving around printing directories.

**`cat` with a filename as an argument**  
Output:  
```
[user@sahara ~/lecture1]$ cat Hello.java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
}[user@sahara ~/lecture1]$ 
```
Our current working directory is `~/lecture1`. Here we can see that with a filename as an argument `cat` will print the contents of the file to the console. This is not an error.

**`cat` with no arguments**  
Output:  
```
[user@sahara ~/lecture1]$ cat


cat
cat
hello cat
hello cat
^C
[user@sahara ~/lecture1]$ ^C
```
Our current working directory is `~/lecture1`. Here we can see that if `cat` is provided no arguments it effectively functions like an `echo` command, reprinting whatever is entered into the command line. Examing the documentation for `cat` informs us that with no arguments `cat` will print the contents of `stdin`. This is not an error.
