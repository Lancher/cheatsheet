### Run .java and compress .jar
```bash
>> javac One.java                           // create One.class
>> java One                                 // run bytecode One.class
>> jar -cvfe One.jar One One.class          // create jar file from Main entry
>> jar -cvfm One.jar Manifest.txt One.class // create jar file from manifest
>> java -jar One.jar                        // run .jar
```
```java
// One.java
public class One {
  public static void main(String [] args) {
    System.out.println("Print One");
  }
}
```
```txt
// manifest.txt
Main-Class: One
```

### Data Types 
```java
// enum
enum Color { RED, BLUE, GREEN }
Color c = Color.RED
Color arr[] = Color.values()                 // .values() return all elements in enum
c.ordinal()                                  // .ordinal() return index in enum

// numbers
int i = 5000;
float gpa = 13.65;
double mask = 0xaf;
Float f = new Float(1.23f);
System.out.println(f.toString());           // .toString() in number object 

// characters
char ch = 'a';
char uniChar = '\u039A';                    // Unicode for uppercase Greek omega character
char[] charArray ={ 'a', 'b', 'c', 'd', 'e' }

// strings
String str1 = "Hello";
String str2 = "World";
System.out.println(str1.concat(str2));      // .concat()
System.out.println(str1 + str2);            // concatenate with +

// arrays
int [] nums = {10, 8, 7, 20, 39, -1}
int [] nums = new int [] {10, 8, 7, 20, 39, -1}
int [] nums = new int [6]                   // init with size 6 and all zeros
nums[1] = 1000 
nums.length                                 // .length
```

### Flows 
```java
// for loop
int [] nums = {10, 8, 7, 20, 39, -1}
for (int i = 0; i < nums.length; i++) { System.out.println(nums[i]); } 
for (int num: nums) { System.out.println(num); } 

// while loop
while (1) { System.out.println("Hello World"); }
for (;;) { System.out.println("Hello World"); }

// switch
char C = 'B';
switch (grade) {
  case 'A' :
    System.out.println("Excellent!"); 
    break;
 case 'B' :
    System.out.println("Good Job");
    break;
 default :
    System.out.println("Invalid grade");
}
```

### Array
```java
// array initialize
int [] nums = {10, 8, 7, 20, 39, -1}
int [] nums = new int [] {10, 8, 7, 20, 39, -1}
int [] nums = new int [6]

// array methods
int [] arr1 = {1, 2, 3} 
int [] arr2 = {1, 2, 3}
int [] arr = {4, 6, 1, 8, 3, 9, 7, 4, 2}
arr1 == arr2                                // is false
arr1.equals(arr2)                           // is false
Arrays.equals(arr1, arr2)                   // is true
Arrays.deepEquals(arr1, arr2)               // is true, nesting compares
Arrays.toString(arr1)                       // .toString() covert to string
Array.sort(arr)                             // .sort() to sort array                            
Array.sort(arr, 0, 2)                       // .sort(array, 0, 2) first 2 elements
int idx = Arrays.binarySearch(arr, 9)       // return -1 if not found                             
int [] cp = Arrays.copyOf(arr, arr.length)  // return identical new array
int [] cp = Arrays.copyOfRange(arr, 1, 5)   // return new array from 0 to 4
Arrays.fill(arr, 0, 3, -1);                 // fill 0 to 2 with -1
Arrays.fill(arr, -1);                       // fill all elements with -1
```

### String / String Buffer(synchronized) / StringBuilder(not synchronized)
```java
// string initialize
String s1 = "HelloWorld";
String s2 = new String("HelloWorld");


// string methods
s.length()                                  // .length()
s.charAt(3)                                 // .charAt() return 'l'
s.substring(3)                              // .substring() return substring form index i
s.substring(2, 5)                           // .substring() return substring from i to j
String s3 = s1.concat(s2);                  // .concat() return "HelloWorld"
int idx = s.indexOf("Share")                // .indexOf() return first occurrence
int idx = s.indexOf("a",3)                  // .indexOf() return first occurrence from index i
int idx = s.lastindexOf("a",3)              // .indexOf() return last occurrence
"abc".equals("abc")                         // .equals() compare two strings
"abc".equalsIgnoreCase("abc")               // .equalsIgnoreCase() compare two strings
s1.compareTo(s2)                            // .compareTo() compare with lexicographically return 0, 1, -1
s.toLowerCase()                             // .toLowerCase() to lower
s.toUpperCase()                             // .toUpperCase() to upper
s.trim()                                    // .trim() return string by removing whitespaces at both ends
s.replace('a', 'b')                         // .replace() return string by replacing all occurrences of oldChar with newChar.
String str3 = String.valueOf(1234)          // convert int to string
int i = Integer.parseInt("+20")             // convert string to int
String [] arrOfStr = str.split("@", 2)      // limit to array length with 2

// string buffer initialize
StringBuffer s = new StringBuffer()         // default is 16 characters
StringBuffer s = new StringBuffer(20)       // init with 20 size
StringBuffer s = new StringBuffer("Hello")  // init with String

// string buffer methods
s.length()                                  // current length of string
s.capacity()                                // total allocation
s.append("~~")                              // .append(), append string to the end
s.insert(5, "~~")                           // .insert(), insert string at index 5
s.reverse()                                 // .reverse(), reverse the string in-place
s.delete(0, 5)                              // delete(), delete from 0 to 4
s.deleteCharAt(3)                           // deleteCharAt(), delete at character at index
s.replace(5, 8, "~~~")                      // replace(), replace with string

// string compares
s.equals("Hello")                           // compare values
s == "Hello"                                // compare references
s.compareTo("Hello")                        // .compareTo() compare with lexicographically return 0, 1, -1
// 
```

### Class
```java
// class nested in class, nested class can access all instances in outer scopes.
class OuterClass { 
    static int outer_x = 10;
    int outer_y = 20;
    private int outer_private = 30;
     
    class InnerClass {
        void display() {
            System.out.println("outer_x = " + outer_x);
            System.out.println("outer_y = " + outer_y);
            System.out.println("outer_private = " + outer_private);
        }
    }
}

// static class nested in class,  staitc nested class can only access staitc instances in outer scopes.
class OuterClass { 
    static int outer_x = 10;
    int outer_y = 20;
    private static int outer_private = 30;
     
    static class StaticNestedClass {
        void display() {
            System.out.println("outer_x = " + outer_x);
            System.out.println("outer_private = " + outer_private);
            // System.out.println("outer_y = " + outer_y);         
        }
    }
}
```

### Abstract 
```java
// one abstract method found, then the class must be abstract
abstract class Base {
    absract void method ();
}

// chain abstract class, from Base -> Derived
abstract class Base {
    abstract void method ();
}
abstract class Derived {
    abstract void method ();
}

// Derived is not abstract, he must implement the abstract method
abstract class Base {
    abstract void method ();
    void real_method () { System.out.println("Hello Base"); }
}
class Derived {
    void method () { System.out.println("Hello Derived"); }
}
 
 
// abstract class can have both abstract and concrete methods
// abstract class can have protected and public abstract methods
// abstract class can have static, final or static final variable with any access specifier
``` 

### Interface
```java
// class must implement all abstract methods in interface
interface in1 {
    final int a = 10; 
    void display();
}
class testClass implements in1 {
    public void display() {
        System.out.println("Geek");
    }
}

// multiple inheritance only in interface not in abstract
interface Interface1 { 
    default void show () { System.out.println("Default 1"); }
}
interface Interface2 { 
    default void show () { System.out.println("Default 2"); }
}
class MyClass implements Interface1, Interface2 {
    public void show { Interface1.super.show(); Interface2.super.show(); }
}

// anonymous inner class
interface Age {
	int x = 21;
	void getAge();
}
Age oj1 = new Age() {
    @Override
    public void getAge() { System.out.print("Age is "+x); }
};
oj1.getAge();

// interface can only extend another interface
// interface can have only abstract methods
// interface can have only have public abstract methods
// interface can only have public static final (constant) variable
```

### This
```java
// this access class instances and methods
class Apple {
    int a;
    void method1() { this.a = 100; }
    void method2() { this.methid1(); }
}

// this as constructor
class Apple {
    int a, b;
    Apple() { this(10, 30); }
    Apple(int a, int b) { this.a = a; this.b = b; }
}
```

### Super
```java
// print the 120 
class Vechile { 
    int maxSpeed = 120;
    void message() { System.out.Println("Hello Vechile"); } 
}
class Car extend Vechile { 
    int maxSpeed = 160;
    void show() { System.out.println(super.maxSpeed); super.message(); } 
}

// static method can not call non-static memthod.
// non-static method can not update static variable.
```

### Final
```java
// final variables => create constant variables
// final methods => prevent method overriding
// final classes => prevent inheritance
```

### Overload
```java
// compile time (static) polymorphism
class Sum {
    public int sum(int x, int y) { return x + y; }
    public int sum(int x, int y, int z) { return x + y + z; }
    public double sum(double x, double y) { return x + y; }
}
```

### Override
```java
// run time (dynamic) polymorphism

// override equals() and toString(), the annotation @Override is not neccessary
class Complex {
    private int a, b;
    
    @Override 
    public boolean equals(O) {
        if (this == o) { return true; }
        if (!(o instanceof Complex)) { return false; }
        Complex c = (Complex) o;
        return this.a == o.a && this.b == o.b;
    }
    
    @Overide
    public String toString() { return "a is " + this.a + ", b is " + this.b; }
}
```

### Constructor
```java
// default contructor will be created automatically, if no contructor found
class Test {
    int a, b;
} 
Test t = new Test();

// Copy Contructor
class Complex {
    private int a, b;
    
    Complex(Complex c) { this.a = c.a; this.b = c.b; }
    
    @Overide
    public String toString() { return "a is " + this.a + ", b is " + this.b; }
}
Complex c3 = c2;

// private contructor - singleton
class Singleton {
    static Singleton instance = null;
    private Singleton() {}
    
    static public Singleton get_instance() {
        if (instance == null) instance = new Singleton();
        return instance;
    }
}
```

### Exception
```java
// catch and print exception 
try { int a = 20 / 0; }
catch (Exception e) { e.printStackTrace(); Sysytem.out.println(e); }
finally { System.out.println(e); }

// throw exception
try { throw new NullPointerException("demo"); }
catch(NullPointerException e) { System.out.println("Caught inside fun()."); }

// custom exception with passing strings
class MyException extend Exception {
    public MyException(String s) {
        super(s);
    }
} 
```

### MultiThreading
```java
// extending the Thread class 
class MyThread extends Thread {
    public void run() {
        System.out.println ("Thread " + Thread.currentThread().getId() + " is running"); 
    }
}
MyThread t = new MyThread();
t.start();

// implementing the Runnable Interface
class MyThread implements Runnable {
    public void run() {
        System.out.println ("Thread " + Thread.currentThread().getId() + " is running"); 
    }
}
Thread t = new Thread(new MyThread());
t.start();

// sychronized block ensures only one thread running at a time.
sychronized(this) {}

// set priority for threads (from 1 ~ 10)
t.setPriority(2);
```

### Garbage Collector
```java
// 1. Garbage Collector is to free heap memory by destroying unreachable objects.
// 2. Use `System.gc() ` or `Runtime.getRuntime().gc()` ro run garbage collection.
// 3. Override the `protected void finalize() throws Throwable` to perform cleanups.
```

### Collections
```java
// ArraryList, dynamic array, not synchronized
ArrayList<Integer> arr = new ArrayList<Integer>(n);
arrli.add(1);

// LinkedList, double linkedlist
LinkedList<String> list = new LinkedList<String>();
list.add("Hello");
list.add(2, "E");
list.addLast("C");
list.addFirst("D");
list.remove("Hello");
list.remove(3);
list.removeFirst();
list.removeLast();

// Vector, dynamic array, synchronized
Vector v = new Vector();
v.add(1);
v.add(2);
v.add("geeks");
v.add("forGeeks");

// Stack
Stack<Integer> stack = new Stack<Integer>();
stack.push(1);
stack.peek();
stack.pop();

// HashSet
HashSet<String> s = new HashSet<String>();
s.add("India");
s.add("Australia");
s.add("South Africa");
s.remove("Australia");

// LinkedHashSet
LinkedHashSet<String> s = new LinkedHashSet<String>();
s.add("A");  
s.add("B");

// TreeSet
TreeSet s = new TreeSet();
s.add("A");
s.add("B");
s.add("C");

// HashMap, array of linked list
HashMap<String, Integer> map = new HashMap<>();
map.put("vishal", 10);
map.clear();

// LinkedHashMap, doubly-linked bucket
LinkedHashMap<String, String> map = new LinkedHashMap<String, String>();
map.put("one", "practice.geeksforgeeks.org");
map.put("two", "code.geeksforgeeks.org");
map.put("four", "quiz.geeksforgeeks.org");

// TreeMap, Red-Black Tree
TreeMap<Integer, Integer> tmap = new TreeMap<Integer, Integer>();
map.put("one", "Hello World");

// PriorityQueue
PriorityQueue<String> pq = new PriorityQueue<String>();
pq.add("C");
pq.add("C++");
pq.add("Java");
pq.add("Python");

// Deque
Deque deque = new LinkedList<>();
deque.add("Element 1 (Tail)"); // add to tail
deque.addFirst("Element 2 (Head)");
deque.addLast("Element 3 (Tail)");
deque.push("Element 4 (Head)"); //add to head
deque.offer("Element 5 (Tail)");
deque.offerFirst("Element 6 (Head)");
deque.offerLast("Element 7 (Tail)");
```

### Generics
```java
// generics class
class Test<T> {
    T obj;
    Test(T obj) { this.obj = obj; }
    public T getObject()  { return this.obj; }
}

// generics method
static <T> void genericDisplay (T element) {
    System.out.println(element.getClass().getName() + " = " + element);
}
```

### Assert
```java
assert value >= 20 : " Underweight";

// by default, assertions are disabled
java –ea Test
java –da Test
```

### Annotation
```java

```








