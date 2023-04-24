# Lab 2 Lab Report 2 - Servers and Bugs (Week 3)

##Part 1 (String Server)
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
I will be doing the.


##Part 3 (Reflection)


