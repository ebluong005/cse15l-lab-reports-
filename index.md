# Lab 2 Lab Report 2 - Servers and Bugs (Week 3) (Resubmit)

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
 
I will be doing ArrayListExamples examples for bugs.
 
(A failure-inducing input)
````
 @Test 
	public void testReversed1() {
    int[] input1 = { -1, -2, -3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ -3, -2, -1 }, input1);
	}


    
 ````

 (An input that doesn’t induce a failure)
````
  @Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
 
 ````
 
 Symptom of running tests
 
 ````
MacBook-Air-33:lab3-1 ethanluong$ javac ArrayExamples.java
MacBook-Air-33:lab3-1 ethanluong$ javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
MacBook-Air-33:lab3-1 ethanluong$ java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests
JUnit version 4.13.2JUnit version 4.13.2
...E.
Time: 0.003
There was 1 failure:
1) testReversed1(ArrayTests)
arrays first differed at element [2]; expected:<-1> but was:<-3>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReversed1(ArrayTests.java:23)
        ... 32 trimmed
Caused by: java.lang.AssertionError: expected:<-1> but was:<-3>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 38 more

FAILURES!!!
Tests run: 4,  Failures: 1
 
 ````
 
 
(Debugging)
 
(before)
````

public class ArrayExamples {

  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }

  // Averages the numbers in the array (takes the mean), but leaves out the
  // lowest number when calculating. Returns 0 if there are no elements or just
  // 1 element in the array
  static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }


}
 
 ````
 
 (after)
 ````
 

public class ArrayExamples {

  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i++) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i++) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }

  // Averages the numbers in the array (takes the mean), but leaves out the
  // lowest number when calculating. Returns 0 if there are no elements or just
  // 1 element in the array
  static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }

}

 ````
 
 Symtoms after dubugging (same input as before)
  ````
MacBook-Air-33:lab3-1 ethanluong$ javac ArrayExamples.java
MacBook-Air-33:lab3-1 ethanluong$ javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
MacBook-Air-33:lab3-1 ethanluong$ java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests
JUnit version 4.13.2
....
Time: 0.002

OK (4 tests)
   ````
 
 
 
 

##Part 3 (Reflection)
 
 Learning how to create local and remote servers was really intersting. Understanding how paths and the terminolgy being websites is something useful that I learned too. 
 Learning more about junit and the process of testing is something that I learned that has been usefull for this class and cse 12.

