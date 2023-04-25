# Lab 2 Lab Report 2 - Servers and Bugs (Week 3)

##Part 1 (String Server)

StringServer code
````
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    
    String message;

    public String handleRequest(URI url) {
        //if userinput contains "/add-message"
        if (url.getPath().equals("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                message += "\n" + parameters[1];
                return message;
            }
        }
        return "404 Not Found!";
    }
}

//use from numberserver
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

````

<img width="592" alt="Screen Shot 2023-04-24 at 3 17 24 PM" src="https://user-images.githubusercontent.com/130106644/234128517-e68fb4ce-bd67-4590-91eb-5e92663dd57d.png">



The frist thing I did was call the main method, by compiling the file "StringServer.java" and inputing java StringServer 1555. That gave me the link to input the url. In this screenshot I used the "/add-message?s=<string>" that is in Handler class that implements URL handler that NumberServer also uses. 
Inside of my handler class I have a coditianls that uses .equals to check for "/add-message". In the input I used, there was an add message and a string of Hello. My method then splits the url path at the "=" and the assigns the split string in to refernce I created to store the split stirng. 
Additinally the method also creates a new line, by checking for S in the splitted message url path.
Then the website output would end up being message used in the url path, appearing as "Hello".

 
 
 <img width="644" alt="Screen Shot 2023-04-24 at 3 19 25 PM" src="https://user-images.githubusercontent.com/130106644/234128799-6cd058aa-df37-4e88-8980-0ec54fc83685.png">

 
 
In this screen shot, I used the same string command that the method uses to add new strings. The server is still the same being "http://localhost:1555/", and the add message command in the path is the same only string input if differnt here. 
. In the last screenshot a new line was actally created. This input command works the same as the last screenshot
only now the message is just diffent. This leads to output being "How Are You. 
 

##Part 2 (Bugs)
 
I will be doing ListExamples examples for bugs.
 
(A failure-inducing input)
````
 @Test
    void testMergePass() {
        List<String> list1 = Arrays.asList("apple", "banana", "cherry");
        List<String> list2 = Arrays.asList("cherry", "date", "elderberry");
        List<String> expected = Arrays.asList("apple", "banana", "cherry", "cherry", "date", "elderberry");
        List<String> actual = ListExamples.merge(list1, list2);
        assertEquals(expected, actual);
    }
 ````

 (An input that doesn’t induce a failure)
````
    @Test
    void testMergeFail() {
        List<String> list1 = Arrays.asList("apple", "banana", "cherry");
        List<String> list2 = Arrays.asList("cherry", "date", "elderberry");
        List<String> expected = Arrays.asList("apple", "banana", "cherry", "date", "elderberry");
        List<String> actual = ListExamples.merge(list1, list2);
        assertEquals(expected, actual);
    }
 
 ````
 
(Debugging)
 
(before)
````
 static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index1 += 1;
    }
    return result;
  }


}
 
 ````
 
 (after)
 ````
 static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
}
 ````
 
 
 
 

##Part 3 (Reflection)
 
 Learning how to create local and remote servers was really intersting. Understanding how paths and the terminolgy behing websites is something useful that I learned too.

