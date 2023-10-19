# Lab 2 Report  

**Part 1**  
In this lab we will first build a string server which supports the path `/add-message` and concatenates the desired message to a string which will be printed line by line in the browser window. The java code for this server is listed below:  

```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    String content = "";
    int linenum = 0;

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return content;
        } else if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    linenum += 1;
                    content = content + String.format("\n%d. %s", linenum, parameters[1]);
                    return content;
                }
            
        }       
        return "404 Not Found!";
        
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

```

Here is the server output in the browser:  
![image1](https://thedonutdan.github.io/cse15l-lab-reports/2023-10-19.png)  
Here is a breakdown of the methods which are called in this screenshot and their relevant arguments and fields:  
The first method, which is called when we start the server, is the `main` method in the `StringServer` class. The only parameter is an array of `String`s which, in thise case, contains the port number `42069`. This opens a port on the local machine where we can access the server.  
Next, `Server`'s `start` method is called with the port number, `42069`, and a new `Handler` class as the arguments. This starts the server and informs it that it should be listening to port `42069`.     
The `Handler` class is important as it is how the program handles requests sent to the port. The relevant fields in `Handler` are `String content` and `int linenum` which keep track of the string displayed on the page and the line numbers, respectively. Upon receiving a request, `handleRequest` is called which will check the validity of the request and handle it accordingly based on the `URL` provided as an argument. In this case it is `http://localhost:42069/add-message?s=This%20is%20how%20we%20add%20a%20line%20`. If the path is correctly entered, `handleRequest` will increment the line number, retrieve the string to be concatenated onto our `content` string, and display the string to the page. If there is no path entered `handleRequest` will simply display the string.  
In this case, `handleRequest` changed `linenum` by adding one to it and also concatenated the string `This is how we add a line` to the `content` string.  


![image2](https://thedonutdan.github.io/cse15l-lab-reports/2023-10-19 (1).png)  
Since the server is already running in this screenshot the only relevant class and method is the `Handler` class containing the `handleRequest` method. The fields `content` and `linenum` have since been updated to contain the lines `2. The next entry will be added on a new line` and `3. So cool!`. The `URL` passed as an argument to `handleRequest` is `http://localhost:42069/add-message?s=So%20cool!` which increments `linenum` and concatenates `So cool!` to the `content` string.

**Part 2**
In this part of the lab we will be showing that I can find the private `ssh` key for my login into `ieng6` on my own machine as well as the public `ssh` key for my login into `ieng6` on `ieng6`. We will also show proof that it functions as expected when I log into `ieng6`.  
![image3](https://thedonutdan.github.io/cse15l-lab-reports/rsapriv.png)  
Here we can see the path to the private key stored on my local machine.     
![image4](https://thedonutdan.github.io/case15l-lab-reports/rsapub.png)  
Here we can see the path to the public key stored on my account on `ieng6` as well as me logging into my account on `ieng6` without being prompted for a password.  

**Part 3**  
Labs 2 and 3 have offered fascinating insight for me into 

