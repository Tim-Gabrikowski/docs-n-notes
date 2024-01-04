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
[ Jump to the matching ] if the current value is 0
] Jump to the matching [ if the current value is nonzero
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
	return 0:
}
```

With this basic setup we include the stdio.h to print to the console. And we create the main function. It takes two parameters, `argc` is the count of arguments when starting the binary, `argv` is an array of char pointers that includes all the arguments (also the name of the executable as the first one). We then check if we have 2 arguments (the binary and the code). If not we print the usage and end the execution.

Due to brainfucks Memory being a long array, we can easily create a cells array. The size of the array i will define it as can array. The "cursor" will be a pointer. 

```c
#define CELL_COUNT
char cells[CELL_COUNT] = {0};
char *cursor = &cells;
```

To Read the code from the param. we create a char pointer called `code` and assign it the value of the `argv` array at index `1`. In this example we will then print out the code.

```c
char *code = argv[1];
printf("Brainfuck: %s", code);
```

After that we start the actuall execution. Due to every instruction only being one character long we can iterate over the code pointer with a `while` loop:

```c
while(*code != '\0') {
	/* execute code.... */
	code++;
}
```

As a condition we check if the current character is not a Null character because strings in c are null terminated. Then we do our executing of the code and then increase the pointer to the next character, aka our next instruction.

To now execute our Brainfuck code, we can use a Switch-Case statement:

```c
switch (*code) {
	case '+':
		break;
	case '-':
		break;
	...
}
```

Each case is the character that we could have. The variable is the value at the code pointer `*code`.
The `+` and `-` statements are easy. We just need to increment or decrement the value at the `cursor` Pointer. When decrementing, we need to make sure it is not 0 or lower becuase there are no negative characters.

```c
case '+':
	(*cursor)++;
	break;
case '-':
	if(*cursor <= 0) break;
	(*cursor)--;
	break;
```

The `<` and `>` expression shoult also be pretty simple. We just need to increment or decrement the cursor pointer. When decrementing the pointer we need to make sure, that it is not lover than the adress of the first cell. When incrementing we need to make sure we don't overshoot the end of the array.

```c
case '>':  
    if(cursor == &cells[MAX_CELLS -1]) break;  
    cursor++;  
    break;  
case '<':  
    if(cursor == &cells[0]) break;  
    cursor--;  
    break;
```

The `.` and `,` are also quite easy. For the printing we just use `printf` with the current character at the cell. For taking the input we use the `getchar` method of the stdlib.

```c
case '.':  
    printf("%c", *cursor);  
    break;  
case ',':  
    *cursor = getchar();  
    break;
```

At this point we should have a simple Brainfuck interpreter. We can compile it using make and then run it with a sample script:

```sh
make
./bf ",+."
```

With this commands we build it and then execute the Brainfuck code `,+.`, which takes in a character, adds 1 to it and prints it. So if we input `a` we get `b` as output.

For the `[` and `]` statements we need to know where the next matching is. For that i would keep track of the current open brackets in an integer variable and define two functions `jumpToClosing` and `jumpToOpening`. As parameters they will take a Pointer to the code pointer. so that i can modify the code pointer from inside the function.

```c
int brackets = 0;  
  
void jumpToClosing(char** c) {}  
void jumpToOpening(char** c) {}
```

For the `jumpToClosing` function we need keep track of our bracket count at the start and then loop through the code and find the next closing bracket with the same index. Every time we se an openning Bracket, we increase the counter and when we see a closing Bracket, we decrement it.

```c
void jumpToClosing(char** c) {  
    int bStart = brackets + 1;  
  
    while(**c != ']' && brackets == bStart) {  
        *c++;  
        switch(**c) {  
            case '[':  
                brackets++;  
                break;  
            case ']':  
                brackets--;  
                break;  
        }  
    }  
}
```

For the `jumpToOpening` we need to do a similar thing. We need to go a step back and check if it is our opening Bracket.  We also need to keep track of our current Bracket count by counting up the counter when we se an other closing Bracket and count down when we se an opening Bracket, because we move backwards.

```c
void jumpToOpening(char** c) {  
    int bStart = brackets - 1;  
  
    while(**c != ']' && brackets == bStart) {  
        *c--;  
        switch(**c) {  
            case '[':  
                brackets--;  
                break;  
            case ']':  
                brackets++;  
                break;  
        }  
    }  
}
```

When calling the function we need to give the adress of the code pointer as parameter. But we first need to increment the Bracket Counter, because the `jumpTo` Functions ignore the bracket they are currently on so it makes no difference for them if you are outsite of an bracket or in the first layer.

```c
case '[':  
    if (*cursor == 0) jumpToClosing(&code);  
    break;  
case ']':  
    if(*cursor != 0) jumpToOpening(&code);  
    break;
```

