# Fast Introduction to C

C is a Structured Programming language that was invented in 1970 by Dennis Ritchie. It is a powerful and widely used language. C has stood the test of time and remains a popular choice for building system-level software, embedded systems, and applications where performance and control are critical.

## Table of Content

- [Tools](#tools)
- [Basic File Structure](#Basic%20File%20Structure)
- [Keywords and DataTypes](#Keywords%20and%20Datatypes)
- [Variables](#variables)
- [Operators](#operators)
- [if-else](#if%20-%20else)
- [Switch](#switch)
- [Loops](#loops)
- [Functions](#functions)
- [Arrays](#arrays)
- [Pointers](#pointers)
- [Strings](#strings)
- [Structure](#structure)
- [Comments](#comments)
- [Executing](#executing)

## Tools

To compile a C Programm you need a compiler, either [GCC](https://gcc.gnu.org/) or [Clang](https://clang.llvm.org/). To install them, follow the instructions on their websites.

## Basic File Structure

A C Programm is written in a file ending in `.c`. In the main File we need to place the `main` function.

``` c
int main () 
{

}
```

You can Include other C files to your Project by writing an  `#include` statement. After that you enter the filename of the Header-File. A Header-File has the extension `.h`. You write this filename in angle brackets, if it is from the standart C Library or in double quotes if it is in your project.

```c
#include <filename.h>
#include "localFile.h"
```

## Keywords and Datatypes

There are 32 reserved Keywords and 5 Datatypes.

| **Keywords**      |          |          |
| :------- | :----- | :------- | :------- |
| auto     | double | int      | struct   |
| break    | else   | long     | switch   |
| case     | enum   | register | typedef  |
| char     | extern | return   | union    |
| const    | float  | short    | unsigned |
| continue | for    | signed   | void     |
| default  | goto   | sizeof   | volatile |
| do       | if     | static   | while    |

| **DataTypes** |                                                |
| :----- | :---------------------------------------------------- |
| char   | Used to refer to characters or strings.               |
| int    | Whole numbers                                         |
| float  | Decimal values with 6 Digits after Comma              |
| double | Decimal values with 15 Digits after Comma             |
| void   | Empty DataType used in functions without return value |

## Variables

To Declare a variable, specify its DataType and its name. There are certain Rules for naming Variables. A variable name can only begin with a letter or underscore, it can only contain letters, digits and underscores. It should not be a keyword. It should not contain whitespaces and is case sensitive.

```c
int main () 
{
	int a = 0;
	char b = 'b';
	float c = 1.5f;
}
```

## Operators

### Arithmetic Operators

| Operator | Meaning   | Example     |
| :-: | :------------- | :---------- |
|  +  | Addition       | 3 + 4 = 7   |
|  -  | Subtraction    | 9 - 4 = 5   |
|  *  | Multiplication | 5 * 3 = 15  |
|  /  | Division       | 51 / 17 = 3 |
|  %  | Remainder      | 15 % 4 = 3  |

### Relational Operators

| Operator | Meaning           |
| :-: | :--------------------- |
|  >  | Greater than           |
| >=  | Greater than or equals |
|  <  | Less than              |
| <=  | Less than or equals    |
| ==  | Equals                 |
| !=  | Not equals             |

###  Logical Operators

| Operator | Meaning |
| :--: | :-- |
|  &&  | And |
| \|\| | Or  |
|   !  | Not |

## If - Else 

### if
```
if (condition) {...}
```

```c
if(a == b) 
{
	c = 5;
}
```

### else

```
if(condition) {...}
else {...}
```

```c
if(a == b) 
{
	c = 5;
} else 
{
	c = 10;
}
```

### else if

```
if(condition) {...}
else if (other condition) {...}
else {...}
```

```c
if(a == b) 
{
	c = 5;
} else if (a < b)
{
	c = 10;
} else 
{
	c = 15;
}
```

### Short form

If your code blocks in the Ifs are only one statement, you can write it in a single line without the Brackets. Also else and else if statements will work.

```c
if(a == b) c = 5;
else if (a < b) c = 15;
else c = 10;
```

## Switch

A switch statement is used to select one statement out of many by a given value.

```c
int a = 2;

switch (a) 
{
	case 0:
		doA();
		break;
	case 1:
		doB();
		break;
	case 2:
		doC();
		break;
	default:
		doAnything();	
}
```

## Loops

### While

A while loop gets executed, while a condition is true. The condition is checked **before** the run of the code. So if it is false on the first run, the code will not be executed.

```
while (condition) {
	...
}
```

### do-while

Like a while loop, the do while loop executes if a condition is true. But the condition is checked **After** it runs, so it allways runs once.

```
do {
	...
} while (condition)
```

### for

A for loop gives us the ability to execute code n amount of times and gives us the current run number. We give it a statement to run before the looping, the condition to run, which gets  checked before it runs and a statement after each execution.

```
for(before; condition; after each)
{
	...
}
```

```c
for(int i = 0; i < 5; i++)
{
	something(i);
}
```

## Functions

Functions are small blocks of code, that can be executed from other parts of the code. To Define a function we must first deklare its return DataType followed by its name. In round Brackets we then declare the parameters the function uses. To return a value, use the `return` Keyword. 

```
void name(parameters) 
{
	...
}
```

```c
int sum (int a, int b) 
{
	return a + b;
}
```

## Arrays

Arrays are collections of Values from the same DataType. You declare an Array the same way you declare an other variable but after the name you give the size of the array in square Brackets.

```c
int arr[5];
```

Creates an Array with 5 Integers. You can have empty Square Brackets, if you directly assign values to the array when declaring. The size of the array is then the count of elements you give it.

```c
int arr[] = {1, 2, 3, 4, 5};
```

To access any element in the array, you write the name of the array and then in square Brackets the index of the element. Remember that we start counting at 0, so the first element has Index 0.

```c
int a = arr[2];
```

You can also declare 2, 3 or n dimentional arrays like so:

```c
int matrix [2][2]; // 2D
int cube [2][2][2]; // 3D
```

## Pointers

When we declare a Variable, the variable name is assigned to a memory location where the value is stored. To get the Adress of a variable and not its value we add the `&` sign before the name. A variable that stores another Variable's address is called a pointer. It points to the other variable.

To create a Pointer, you just write a `*` before the variable name on declaration. To then assign it an adress, you use the `&` sign before the wanted variable name like said above.

```c
int a = 15;
int *ap;
ap = &a;
```

`aP` stores the Adress of `a`. If you want to read the value of `a` through the pointer `aP`, you write an `*` before the pointer's name:

```c
int c = *aP;
```

`c` now has the value of `a`, `15`.

## Strings

Strings in C are Arrays of Characters. You define them like so:

```c
char myString[12] = "Hello World!";
```

The `string.h` file of the Standard library has a lot of functions to work with strings like compare or copy.

## Structure

A Structure is a Collection of different data items. To define a structure we use the `struct` Keyword followed by the name of our structure. In curly Brackets we then write the members of the struct (int, char...) with their names, seperated by semicolon.

```c
struct car 
{
	char name[20];
	int year;
	char model [20];
}
```

to create a variable of our struct, we write the `struct` keyword followed by the name of out struct and the name of our variable. We then assign the values by writing them comma seperated in curly Brackets:

```c
struct car BMW = {"BMW APLA", 1990, "Parrot"};
```

To access a variable of a struct, type the structs name and then use the dot notation to access its member variables:

```c
int y = BMW.year;
```

## Comments

Single line comments can be created by using `//`. They start with the double slash and end at the end of the line.

Multiline comments begin with `/*` and end with `*/`. They can include multiple lines or just a few characters inside a line.

```c
int a = 10; // single line
/*
Multiline
Comment
*/
int b = 15;
/* also a multiline comment ;) */ int c = a + b;
```

## Executing

To compile and execute a C programm using `gcc`, type `gcc` and then the filename of the C-File. After that with the option `-o` declare the output filename.

```sh
gcc main.c -o bin.exe
./bin.exe
```