# Lab Report 2 #

## Servers and Bugs ##

Author: Emma Dunmire

Date: 4/20/23

**Part 1**

The Code For StringServer
```import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    String str = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return "Page Is Open\n Add a string to begin";
        }
        else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    str += parameters[1] + "\n";
                    return String.format("%s", str);
                }
            }
            return "404 Not Found!";
        }
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

*insert screenshot 1*

When `add-message?s=Hi Again` is entered as a request, the handleRequest method in the Handler class is called. The value for the `url` parameter is the entire url.
Since the path for the url is not just a slash, the program checks if the url path is `/add-message` (which it is) and then will run the if-statement. Inside the if-statement,
the query gets split at the equals sign into an array containing two elements (one is s and the other is the inputted string). It will then add the inputted string to the
running string with an additional new line (`/n`) at the end and then output it as the return value.

*insert screenshot 2*

Similar to previous example, `add-message?s=How are you?` is the request, which alters the `url` parameter. Though the path will remain the same, the query changes from `s=Hi Again`
to `s=How are you?`. Calling the handleRequest method again, this time it will run through the same if-statements but will concatanate the string "How are you?" onto the previous
string. Now str will contain "Hello\nHi Again\nHow are you?\n" which will get output as the return value to the handleRequest method.
