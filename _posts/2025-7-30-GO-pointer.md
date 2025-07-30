---
title: Pointer
categories: [Golang, Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ Pointer and Reference

- `*`: dereference operator(get/set value at address)
- `&`: get pointer(get address) operator
- `*T`: pointer to a value of type `T`, like `str *string`

- `&before variable`: get the reference, address of the variable
- `*before variable name`: dereference the pointer, go to the pointer and **get or set** the value of that address

- `pointer`: variable that stores the memory address of another variable
- `y` is pointer of int

```GO
x := 7
fmt.Println(x)  //print value 7
fmt.Println(&x) //&, get reference, print address 0x14000112020

y := &x //y is pointer
fmt.Println(y) //0x14000112020

*y = 8 //*, dereference the pointer, change value of x
fmt.Println(x) //now x is 8
```

- `*before data type`: pointer(get memory address)of that data type

- ☑️ **Changes the value of myWord**
- if you want to change the value of an immutable, need to pass the pointer

```GO
//parameter (str *string)
//*, pass the pointer for this parameter, not the value
//passing the memory address of variable as parameter
//pass memory address of myWord
func changePointer(str *string) {
	*str = "changed1" //*str = change the value of that pointer
}
```

- ☑️ does **NOT** change value of myWord

```GO
// does not change value of myWord
func changeValue(str string) { //pass value of myWord
str = "changed2"
}
```

```GO
func main(){
	myWord := "hello"
	changePointer(myWord) // <- pass address(0x14000112020)of myWord as param
	changeValue(myWord) // <- pass value "hello" as param
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

## ✅
