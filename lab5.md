# Lab 5 - Putting It All Together  
**By Daniel Andrews**

**Part 1 - Debugging Scenario**  
**Student:**  
Hello, I've cloned the ArrayExamples repo from Lab 3 from the CSE15L github page and I'm trying to run some tests on it using a bash script. The problem is that I keep getting an issue with the reverseInPlace test. I looked at the funciton and it looks alright, it should be taking the elements at the start and putting them at the end, and vice versa, but I can't seem to get it to run! Help would be appreciated!  
![Image 1] (https://thedonutdan.github.io/cse15l-lab-reports/symptom.png)  
Here is a screenshot of the results from running the tests.  

**TA:**  
Hello! You should open the .java file and look closely at the function. Think about how the array changes as elements are switched around, is the function missing a step?  

**Student:**  
I looked again at the function, and noticed that it never saves any of the elements that are being replaced, so it ends up switching elements back around again! I made some edits and this is how the .java file looks now!  
![Image 2] (https://thedonutdan.github.io/cse15l-lab-reports/afterfix.png)  
The tests pass! Thanks for the help!  

**Setup**  

Files and directories:  
/lab3  
  /lib  
    -hamcrest-core.jar  
    -junit-4.jar  
  -ArrayExamples.java  
  -ArrayTests.java  
  -test.sh  

File contents before the bug fix:  
ArrayExamples.java  
![Image 3] (https://thedonutdan.github.io/cse15l-lab-reports/beforefix.png)  

ArrayTests.java  
![Image 4] (https://thedonutdan.github.io/cse15l-lab-reports/arraytests.png)  

test.sh  
![Image 5] (https://thedonutdan.github.io/cse15l-lab-reports/bash.png)  

**Part 2 - Reflection**  

The thing I've learned most about is utilizing VIM. I've had plenty of experience using the command line from prior experience programming in school and as a hobby, but I always avoided using VIM even if it was something I did want to learn. While I see myself still primarily using desktop apps rather than the command line text editor it is a use tool for some situations like when I am working on a remote server through the command line.

