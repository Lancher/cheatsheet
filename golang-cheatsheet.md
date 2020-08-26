
## Go Materials

`go rpc`: https://pdos.csail.mit.edu/6.824/notes/l-rpc.txt  
`go faq`: https://pdos.csail.mit.edu/6.824/papers/tour-faq.txt

## Goroutine

Use `go` to run asynchro
## Go Command Tool

`go build`: Compiles a bunch of go source code files to a executable.  
`go run`: Compiles and execute one or two files.  
`go fmt`: Format all the code in each file.  
`go install`: Compile and "installs" a package.  
`go get`: Download the raw source code.  
`go test`: Run any test files in current project.

## Packages

Two types of packages:
- Executable Package (`package main`) and must have function `main()`.
- Reusable Package (`package xxxxx`).

## Common Import

```
import "math"
import "strings"
import "sort"
import "strconv"
```

## Variables

Use `var` to initialize variables.

```
var i int = 0
```

`:=` is initialization + assignment.

```
card := "Hello World"
card = "New Hello World"
a, b, c := 1, 2, 3
```

constant string

```
const s string = "constant"
```

## For

Iterate the for loop.

```
for i := 7; i <= 9; i++ {
    fmt.Println(i)
}
```

Simulate the while loop.

```
for {
    fmt.Println("loop")
    break
}
```

## Division

```
 fmt.Println(10 / 3)  // = 3
```

## Min/Max

```
Use if else to find min/max
```

## Array & Slice & Map

`Array` is fixed length array:

```
var a [4]int
b := [2]string{"Penn", "Teller"}
b := [...]string{"Penn", "Teller"}
```

`Slice` is initialized without fixed array length:

```
letters := []string{"a", "b", "c", "d"}
s = make([]byte, 5, 5)
s := make([]byte, 5)
```

2D slice:

```
2d := [][]string{}
2d = append(2d, []string{"a", "b"})
```

1D slice to 2D slice:

```
d1 := []string{"a", "b", "c", "d", "e"}
d2 := [][]string{}
d2 = append(d2, d1)
fmt.Println("Original 2D Array")
fmt.Println(d2)
fmt.Println("Original 2D Array - Update 1D 0 Element")
d1[0] = "1"
fmt.Println(d1)
fmt.Println(d2)
fmt.Println("Original 2D Array - Delete 1D Last Element")
d1 = d1[:len(d1)-1]
fmt.Println(d2)
fmt.Println("Original 2D Array - Update 1D 3th Element")
d1[3] = "?"
fmt.Println(d2)
fmt.Println("Original 2D Array - Append 1D Last Element")
d1 = append(d1, "@")
fmt.Println(d2)

// output
Original 2D Array
[[a b c d e]]
Original 2D Array - Update 1D 0 Element
[1 b c d e]
[[1 b c d e]]
Original 2D Array - Delete 1D Last Element
[[1 b c d e]]
Original 2D Array - Update 1D 3th Element
[[1 b c ? e]]
Original 2D Array - Append 1D Last Element
[[1 b c ? @]]
```

Pass slice as argument:

```
https://nanxiao.gitbooks.io/golang-101-hacks/content/posts/pass-slice-as-a-function-argument.html
```

Get the length and capacity of slice & array:

```
len(s) == 5
cap(s) == 5
```

`Slice` is a descriptor of an array segment. It consists of a pointer to the array, the length of the segment, and its
capacity (the maximum length of the segment):

```
b := []byte{'g', 'o', 'l', 'a', 'n', 'g'}
a := b[2:]
a[0] = 115
fmt.Println(b) // [103 111 115 97 110 103]
```

Use `copy(dst, src)` to copy minimum length of slices:

```
a := []byte{'g', 'o', 'l', 'a', 'n', 'g'}
b := make([]byte, len(a))
copy(b, a)
```

Only `slice` can be invoked in `append(slice, ...)`:

```
a := []byte{'g', 'o', 'l', 'a', 'n', 'g'}
a = append(a, 100, 100)
```

`Map` is a key-value storage:

```
m := make(map[string]int)
n := map[string]int{"foo": 1, "bar": 2}
```

Slice in a map:

```
m := make(map[string][]string)
m["yes"] = append(m["yes"], "no")
```

Delete a key in map:

```
delete(m, "k2")
```

Detect if an key inside ``:

```
if value, ok := dict["baz"]; ok {
    fmt.Println("value: ", value)
} else {
    fmt.Println("key not found")
}
```

## Comparison

Check if a number between 100 and 1001

```
if 100 <= a && a <= 1001 { fmtPrintln("between 100~1001") }
```



## Range

Iterate array or slice:

```
for _, num := range nums {
    sum += num
}
```

```
for k, v := range m {
  fmt.Printf("%s -> %s\n", k, v)
}
```

## Function

Data type is at the end of function:

```
func sum(a int, b int, c int) int {
    return a + b + c
}
func sum(a, b, c int) int {
    return a + b + c
}
```

Multiple return values:

```
func vals() (int, int) {
    return 3, 7
}
a, b := vals()
```

Variadic Functions:

```
func sum(nums ...int) {
    total := 0
    for _, num := range nums {
        total += num
    }
    fmt.Println(total)
}
```

## Closure

Anonymous functions, which can form closures.

```
func intSeq() func() int {
    i := 0
    return func() int {
        i++
        return i
    }
}
```

## Pointer

```
i := 0
func zeroptr(iptr *int) {
    *iptr = 0
}
fmt.Println(&i)
```

## Struct & Methods

The `Struct` is the collections of elements:

```
type person struct {
    name string
    age  int
}
p = person{"Bob", 20}
pp := &s
fmt.Println(p.age)
fmt.Println(pp.age)
```

Pass `pointer` to avoid copy new item and pass `value` to allow mutate:

```
type rect struct {
    width, height int
}

func (r *rect) area() (int, int) {
    return r.width * r.height, -1
}

func (r rect) perim() int {
    return 2*r.width + 2*r.height
}
```

## Interface

Use `interface` to represent a group of struct:

```
type Animal interface {
	Speak() string
}

type Dog struct {
}

func (d Dog) Speak() string {
	return "Woof!"
}

type Cat struct {
}

func (c Cat) Speak() string {
	return "Meow!"
}

func main() {
	animals := []Animal{Dog{}, Cat{}}
	for _, animal := range animals {
		fmt.Println(animal.Speak())
	}
}
```

## Error

How errors return:

```
f, err := os.Open("filename.ext")
if err != nil {
    log.Fatal(err)
}
```

Construct your error by:

```
import "errors"
func f() (int, error) {
    return -1, errors.New("can't work with 42")
}
```

## Goroutine

Use `go` to run asynchronous tasks:

```
func f(from string) {
    for i := 0; i < 3; i++ {
        fmt.Println(from, ":", i)
    }
}

go f("goroutine")
```

Run `go` with anonymous function:

```
go func(msg string) {
    fmt.Println(msg)
}("going")
```

## channel

Non-buffered channels block. Read blocks when no value is available, write blocks until there is a read.

```
ch := make(chan int)
ch <- 42
v := <-ch
```

Create a buffered channel. Writing to a buffered channels does not block if less than <buffer size>.

```
ch := make(chan int, 100)
```

Close the channel by sender.

```
close(ch)       //  close
v, ok := <-ch   //  receiver check if closed
```

Use `select` to monitor asychronous  



## Type

`type` is to declare the one type as another type:

```
type string_slice [] string
```

## Type as Callback function

```
type foo func(string, string) string

func bar(route string, io foo) {
    response := io("param", "param")
}

bar("Hello", func(arg1, arg2 string) string {
    return arg1 + arg2
})
```

## Method

Pass `pointer` to avoid copy new item and pass `value` to allow mutate:

```
type rect struct {
    width, height int
}

func (r *rect) area() int {
    return r.width * r.height
}

func (r rect) perim() int {
    return 2*r.width + 2*r.height
}
```

## Multiple Return Value

The syntax is like Python.

```
func re (int, int) {
    return 1, 2
}
a, b = re()
```

## Type Conversion

Transform to string.

```
[]byte("Hi there")
```

nous tasks:

```
func f(from string) {
    for i := 0; i < 3; i++ {
        fmt.Println(from, ":", i)
    }
}

go f("goroutine")
```

Run `go` with anonymous function:

```
go func(msg string) {
    fmt.Println(msg)
}("going")
```

## channel

Non-buffered channels block. Read blocks when no value is available, write blocks until there is a read.

```
ch := make(chan int)
ch <- 42
v := <-ch
```

Create a buffered channel. Writing to a buffered channels does not block if less than <buffer size>.

```
ch := make(chan int, 100)
```

Close the channel by sender.

```
close(ch)       //  close
v, ok := <-ch   //  receiver check if closed
```

Only the closed channel can be iterated:

```
queue := make(chan string, 2)
close(queue)
```

Use `select` to monitor asynchronous channels:

```
select {
    case channelOut <- 42:
        fmt.Println("We could write to channelOut!")
    case x := <- channelIn:
        fmt.Println("We could read from channelIn")
    case <-time.After(time.Second * 1):
        fmt.Println("timeout")
}
```  

Use `channel` to synchronize:

```
done := make(chan bool, 1)
<-done
```

Use `select` with timeout:

```
import "time"
select {
case res := <-c1:
    fmt.Println(res)
case <-time.After(1 * time.Second):
    fmt.Println("timeout 1")
}
```

We can use select with a `default` clause to implement non-blocking sends, receives, and even non-blocking multi-way
selects.

```
select {
case msg := <-messages:
    fmt.Println("received message", msg)
default:
    fmt.Println("no message received")
}
```


## Timer

Sleep 1s:

```
import "time"
timer1 := time.NewTimer(2 * time.Second)
```

Stop timer:

```
import "time"
timer2 := time.NewTimer(time.Second)
go func() {
    <-timer2.C
    fmt.Println("Timer 2 expired")
}()
stop2 := timer2.Stop()
```

Use ticker to execute periodically events:

```
import "time"
ticker := time.NewTicker(500 * time.Millisecond)
for t := range ticker.C {
    fmt.Println("Tick at", t)
}
```

## Mutex

```
var mutex = &sync.Mutex{}
mutex.Lock()
mutex.Unlock()
```

## Sort

Sort the slice or array:

```
strs := []string{"c", "a", "b"}
sort.Strings(strs)

ints := []int{7, 2, 4}
sort.Ints(ints)
```

Sort by custom function:

```
type byLength []string

func (s byLength) Len() int {
    return len(s)
}
func (s byLength) Swap(i, j int) {
    s[i], s[j] = s[j], s[i]
}
func (s byLength) Less(i, j int) bool {
    return len(s[i]) < len(s[j])
}

fruits := []string{"peach", "banana", "kiwi"}
sort.Sort(byLength(fruits))
```

// sort slice
sort.Slice(s[:], func(i, j int) bool {
	return s[i].Lo < s[j].Lo
})

// sort by lex or dict order
sort.Strings(res)
sort.Ints(s)

//
family := []struct {
	Name string
	Age  int
}{
	{"Alice", 23},
	{"David", 2},
	{"Eve", 2},
	{"Bob", 25},
}

// Sort by age, keeping original order or equal elements.
sort.SliceStable(family, func(i, j int) bool {
	return family[i].Age < family[j].Age
})

## Panic

Mostly we use it to fail fast on errors that shouldn’t occur during normal operation.

```
panic("a problem")
```

## Defer

Ensure the cleanup events will happen even there is panic during the function.

```
f := createFile("/tmp/defer.txt")
defer closeFile(f)
writeFile(f)
```

## String Concatenation

Concatenate string literal simply. However, string object is generated for every + is used

```
fmt.Println("Panda " + "is " + "cute.")
```

If bytes.Buffer is used, new object is not generated

```
var buffer bytes.Buffer
buffer.WriteString("P")
buffer.WriteString("a")
buffer.WriteString("n")
fmt.Println(buffer.String())
```

# Substring
str := "Hello World"
subStr := str[1:4]
