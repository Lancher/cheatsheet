### Run & Compile .java
```
>> javac One.java                           // 1. create One.class
>> java One                                 // 2. run bytecode One.class
>> jar -cvfe One.jar One One.class          // 3.(a) create jar file, jar -cvfe [Output Jar] [Main Class] [Related Classes]
>> jar -cvfm One.jar Manifest.txt One.class // 3.(b) create jar file with manifest, jar -cvfm [Output Jar] [Manifest File] [Related Classes]
>> java -jar One.jar                        // 4. run .jar, 

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