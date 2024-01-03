# Brainfuck Interpreter in C

In this entry I want to create a simple Brainfuck Interpreter in C. 

## What is Brainfuck?

[brainfuck](https://esolangs.org/wiki/Brainfuck) is an Esoteric Language, so it is a language that is ment to hurt people writing or reading code in it. It is a Turing complete and only exists of 8 symbols:  `+-.,><[]` Every other character is automatically handled as a comment. Brainfucks Memory is Cell based, so it is an Array of cells, initialised to 0 and a Pointer pointing to the current Cell. 

```brainfuck
> Move the Pointer to the right
< Move the Pointer to the left
+ Increment the current Cell
- Decrement the current cell
. Output the character signified by the current cell
, Input a character and store it in the current cell
```

So a "simple" Hello World Programm in Brainfuck looks like this:

```brainfuck
++++++++[>++++++++<-]>++++++++.>++++++++[>++++++++++++<-]>+++++.+++++++..+++.>++++++++[>+++++<-]>++++.------------.<<<<+++++++++++++++.>>.+++.------.--------.>>+.
```

Try to understand it. It is black magic and definitely Brainfuck!

## Create the Interpreter

The interpreter will just take the Brainfuck code as input and execute it live. 

For that we need to create a new Folder and some Files. My Project looks as following:

```
Brainfuck-C
├── Makefile
└── main.c
```

Makefile:

```Makefile
CC = gcc  
CFLAGS = -Wall -Werror  
  
bf: main.c  
    $(CC) $(CFLAGS) -o bf main.c  
  
clean:  
    rm -f bf
```

main.c

```c
#include <stdio.h>  
  
int main(int argc, char *argv[]) {  
    if (argc != 2) return printf("USAGE: bf [code]\n");   
}
```

With this basic setup we include the stdio.h to print to the console. And we create the main function. It takes two parameters, `argc` is the count of arguments when starting the binary, `argv` is an array of char pointers that includes all the arguments (also the name of the executable as the first one).