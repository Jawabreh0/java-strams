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

## CHARACTER INPUT/OUTPUT

### Reading and Writing Characters

* As pointed out earlier, subclasses of Reader and Writer implement streams that can handle characters
* The two subclasses used for handling characters in file are:
    - FileReader
    - FileWriter
* Remember, while opening a file, we can pass either file name or File object during the creation of objects of the above classes.

### Reader Class (FileReader)

#### Reader Class example
Count total number of spaces in the file
```java
// Import the required Java classes for file input and exception handling
import java.io.FileReader;
import java.io.IOException;

// Define a class called Main
public class Main {
  
  // Define the main method and indicate that it may throw an IOException
  public static void main(String[] args) throws IOException {
    
    // Declare a variable of type FileReader and initialize it with the input file "testFile-one.txt"
    FileReader in;
    in = new FileReader("/home/jawabreh/Desktop/Java/testFile-one.txt");
    
    // Declare variables to keep track of the total number of characters and white spaces
    int ch, total, spaces;
    spaces = 0;
    
    // Use a for loop to read each character of the input file
    for (total = 0; (ch = in.read()) != -1; total++) {
      
      // Check if the current character is a white space
      if (Character.isWhitespace((char) ch))
        spaces++; // If so, increment the counter for white spaces
    }
    
    // Print the total number of white spaces to the console
    System.out.println("Total number of white spaces is: " + spaces);
    
    // Close the input stream to release any system resources
    in.close();
  }
}
```
#### Reader Class example
Read File Content using FileReader (Reader Class)
here there are two solutions, first by providing file as object, second by directly the file name as string

Solution using file object
```java
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;

public class Main {
    public static void main(String[] args) {
        FileReader in = null;

        try {
            in = new FileReader("/home/jawabreh/Desktop/Java/testFile-one.txt");
            int data;
            while ((data = in.read()) != -1){
                System.out.println((char) data);
            }
        }
        catch (FileNotFoundException e){
            e.printStackTrace();
        }
        catch (IOException e){
            e.printStackTrace();
        }
        finally {
            try {
                if (in != null) {
                    in.close();
                }
            }
            catch (IOException e){
                e.printStackTrace();
            }
        }
    }
}
```

By providing file as string 
```java
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;

public class asString {
    public static void main(String[] args) {
        String fileName = "/home/jawabreh/Desktop/Java/testFile-one.txt";
        FileReader readFile = null;

        try {
            readFile = new FileReader(fileName);
            int data;
            while ((data = readFile.read()) != -1) {
                System.out.println((char) data);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (readFile != null) {
                    readFile.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```
### Writer Class (FileWriter)

* FileWriter is a character stream writer

#### Example of writing file using FileWriter

```java
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;

public class Main {
    public static void main(String[] args) {
        File file = new File("createdFile");

        FileWriter fr = nulll;

        try{
            fr = new FileWriter(file);
            fr.write('A');
            fr.write(67);
            fr.write("456");
        }
        catch (IOException e){
            e.printStackTrace();
        }
        finally {
            try{
                fr.close();
            }
            catch (IOException e){
                e.printStackTrace();
            }
        }
    }
}
```
## BUFFERED INPUT/OUTPUT

* Java supports creation of buffers to store temporarily data that read from or written to a stream. This process is known as buffered I/O operation.
* Buffered stream classes – BufferedInputStream, BufferedOutputStream, BufferedReader, BufferedWriter buffer data to avoid every read or write going to the stream. (Default buffer size = 8KB)
* Buffered character streams understand lines of text.
* BufferedWriter has a newLine method which writes a new line character to the stream.
* BufferedReader has a readLine method to read a line of text as a String.

#### Example: Use a BufferedReader to read a file one line at a time and print the lines to standard output

```java
import java.io.BufferedReader;
import java.io.FileReader;

public class Main {
    public static void main(String[] args)
    {
        BufferedReader in;
        in = new BufferedReader(new FileReader("file.txt"));

        String line;

        while ((line = in.readLine()) != null)
            System.out.println(line);

        in.close();
    }
}
```
* Wrapping a BufferedReader around a FileReader will result in getting the file contents as a complete string directly.
* As a result you will have to string process what you get to achieve data fields that have different data types

#### Example:

```java
import java.io.BufferedReader;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;

public class Main {
    public static void main(String[] args) {
        String fileName = "FileWanted.txt";
        FileReader readFile = null;
        BufferedReader readStream = null;
        
        try{
            readFile = new FileReader(fileName);
            readStream = new BufferedReader(readFile);
            
            String line;
            
            while ((line = readStream.readLine()) != null)
                System.out.println(line);
        }
        catch (FileNotFoundException e){
            e.printStackTrace();
        }
        catch (IOException e){
            e.printStackTrace();
        }
        finally {
            try {
                readFile.close();
                readStream.close();
            }
            catch (IOException e){
                e.printStackTrace();
            }
        }
    }
}
```
## Scanner to read files (Another Buffered Input)

### Example

```java
import java.io.File;
import java.io.IOException;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        File readFile = new File("/home/jawabreh/Desktop/Java/testFile-one.txt");
        Scanner sc = null;

        try{
            sc = new Scanner(readFile);
            while (sc.hasNext()){
                System.out.print(sc.next() + " ");
                System.out.print(sc.nextDouble() + " ");
                System.out.print(sc.next() + " ");
                System.out.println(sc.nextInt());
            }
        }

        catch (IOException e){
            e.printStackTrace();
        }
        finally {
            if (sc != null) {
                sc.close();
            }
        }
    }
}
```
## Differences Between BufferedReader and Scanner classes
* A scanner is a much more powerful utility than BufferedReader. It can parse the user input and read an int, short, byte, float, long and double apart from String. On the other hand, BufferedReader can only read String in Java.
* BuffredReader has a significantly large buffer (8KB) than Scanner (1KB), which means if you are reading long String from a file, you should use BufferedReader but for short input and input other than String, you can use Scanner class.
* BufferedReader is older than Scanner. It's present in Java from JDK 1.1 onward but Scanner is only introduced in JDK 1.5 release.
* Scanner uses regular expression to read and parse text input. It can accept custom delimiter and parse text into primitive data type e.g. int, long, short, float or double using nextInt(), nextLong(), nextShort(), nextFloat(), and nextDouble() methods, while BufferedReader can only read and store String using readLine() method.
* Another major difference between BufferedReader and Scanner class is that BufferedReader is synchronized while Scanner is not. This means, you cannot share Scanner between multiple threads but you can share the BufferedReader object.

