---
title: Tipo De Datos, Literal, Operador, Conversiones
categories: [DAW bilingual, Programacion]
tags: [] # TAG names should always be lowercase
---

## ✅ Tipo De Datos

- byte: 8bit
- short: 16bit
- int: 32bit
- long: 64bit
- float: 32bit
- double: 64bit
- Char: 16bit

## ✅ Literal

> fixed value written directly in code

```java
int x = 10; //integer literal
String name = "Alice"; //String literal
boolean flag - true; //boolean literal
```

## ✅ La Constant

> datos que nuca varían, no va poder ser modificado nunca

- se declaran en mayúscula

```java
final (static) double PI = 3.141592;
```

```java
int a = 10;  //10 -> literal, a -> variable
a = 20; //variable changed

final int b = 30; //30 -> literal b -> constant
b = 40; //❌ Error, cannot assign value to constant final
```

- `a`: variable
- `10, 20, 30, 40`: literal
- `final`: constant

## ✅ XOR

- `^`
- `a^b`

#### 1️⃣ XOR in integers

```java
int A = 5;    // binary: 0101
int B = 3;    // binary: 0011
int result = A ^ B;

   0101   (5)
^  0011   (3)
---------
   0110   (6)
   // result = 6
```

#### 2️⃣ XOR in boolean

- only when one is true, result is true

```java
boolean A = true;
boolean B = false;
System.out.println(A ^ B); // true
System.out.println(A ^ true); // false
```

## ✅ Shift operators

#### `<<`

- left shift, empty right is filled with 0s

```java
int a = 5;       // binary: 0000 0101
int result = a << 1;

0000 0101   (5)
<< 1
---------
0000 1010   (10)
```

- `a^n` = `a * 2^n`
- equivale a num = num \* 2

#### `>>`

- signed right shift
- leftmost bit is copied, preserve the number

```java
int a = 20;      // binary: 0001 0100
int result = a >> 2;

0001 0100  (20)
>> 2
0000 0101  (5)
```

- Divides by 2 for each shift right
- equivale a num = num / 2

#### `>>>`

- shift right
- but fill left with `0s`

## ✅ Operador

```java
int i=1;
int z;

z = 5 + i++; //z=6
z = 5 + i;
i++;

z= 5 + ++i; //7
i++;
z = 5 + i;
```

## ✅ Conversiones, Casting

1. Conversiones implicitas

- la variable destino tenga más precisión que la variable origen

```java
int x = 5;
double y;

y = x;
//possible, double > int
```

```java
int x ;
double y = 5.3;

x = y;
//not possible, double > int
```

2. Conversiones explicitas = casting

```java
int x ;
double y = 5.3;

x = (int) y;
//now possible
// x = 5 , trunca
```

## ✅

## ✅

## ✅

## ✅

## ✅
