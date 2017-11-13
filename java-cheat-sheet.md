#### Run and Compile .java
```
>> javac One.java                           // create One.class
>> java One                                 // run bytecode One.class
>> jar -cvfe One.jar One One.class          // create jar file from Main entry
>> jar -cvfm One.jar Manifest.txt One.class // create jar file from manifest
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
Color arr[] = Color.values()                // .values() return all elements in enum
c.ordinal()                                 // .ordinal() return index in enum


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


// numbers
int i = 5000;
float gpa = 13.65;
double mask = 0xaf;
Float f = new Float(1.23f);
System.out.println(f.toString());           // .toString() in number object 


// characters
char ch = 'a';
char uniChar = '\u039A';                    // Unicode for uppercase Greek omega character
char[] charArray ={ 'a', 'b', 'c', 'd', 'e' }; 


// strings
String str1 = "Hello";
String str2 = "World";
System.out.println(str1.concat(str2));      // .concat()
System.out.println(str1 + str2);            // concatenate with +


// arrays
int [] nums = {10, 8, 7, 20, 39, -1};
int [] nums = new int [] {10, 8, 7, 20, 39, -1};
int [] nums = new int [6];                  // init with size 6 and all zeros
nums[1] = 1000;
nums.length                                 // .length
```


#### Array
```
// initialize
int [] nums = {10, 8, 7, 20, 39, -1};
int [] nums = new int [] {10, 8, 7, 20, 39, -1};
int [] nums = new int [6];


// compare
int [] arr1 = {1, 2, 3}; 
int [] arr2 = {1, 2, 3}; 
arr1 == arr2                                // is false
arr1.equals(arr2)                           // is false
Arrays.equals(arr1, arr2)                   // is true
Arrays.deepEquals(arr1, arr2)               // is true, nesting compares


// to string
Arrays.toString(arr1)                       // .toString() covert to string


// sort
int [] arr = {4, 6, 1, 8, 3, 9, 7, 4, 2};
Array.sort(arr)                            
Array.sort(arr, 0, 2)                      // sort first 2 elements
int idx = Arrays.binarySearch(arr, 9)      // return -1 if not found                             


// copy
int [] cp = Arrays.copyOf(arr, arr.length);
int [] cp = Arrays.copyOfRange(arr, 1, 5);


// fill
Arrays.fill(arr, 0, 3, -1);                 // fill 0 to 2 with -1
Arrays.fill(arr, -1);                       // fill all elements with -1
```






















