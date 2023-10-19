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
![image1](https://thedonutdan.github.io/cse-15l-labreports/2023-10-19.png)  
![image2](https://thedonutdan.github.io/cse-15l-labreports/2023-10-19 (1).png)  

