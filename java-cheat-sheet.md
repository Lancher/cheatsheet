#### Run and Compile .java
```
>> javac One.java                           // create One.class
>> java One                                 // run bytecode One.class
>> jar -cvfe One.jar One One.class          // create jar file with Main entry
>> jar -cvfm One.jar Manifest.txt One.class // create jar file with manifest
>> java -jar One.jar                        // run .jar
```
```
// One.java
public class One {
  public static void main(String [] args) {
    System.out.println("Print One");
  }
}
```
```
// manifest.txt
Main-Class: One
```

#### Basics
```
// enum
enum Color { RED, BLUE, GREEN }
Color c = Color.RED
Color arr[] = Color.values()    // .values() return all elements in enum
c.ordinal()                     // .ordinal() return index in enum



```
