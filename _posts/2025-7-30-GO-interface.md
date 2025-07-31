---
title: Interface/Error Handling
categories: [Golang, Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ Interface

- Interface:
- 1️⃣ Go’s equivalent of Java’s `Object class`
- most general type
- any value can be stored in a variable of type `interface{}`

- 2️⃣ **set of methods** to be implemented on several objects
- inside interface `shape`, mention function name `area()`
- if an object `circle` has that function `area()`
- ➡️ `circle` implements the `shape` interface

- can implement more than one interface
- object should have **ALL** the functions in interface

## 1️⃣ interface as **most general type**

```GO
//create interface
box := interface{}("hello") //can assign any type to interface

func describeValue(t interface{}) {
	fmt.Printf("%T, %v\n", t, t)
}

describeValue(box) //string, hello
```

## 2️⃣ interface as **set of methods**

- ☑️ **example 1:** `Circle` and `Rect structs` implement `Shape interface`

```
    Shape Interface
        [area()]
          /  \
     Circle   Rect
```

```GO
// create interface
type Shape interface {
	//any object that has area() is implementing type Shape
	area() float64 //return float64
}

type Circle struct {
	radius float64
}

type Rect struct {
	width  float64
	height float64
}

//circle has area() -> implements shape interface
func (c Circle) area() float64 {
	return c.radius * c.radius * 3.14
}
//rect has area() -> implements shape interface
func (r Rect) area() float64 {
	return r.height * r.width
}

//can make function with shape interface
func getArea(s Shape) float64 {
	return s.area()
}
```

```GO
func main() {
	c1 := Circle{4.5}
	r1 := Rect{5, 20}

	 //implement interface, can put both circle and rect in Shape
	shapes := []Shape{c1, r1}

	for _, shape := range shapes {
		fmt.Println(shape.area()) //use interface function
		fmt.Println(getArea(shape)) //use function that reference interface
	}
}
```

- ☑️ **example 2:** `Shape` and `Mesurable interface` implement `Geometry interface`
- `struct Rect` implements `Shape` and `Mesurable interface`

```
          Geometry Interface
          /               \
Shape Interface         Mesurable Interface
    [area()]                [permimeter()]
            \                  /
                    Rect
```

```GO
type Geometry interface {
	Shape
	Measurable
}

type Shape interface {
	area() float64
}

type Measurable interface {
	perimeter() float64
}

type Rect struct {
	width, height float64
}

func (r Rect) area() float64 {
	return r.width * r.height
}

func (r Rect) perimeter() float64 {
	return (r.width + r.height) * 2
}

func describeShape(g Geometry) { //geometry as param
	fmt.Println("Area: ", g.area())
	fmt.Println("Perimeter: ", g.perimeter())
}

func main() {
	rect := Rect{4, 5}
	describeShape(rect)
}
```

## ✅ Error handling with Error Interface

- ☑️ **Go built-in `Error Interface` looks like this**
- to implement `Error Interface`, need to create `Error()` function

```GO
type error interface {
	Error() string
}
```

- ☑️ error message interface

```GO
type CalculationError struct {
	message string
}

func (ce CalculationError) Error() string { //implement error interface
	return ce.message
}

func calculate(val float64) (float64, error) { //calculate method, can return error message
	if val < 0 {
		return 0, CalculationError{"Invalid input"}
	}
	return math.Sqrt(val), nil
}

func main(){
    result, err := calculate(-9)
	if err != nil {
		fmt.Println(err)
	} else {
		fmt.Println(result)
	}
}
```

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
