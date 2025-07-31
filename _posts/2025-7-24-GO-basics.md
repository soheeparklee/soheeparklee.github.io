---
title: Variable/Print/Scanner/Type/Operator/Array/Slice/Function/Mutable
categories: [Golang, Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ main

```GO
package main

import "fmt"

func main() {

}
```

## ✅ Variable

```GO
var name string = "Jack"
var num uint = 123

var simpleName = "Cassy" //implicit type
var simpleNum = 124

number := 6
number = 5 //change number value
```

## ✅ Print

- `%T`: print type
- `%v`: print value
- `%t`: print boolean

- `%b`: print binary
- `%d`: print decimal
- `%f`: print float

- `%s`: print String
- `%9q`: print with 9 padding
- `%09d`: print with 9 padding, but filled with

```GO
fmt.Printf("%T", 10) //print type, int
fmt.Printf("%v", 10) //print value, 10

fmt.Printf("%t", true) //print boolean

fmt.Printf("%b", 1024) //binary representation of 1024
fmt.Printf("%d", 1024) //print base10, 1024

fmt.Printf("%f", 2.44354643) //print float

fmt.Printf("%s", "Hello Go")
fmt.Printf("String: %9q", "Go") //make 9padding, String:      "Go"
fmt.Printf("String: %09d", 45)  //fill padding with 0, String: 000000045
```

## ✅ User Input, Scanner

```GO
//import packages
import (
	"bufio" //for scanner
	"fmt" //for printing
	"os" //for scanner
	"strconv" //text to int
)

scanner := bufio.NewScanner(os.Stdin)  //define scanner
fmt.Println("I was born in: ")
scanner.Scan() //get user input, always in TEXT

input, _ := strconv.ParseInt(scanner.Text(), 10, 64) //change text to int
fmt.Printf("You are %d years old", 2025-input)
```

## ✅ Type assertion

- ☑️ **Check type of this variable**
- only can check type of `interface{}`

```GO
func getType(i interface{}) { //get interface as parameter
	switch v := i.(type) { //get type of interface
	case int:
		fmt.Println("this is int: ", v)
	case string:
		fmt.Println("this is string: ", v)
	default:
		fmt.Println("unknown type")
	}
}

func main() {
	getType(42) //this is int:  42
	getType("hello") //this is string:  hello
}
```

- ☑️ **Check if this interface is a specific type**
- check if interface box is int

```GO
box := interface{}(12) //create interface

retrievedInt, ok := box.(int) //check if interface box is int
	if ok {
		fmt.Println("Retrieved int: ", retrievedInt)
	} else {
		fmt.Println("Value is not an integer")
	}
//result: Retrieved int: 12
```

## ✅ Change type

- ☑️ **TEXT to INT**

```GO
import (
	"strconv" //text to int
)

//get text, change to int input
//change to decimal(10), 64
//if error, do _

input, _ := strconv.ParseInt(text, 10, 64)
```

- ☑️ **INT to Float**

```GO
//change to float64
float64(num)

//change to int
int(num)
```

## ✅ Arithmetic Operator

- only can use arithmetic operators with same type

```GO
var num1 float64 = 8
var num2 int = 4
answer := num1 + float64(num2) //change int to float
```

```GO
string1 := "hello"
string2 := "go"
fmt.Println(string1 + string2)
```

## ✅ Compare

- ☑️ **Compare same type**

```GO
x := 5
y := 6
val := x > y
fmt.Printf("%t", val) //false
```

- ☑️ **Compare String**

```GO
str1 := "a"
str2 := "A"
answer := str1 == str2
fmt.Printf("%t", answer) //false
```

## ✅ AND, OR

- AND: `&&`
- OR: `||`

## ✅ Conditional

```GO
age := 20

if age > 18 {
	fmt.Println("You can watch this movie")
} else if age > 14 {
	fmt.Println("You can watch with a parent")
} else {
	fmt.Println("You cannot watch")
}
```

## ✅ For Loop

- ☑️ **use for like while**

```GO
x := 0
for x < 5 {
	fmt.Println(x)
	x++
}
```

- ☑️ **For Loop**
- result will be same as above

```GO
for i := 0; i < 5; i++ {
	fmt.Println(i)
}
```

## ✅ Switch

- ☑️ **with variable outside**

```GO
x := 3

switch x { //put variable here
case 1, 2, 3, 4, 5, 6, 7:
	fmt.Println("not answer")
case 8, 9:
	fmt.Println("close!")
case 10:
	fmt.Println("answer")
default:
	fmt.Println("no match")
}
```

- ☑️ **with variable inside**

```GO
x := 3

switch { //dont put variable here
case x < 8:
	fmt.Println("not answer")
case x == 8 || x == 9:
	fmt.Println("close!")
case x == 10:
	fmt.Println("answer")
default:
	fmt.Println("no match")
}
```

## ✅ Array

- have to define size of array
- has size inside `[]`
- `pointer`: index, `arr[0]`
- `length`: size of array, how many elements`len(arr)`
- `capacity`: max of how many elements the array can have
- in array, `length` 🟰 `capacity`

- `fmt.Println(arr)`: print all array
- `len(arr)`: get length of array

- ☑️ **Define array**

```GO
var arr [5]int //make array of size 5
arr[0] = 100
fmt.Println(arr) //print all array
fmt.Println(arr[0]) //100
```

```GO
arr := [3]int{1, 2, 3} //make array of size 3, with 1, 2, 3
len(arr) //get length of array
```

- ☑️ **2D array**

Or if you're wrapping the entire code section, just do:

{% raw %}

```go
arr2D := [2][3]int{{1, 2, 3}, {4, 5, 6}}
fmt.Println(arr2D) //print all array
fmt.Println(arr2D[0][1]) //2
```

{% endraw %}

## ✅ Slice

- like a **portion** of array
- do NOT have to define size of slice
- inside `[]` is empty
- `pointer`: tell us location of the first element in the slice
- `length`: size of slice, number of elements in the slice
- `capacity`: how many elements the slice could have if extended until the end of the array

- ☑️ **Create slice from array**

```GO

var x [5]int = [5]int{1, 2, 3, 4, 5} //create array

var s []int = x[:]
//slice does not define size
//copy the array [1 2 3 4 5]
fmt.Println(len(s)) //5

var t []int = x[1:]
//start at pointer one, go to the end of the array
// [2 3 4 5]
fmt.Println(len(t)) //4
fmt.Println(cap(t)) //4

var v []int = x[1:3]
//start at one, finish before 3
// [2 3]
fmt.Println(len(v)) //2
fmt.Println(cap(v)) //4
```

- ☑️ **Slice the slice**

```GO
fmt.Println(v[:cap(v)])
//get slice of slice
//v is [2, 3]
//v[:cap(v)] = v[:4]
//get slice v + extend until the end of array
// [2, 3, 4, 5]
```

- ☑️ **Create, add to slice**

```GO
s := []int{}
s := make([]int, 5) //create empty slice with len, cap 5
```

```GO
var s []int = []int{5, 6, 7, 8, 9} //create a slice with elements
// or
s := []int{5, 6, 7, 8, 9}

s = append(s, 10)
//create a new slice with 10 added to slice s
// [5 6 7 8 9 10]
```

## ✅ Range

- ☑️ **i: index, element: element of index**

```GO
//index: i element: element at that index
var a []int = []int{1, 3, 4}

for i, element := range arr {
	fmt.Printf("%d: %d\n", i, element)
}
// 0: 1
// 1: 3
// 2: 4
```

- ☑️ **if index is not needed, use** `_`

```GO
for _, element := range arr {
	fmt.Println(element)
}
```

- ☑️ **use Range and For together**

```GO
	for i, element1 := range arr {
		for j := i + 1; j < len(arr); j++ {
			if element1 == arr[j] { //print only duplicated element in arr
				fmt.Println(element1)
			}
		}
	}
```

## ✅ Map

- `key` + `value`
- no order

- ☑️ **create empty map**

```GO
mp := make(map[string]int) //create empty map
```

- ☑️ **create map with elements**

```GO
var mp map[string]int = map[string]int{ //create map with instances
		"apple":  5,
		"orange": 6,
		"peach":  7,
	}

//get value of key
fmt.Println(mp["apple"])

//change value of key
mp["apple"] = 900

//add key and value to map
mp["banana"] = 10

//delete apple key
delete(mp, "apple")

//check if a key exists
val, ok := mp["banana"]
fmt.Println(val, ok)
//if it does not exist, 0, false
//if it exists, get value, true
```

## ✅ Functions

- ☑️ **Create function and end with** `defer`

- return value can be more than one
- `defer`: run right before returning
- used for closing file system, finish I/O

```GO
func math(x, y int) (r1, r2 int) {
	defer fmt.Println("run last") //2️⃣ run before return and finishing function
	r1 = x + y
	r2 = x - y
	fmt.Println("run before") //1️⃣
	return //3️⃣
}

func main() {
	add, minus := math(3, 5)
	fmt.Println(add)
	fmt.Println(minus)
}

// run order of function math
run before
run last
8
-2
```

- ☑️ **Admit the function to a variable**

```GO
f := addFunc(4, 5) // Get the function
f()               // Now call it
```

- ☑️ **Function inside function**
- function can be admitted to a variable `variable := func()`
- then variable becomes function name, run function `variable()`

- 1️⃣ create function wo name and reference to variable `test`

```GO
func main() {
	//1️⃣ create function wo name and reference to variable test
	test := func(x, y int) int {
		return x + y
	}
	fmt.Println(test(4, 5))
}
```

- 2️⃣ create function and call it instantly
- hand over parameters right away to referenced variable
- same result as running `test()`

```GO
func main() {
	test := func(x, y int) int { //create function, reference variable
		return x + y
	}(4, 5) //2️⃣ hand over parameters right away
	fmt.Println(test)
	//same as test(4, 5)

	//create and run function w param right away
	func(x, y int){
		fmt.Println(x+y)
	}(4, 5)

}
```

- ☑️ **Hand over function as param**

```GO
func outTest(inTest func(int, int) int) {
	ans := inTest(3, 4)
	fmt.Println(ans)
}

func main() {
	test1 := func(x, y int) int {
		return x + y
	}
	test2 := func(x, y int) int {
		return x - y
	}

	outTest(test1) //7
	outTest(test2) //-1
}
```

- ☑️ **Function closure, function inside function**
- Function closure: when inside function uses variable of outside function
- capture variables from its **surrounding** scope
- keep variables like `x` and `sum` alive even after outer function returns
- sum will keep increasing, `sum++`

```GO
func returnFunc(x string) func() { //return a function
	sum := 1
	return func() {
		sum++ //function closure will remember variables
		fmt.Println("hello "+x, sum)
	} //function closure, use x, sum
}

func main() {
	returnFunc("Tim")
	//return a function, but does not call it
	//does not print anything
	returnFunc("Tim")()
	//call the function that returnFunc returned
	//return a function, then call -> print hello Tim 2

	y := returnFunc("John") //return function
	y()
	//call function
	//function closure remember variable x, sum
	// -> print hello John 2
	y() //hello John 3
	y() //hello John 4
}

```

## ✅ Mutable, Immutable

- ☑️ **Mutable**
- `Slice`, `Map`
- if `y` reference `x`
- and if `y` changes, `x` will **ALSO** change
- `y` is pointing to same `Slice`, `Map`
- modify the existing `Slice`, `Map`

```GO
var x []int = []int{1, 2, 3}
y := x
y[0] = 100
fmt.Println(x, y)
//x: [100 2 3]
//y: [100 2 3]


var x map[string]int = map[string]int{"a": 10}
y := x
y["b"] = 100
fmt.Println(x, y)
//x: map[a:10 b:100]
//y: map[a:10 b:100]
```

- in memory, instead of storing value, store the **address** of the value
- `slice` is saved on memory address 123
- `x` reference memory address 123
- `y` also reference memory address 123
- if `y` changes the slice, the slice that `x` reference also change

```
|             RAM            |
|----------------------------|
| 123 |   []int{1, 2, 3}     |
|  x  |        123           |
|  y  |        123           |
```

- ☑️ **Immutable**
- `Array`, `int`
- if `y` reference `x`
- and if `y` changes, `x` will **NOT** change
- `y` has created new array, different from `x`
- `x` and `y` point to different array
- DO NOT modify the existing `Array`, `int`

```GO
var x [3]int = [3]int{1, 2, 3}
y := x
y[0] = 100
fmt.Println(x, y)
//x: [1 2 3]
//y: [100 2 3]
```

- in memory, store the value itself
- `x` reference `array`
- `y` also reference its own `array`
- even if `y` changes, `x` is NOT affected

```
|             RAM            |
|----------------------------|
| x |   [3]int{1, 2, 3}      |
| y |   [3]int{100, 2, 3}    |
```

## ✅ Structs and Custom Types

- ☑️ **Create your own custom type**
- create class `Point` with two `int field` and `boolean field`

```GO
type Point struct {
	//field
	x        int32
	y        int32
	isOnGrid bool
}
```

```GO
var p1 Point = Point{1, 2, true} //1️⃣ create type Point
p1.x = 7 //can access field

p2 := Point{4, 10, false} //2️⃣ create type Point

p3 := Point{x: 3, y: 5} //3️⃣ create type Point, unmentioned field will be default value
```

- ☑️ **Stuct and pointer**

```GO
func changeX(pt *Point) { //param: addr of pointer
	pt.x = 100 //change value of pointing variable
}

func main() {
	p4 := &Point{y: 3} //create point, get addr
	p4.x = 9 //can change field
	fmt.Println(p4) //print address, &{0 3 false}
	changeX(p4)
	fmt.Println(p4) // &{100 3 false}
}
```

- ☑️ **Stuct inside Struct**
- 💡 notice `Point struct` inside `Circle` is a **pointer**

```GO

type Point struct {
	x int32
	y int32
}

type Circle struct {
	radius float64
	center *Point //💡 pointer to Point, address of Point
	//*Point //pointer name can be ommited
}
```

```GO
func main() {
	p1 := &Point{1, 3}
	c1 := Circle{10.123, p1} //1️⃣ create struct Circle

	c2 := Circle{14.56, &Point{3, 6}} //2️⃣ create struct Circle
	fmt.Println(c2) //{14.56 0x1400000e0d8}
	fmt.Println(c2.center) //&{3 6}, address
	fmt.Println(*c2.center) //{3 6}, get value of center
	fmt.Println(c2.center.x) //3
}
```

## ✅ Struct Methods

- Struct Method: functions to perform on an object
- Struct methods need to mention on which object to use this method
- `(s Student)`

- ☑️ **Getter**

```GO
type Student struct {
	name   string
	grades []int
	age    int
}


// s Student is reference to which this method will be used
func (s Student) getAge() int {
	return s.age
}

func main(){
	student1 := Student{"John", []int{70, 90, 80, 85, 100}, 17}
	student1.getAge()
}
```

- ☑️ **Setter**
- 💡 to change a value, need to reference the **pointer** of the object
- `(s *Student)`

```GO
func (s *Student) setAge(newAge int) { //need to pass pointer of Student
	s.age = newAge
}

// func (s Student) setAge(newAge int) { //this will not change student age
// 	s.age = newAge
// }
```

- ☑️ **get grade AVG, get max grade**

```GO

func (s Student) getAvgGrade() float32 {
	sum := 0
	for _, element := range s.grades {
		sum += element
	}
	return float32(sum) / float32(len(s.grades))
}

func (s Student) getMaxGrade() int {
	max := 0
	for _, element := range s.grades {
		if element > max {
			max = element
		}
	}
	return max
}
```

## ✅

```GO

```
