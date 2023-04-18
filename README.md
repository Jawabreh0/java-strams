# Java Streams

This repository contains Java code examples that demonstrate how to work with streams. Streams are a powerful and efficient way to process large amounts of data in Java, and can be used for a variety of purposes, such as reading and writing data, filtering and sorting data, and transforming data. The examples in this repository cover basic stream operations, such as creating streams, filtering data, sorting data, and aggregating data, as well as more advanced stream operations, such as parallel streams and collectors.

## Java Files and Streams Summary:

### File Processing

 * Storing and manipulating data using files is known as file processing
 * Reading/Writing of data in a file can be performed at the level of bytes, characters, or fields depending on application requirements.
 * Object Serialization: The process of reading and writing objects
 
 ### Streams
 
 * Java Uses the concept of Streams to represent the ordered sequence of data, a common characteristic shared by all I/O devices
 * Streams presents a uniform, easy to use, object oriented interface between the program and I/O devices
 * A stream in Java is a path along which data flows (like a river or pipe along which water flows)
 
 ![stream-view](stream-view.png)
 
 * The concepts of sending data from one stream to another (like a pipe feeding into another pipe) has made streams powerful tool for file processing.
 * Connecting streams can also act as filters.
 * Streams are classified into two basic types:
    - Input Stream
    - Output Stream 
    
 ### Java Stream Classes
 * Input/Output related classes are defined in java.io package
 * Input/Output in Java is defined in terms of streams
 * A stream is a sequence of data, of no particular length
 * Java I/O classes can be categorised into two groups based on the data type one which they operate:
     - Byte Stream
     - Character Stream
 
 ### Java Stream Classes
 
 ![classification-of-java-stream-classes](classification-of-java-stream-class.png)
 
 * File class is not for the contents of a file, but the file object

### Java.io.File methods
 * getName()
 * getPath()
 * getAbsolutePath()
 * getParent()
 * isAbsolute()
 * lastModified()
 * IsFile()
 * isDirectory()
 * canRead()
 * canWrite()
 
 ## BYTE INPUT/OUTPUT
 
 ### Reading/Writing Bytes
 
 As most file systems use only 8-bit bytes, Java supports number of classes that can handle bytes. The two most commonly used classes for handling bytes are:
* FileInputStream
* FileOutputStream

### Byte Input Stream - example
Count total number of bytes in the file
```java
// Import the required Java classes for input and output
import java.io.*;

// Define a class called CountBytes
// Import the required Java classes for input and output
import java.io.*;

// Define a class called Main
class Main {
  
  // Define the main method with exception handling
  public static void main(String[] args) throws FileNotFoundException, IOException {
  
    // Declare a variable of type FileInputStream
    FileInputStream in;
    
    // Initialize the FileInputStream object with the input file "/home/jawabreh/Desktop/Java/testFile-one.txt"
    in = new FileInputStream("/home/jawabreh/Desktop/Java/testFile-one.txt");
    
    // Declare and initialize a variable called "total" to count the number of bytes in the input file
    int total = 0;
    
    // Read the input file byte by byte until the end of the file is reached
    while (in.read() != -1) {
      total++;
    }
    
    // Print the total number of bytes in the input file to the console
    System.out.println("The total number of bytes is :" + total);
    
    // Close the input stream to release any system resources
    in.close();
  }}
```
### Byte Output Stream - example
Write Jerusalem , Qudus into file using FileOutputStram
```java
// Import the required Java classes for file output and exception handling
import java.io.FileOutputStream;
import java.io.IOException;

// Define a class called Main
public class Main {
  
  // Define the main method
  public static void main(String[] args) {
    
    // Declare an array of bytes representing the names of two cities
    byte cities[] = {'J', 'E', 'R', 'U', 'S', 'A', 'E', 'M', '\n', 'Q', 'U', 'D', 'U', 'S'};
    
    // Declare a variable of type FileOutputStream
    FileOutputStream out;
    
    try {
      // Initialize the FileOutputStream object with the output file "Cities.txt"
      out = new FileOutputStream("Cities.txt");
      
      // Write the byte array "cities" to the output file
      out.write(cities);
      
      // Print a message to the console indicating that the writing operation is complete
      System.out.println("DONE");
      
      // Close the output stream to release any system resources
      out.close();
    }
    // Catch any IO exceptions that may be thrown by the FileOutputStream object
    catch (IOException e) {
      e.printStackTrace();
    }
  }
}
```
