

## Check version and if installed
```
go version
```


## Go Workspace and GOPATH

- The Go workspace is the "Home" of go, typically "$HOME/go"
- Installed packages will be installed in "bin" called the GOPATH
```
go env | grep GOPATH
```

## Docs

```
# go doc package function_name
go doc fmt Println
```

## Run code

```
go run codefile.go
```

- Code needs to have a `main` function

```
package main

import "fmt"

func main() {
	fmt.Println("Hello, 世界")
}

```


## TODO: Version Management
## TODO: Dependency Management

## Syntax
- Semicolons at end of line are optional
- {} Brackets / Parenthesis are used for scoping (not indentation)

## Spacing / Indentation

- No semantically significant whitespace (unlike Python)
 blocks instead of curly brackets.
- Indentation and visual order is high regarded: `gofmt` can be used to format a file


## Packages

- Every Go program is made up of packages.
- Programs start running in package main. 
- Using code in other packages: `import` package 
```
import "fmt"
import "math"
```
- Alternatively use parenthesized, "factored" import statement (recommended)
```
import (
	"fmt"
	"math/rand"
)
```

-  A name is exported if it begins with a capital letter `math.Pi`

## Variables

- The `var` statement declares a list of variables; as in function argument lists, the type is last. 

```
var c, python, java bool
var i int
```
-  If an initializer is present, the type can be omitted; the variable will take the type of the initializer. 
```
var i, j int = 1, 2
var c, python, java = true, false, "no!"
```
-  Inside a function, the := short assignment statement can be used in place of a var declaration with implicit type. 
```
k := 3
c, python, java := true, false, "no!"
```
-  Outside a function, every statement begins with a keyword (var, func, and so on) and so the := construct is not available. 

### Variable Types

```
bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8, represents a single ASCII character

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128
```

-  The int, uint, and uintptr types are usually 32 bits wide on 32-bit systems and 64 bits wide on 64-bit systems. When you need an integer value you should use int unless you have a specific reason to use a sized or unsigned integer type. 

### Variable Zero Types

-  Variables declared without an explicit initial value are given their zero value. 

```
 The zero value is:

    0 for numeric types,
    false for the boolean type, and
    "" (the empty string) for strings.
```

### Variable Type conversion

- The expression `T(v)` converts the value `v` to the type `T`. 
```
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)


i := 42
f := float64(i)
u := uint(f)
```

- Declaring a variable without specifying an explicit type (either by using the `:=` syntax or var = expression syntax), the variable's type is inferred from the value on the right hand side.

```
var i int
j := i // j is an int
```

## Constants

- Use `const`
- Cannot be declared using the `:=` syntax. 

```
const Pi = 3.14
```

## Functions

```
package main

import "fmt"

func add(x int, y int) int {
	return x + y
}

// func add(x, y int) int { // type can be omited if it is the same, only specify the last occurence
// 	return x + y
// }


func main() {
	fmt.Println(add(42, 13))
}
```

### Returning multiple values

```
package main

import "fmt"

func swap(x, y string) (string, string) {
	return y, x
}

func main() {
	a, b := swap("hello", "world")
	fmt.Println(a, b)
}
```

### Named returned values and "naked" returns

- Go's return values may be named. If so, they are treated as variables defined at the top of the function.

- These names should be used to document the meaning of the return values.

- A return statement without arguments returns the named return values. This is known as a "naked" return. 

```
func split(sum int) (x, y int) {
	x = sum * 4 / 9
	y = sum - x
	return
}
```

### defer
-  A defer statement defers the execution of a function until the surrounding function returns. 
-  Deferred function calls are pushed onto a stack. When a function returns, its deferred calls are executed in last-in-first-out order. 
```
func main() {
	defer fmt.Println("world")

	fmt.Println("hello")
}
```

## Loops


```
sum := 0
for i := 0; i < 10; i++ {
	sum += i
}
```
-  The init and post statements are optional. 

```
sum := 1

for ; sum < 1000; {
	sum += sum
}

// or even
for sum < 1000 {
	sum += sum
}
```

## Conditional / Control flow

### Boolean Operators

```
true && true  //true
true && false //false
true || false // true
false || false //false
!true  //false
!false //true
```

### if
-  Go's if statements are like its for loops; the expression need not be surrounded by parentheses ( ) but the braces { } are required. 
```
	if x < 0 {
		return sqrt(-x) + "i"
	}
	else if y > 2 {
		return "def"
	}
	else {
		return "abc"
	}
```
-  Like for, the if statement can start with a short statement to execute before the condition. 
-  Variables declared by the statement are only in scope until the end of the if. 
```
	if v := math.Pow(x, n); v < lim {
		return v
	}
```

### switch
- Go only runs the selected case, not all the cases that follow. So `break` used in other languages e.g. C / Javascript is not needed
- Switch cases evaluate cases from top to bottom, stopping when a case succeeds. 
```
	switch os := runtime.GOOS; os {
	case "darwin":
		fmt.Println("OS X.")
	case "linux":
		fmt.Println("Linux.")
	default:
		// freebsd, openbsd,
		// plan9, windows...
		fmt.Printf("%s.\n", os)
	}
```

### range

```
ids := []int{1,3123,42,123,3}

for i, id := range ids {
	fmt.printf("%d - ID: %d\n", i, id)
}
```


## Install package

```
go get path_to_install

go install golang.org/x/website/tour@latest
```


## Strings


- Strings are immutable, so you cannot update the value of a string.
```
  var first = "test"
  var second = first
  first = "another test"
  first  //"another test"
  second //"test"
```

### String Functions
```
var name = "test"

len(name) //4 

name[0] //"t" (indexes start at 0)
name[1] //"e"  

name[0:2] //"te"
name[:2]  //"te"

var newstring = name[:] // copy a string

strings.ToUpper() returns a new string, uppercase
strings.ToLower() returns a new string, lowercase
strings.HasSuffix() checks if a string ends with a substring
strings.HasPrefix() checks if a string starts with a substring
strings.Contains() checks if a string contains a substring strings.Count() counts how many times a substring
appears in a string
strings.Join()usedtojoinmultiplestringsandcreatea new one
strings.Split()usedtocreateanarrayofstringsfroma string, dividing the original one on a specific character, like a comma or a space
strings.ReplaceAll() used to replace a portion in a string and replace it with a new one
  
```

## Arrays

- An array can only contain values of the same type.
- Fixed length
- Slices typically used instead due to these restrictions

```
var arrayVariable [2]string
arrayVariable[0] = "1"
arrayVariable[1] = "abcd"

var myArray = [3]string{"First", "Second", "Third"}
var myArray = [...]string{"First", "Second", "Third"}

// arrayVariable := [2]string("1", "abcd") // alternatively
```
## Slices
- like arrays but length can change

```
aSlice = []int{-3, -2, -1, 0, 1, 2, 3}
aSlice = append(aSlice, 4)

mySlice := make([]string, 3) //a slice of 3 empty strings
```


## Maps / Key Value pairs

```
emails := make(map[string]string)
emails["bob"] = "bob@example.com"
emails["brad"] = "brad@example.com"
emails := map[string]string{["bob" : "bob@example.com", "brad": "brad@examplecom"}

agesMap := make(map[string]int)
agesMap["flavio"] = 39
agesMap := map[string]int{"flavio": 39}
```

### Functions

```
len(emails)
delete(emails, "brad")
```

## Pointers


```
a := 5
b := &a
fmt.Println(b)  // addreses value
fmt.Println(a)  // 5 
fmt.Println(*b) // 5 
b := 10
fmt.Println(a)  // 10
fmt.Println(*b) // 10
```

## Closures

```
func adder() func(int) int {
	sum := 0 
	return function(x int) int {
		sum += x
		return sum
	}
}

func main(){
	sum := adder()
	for i := 0 i < 10; i++ {
		fmt.Println(sum(i))
	}
}
```

## Structs

- A type that contains one or more variables/fields which can have different types (a collection of variables)
- No classes in Go, so is the equivalent
```
type Person struct {
	fname string
	lname string
	age int
}

// alternatively
type Person struct {
	fname, lname string
	age int
}

// value reciever: access data
func (p Person) greet() string {
	return "Hi, I am " + p.fname + " " + p.lname
}

// pointer receiver: changes data
func (p *Person) increaseAge() {
	p.age++
}

func main(){
	person1 := Person{fname: "Bob", lname: "Smith", age: 2}
	person2 := Person{"Bob", "Smith", 2}

	fmt.Println(person1.greet()
	fmt.Println(person1.increaseAge())
}
```

## Interfaces

- An interface is a type that defines one or more method signatures
- Methods are not implemented, just their signature: the name, parameter types and return value type.
- Implementation in a separate function

```
type Shape interface {
	area() float
}

type Circle struct {
	x,y, radius float64
}

type Rectangle struct {
	width, heigth float64
}

func (c Circle) area() float64 {
	return math.Pi * c.radius * c.radius
}

func (r Rectangle) area() float64 {
	return r.width * r.height
}

func getArea (s Shape) float64 {
	return s.area()
}

func main(){
	circle := Cirlce (x: 0, y: 0, radius: 4)
	rectangle := Rectangle (width: 4, height: 4)

	fmt.Println(getArea(circle))
	fmt.Println(getArea(rectangle))
}
```



## Math

- `+`, `-`: addition, subtraction
- `*`, `/`, `%`: multiplication, division, modulus/remainder
- `<=`` >=`, `<`, `>`: comparison
- `++` / `--`: increment / decrement
- `==`, `!=`: equality and inequality
- `int` will not automatically be converted if result is non `int`. Will need to convert in order to return proper non truncated result e.g.`float64(i)`

```
	var intVar int = 3

	fmt.Println(3 / 2)
	fmt.Println(3.0 / 2)
	fmt.Println(3 / 2.0)
	fmt.Println(3 * 0.1 / 2)

	fmt.Println(intVar / 2) // 1
	fmt.Println(intVar / 2.0) // 1
	fmt.Println(float64(intVar) / 2) // 1.5
```



## Comments

```
// single line comment

/* multiple line
comment 
*/
```


## TODO: String formatting
## TODO: Read / Writing Paths
## TODO: Read / Writing Files
## TODO: JSON
## TODO: Sorting
## TODO: Pattern Matching and Replacement
## TODO: dates