<h1 style"align: center"> 0x19. C - Stacks, Queues - LIFO, FIFO </h1>


<img src="https://pbs.twimg.com/media/CFYYWy6UEAE9Ow-.png" style="align: center">
## Requirements
## General

    - Allowed editors: vi, vim, emacs
    - All your files will be compiled on Ubuntu 20.04 LTS using gcc, using the options -Wall -Werror -Wextra -pedantic -std=c89
    - All your files should end with a new line
    - A README.md file, at the root of the folder of the project is mandatory
    - Your code should use the Betty style. It will be checked using betty-style.pl and betty-doc.pl
    - You allowed to use a maximum of one global variablGitHub



Please use the following data structures for this project. Don’t forget to include them in your header file.

/**
 * struct stack_s - doubly linked list representation of a stack (or queue)
 * @n: integer
 * @prev: points to the previous element of the stack (or queue)
 * @next: points to the next element of the stack (or queue)
 *
 * Description: doubly linked list node structure
 * for stack, queues, LIFO, FIFO
 */
typedef struct stack_s
{
        int n;
        struct stack_s *prev;
        struct stack_s *next;
} stack_t;

/**
 * struct instruction_s - opcode and its function
 * @opcode: the opcode
 * @f: function to handle the opcode
 *
 * Description: opcode and its function
 * for stack, queues, LIFO, FIFO
 */
typedef struct instruction_s
{
        char *opcode;
        void (*f)(stack_t **stack, unsigned int line_number);
} instruction_t;

Compilation & Output

    Your code will be compiled this way:

$ gcc -Wall -Werror -Wextra -pedantic -std=c89 *.c -o monty

    Any output must be printed on stdout
    Any error message must be printed on stderr
        Here is a link to a GitHub repository that could help you making sure your errors are printed on stderr

## Tests

We strongly encourage you to work all together on a set of tests
The Monty language

Monty 0.98 is a scripting language that is first compiled into Monty byte codes (Just like Python). It relies on a unique stack, with specific instructions to manipulate it. The goal of this project is to create an interpreter for Monty ByteCodes files.

Monty byte code files

Files containing Monty byte codes usually have the .m extension. Most of the industry uses this standard but it is not required by the specification of the language. There is not more than one instruction per line. There can be any number of spaces before or after the opcode and its argument:

julien@ubuntu:~/monty$ cat -e bytecodes/000.m
push 0$
push 1$
push 2$
  push 3$
                   pall    $
push 4$
    push 5    $
      push    6        $
pall$
julien@ubuntu:~/monty$

Monty byte code files can contain blank lines (empty or made of spaces only, and any additional text after the opcode or its required argument is not taken into account:

julien@ubuntu:~/monty$ cat -e bytecodes/001.m
push 0 Push 0 onto the stack$
push 1 Push 1 onto the stack$
$
push 2$
  push 3$
                   pall    $
$
$
                           $
push 4$
$
    push 5    $
      push    6        $
$
pall This is the end of our program. Monty is awesome!$
julien@ubuntu:~/monty$

The monty program

    Usage: monty file
        where file is the path to the file containing Monty byte code
    If the user does not give any file or more than one argument to your program, print the error message USAGE: monty file, followed by a new line, and exit with the status EXIT_FAILURE
    If, for any reason, it’s not possible to open the file, print the error message Error: Can't open file <file>, followed by a new line, and exit with the status EXIT_FAILURE
        where <file> is the name of the file
    If the file contains an invalid instruction, print the error message L<line_number>: unknown instruction <opcode>, followed by a new line, and exit with the status EXIT_FAILURE
        where is the line number where the instruction appears.
        Line numbers always start at 1
    The monty program runs the bytecodes line by line and stop if either:
        it executed properly every line of the file
        it finds an error in the file
        an error occured
    If you can’t malloc anymorTasks
0. push, pall
mandatory

Implement the push and pall opcodes.

The push opcode

The opcode push pushes an element to the stack.

    Usage: push <int>
        where <int> is an integer
    if <int> is not an integer or if there is no argument given to push, print the error message L<line_number>: usage: push integer, followed by a new line, and exit with the status EXIT_FAILURE
        where is the line number in the file
    You won’t have to deal with overflows. Use the atoi function

The pall opcode

The opcode pall prints all the values on the stack, starting from the top of the stack.

    Usage pall
    Format: see example
    If the stack is empty, don’t print anything

julien@ubuntu:~/monty$ cat -e bytecodes/00.m
push 1$
push 2$
push 3$
pall$
julien@ubuntu:~/monty$ ./monty bytecodes/00.m
3
2
1
julien@ubuntu:~/monty$

Repo:

    GitHub repository: monty

1. pint
mandatory

Implement the pint opcode.

The pint opcode

The opcode pint prints the value at the top of the stack, followed by a new line.

    Usage: pint
    If the stack is empty, print the error message L<line_number>: can't pint, stack empty, followed by a new line, and exit with the status EXIT_FAILURE

julien@ubuntu:~/monty$ cat bytecodes/06.m 
push 1
pint
push 2
pint
push 3
pint
julien@ubuntu:~/monty$ ./monty bytecodes/06.m 
1
2
3
julien@ubuntu:~/monty$ 

Repo:

    GitHub repository: monty

2. pop
mandatory

Implement the pop opcode.

The pop opcode

The opcode pop removes the top element of the stack.

    Usage: pop
    If the stack is empty, print the error message L<line_number>: can't pop an empty stack, followed by a new line, and exit with the status EXIT_FAILURE

julien@ubuntu:~/monty$ cat bytecodes/07.m 
push 1
push 2
push 3
pall
pop
pall
pop
pall
pop
pall
julien@ubuntu:~/monty$ ./monty bytecodes/07.m 
3
2
1
2
1
1
julien@ubuntu:~/monty$ 

Repo:

    GitHub repository: monty

3. swap
mandatory

Implement the swap opcode.

The swap opcode

The opcode swap swaps the top two elements of the stack.

    Usage: swap
    If the stack contains less than two elements, print the error message L<line_number>: can't swap, stack too short, followed by a new line, and exit with the status EXIT_FAILURE

julien@ubuntu:~/monty$ cat bytecodes/09.m 
push 1
push 2
push 3
pall
swap
pall
julien@ubuntu:~/monty$ ./monty bytecodes/09.m 
3

4. add
mandatory

Implement the add opcode.

The add opcode

The opcode add adds the top two elements of the stack.

    Usage: add
    If the stack contains less than two elements, print the error message L<line_number>: can't add, stack too short, followed by a new line, and exit with the status EXIT_FAILURE
    The result is stored in the second top element of the stack, and the top element is removed, so that at the end:
        The top element of the stack contains the result
        The stack is one element shorter

julien@ubuntu:~/monty$ cat bytecodes/12.m 
push 1
push 2
push 3
pall
add
pall

julien@ubuntu:~/monty$ ./monty bytecodes/12.m 
3
2
1
5
1
julien@ubuntu:~/monty$

Repo:

    GitHub repository: monty

5. nop
mandatory

Implement the nop opcode.

The nop opcode

The opcode nop doesn’t do anything.

    Usage: nop

Repo:

    GitHub repository: monty

6. sub
#advanced

Implement the sub opcode.

The sub opcode

The opcode sub subtracts the top element of the stack from the second top element of the stack.

    Usage: sub
    If the stack contains less than two elements, print the error message L<line_number>: can't sub, stack too short, followed by a new line, and exit with the status EXIT_FAILURE
    The result is stored in the second top element of the stack, and the top element is removed, so that at the end:
        The top element of the stack contains the result
        The stack is one element shorter

julien@ubuntu:~/monty$ cat bytecodes/19.m 
push 1
push 2
push 10
push 3
sub
pall
julien@ubuntu:~/monty$ ./monty bytecodes/19.m 
7
2
1
julien@ubuntu:~/monty$

Repo:

    GitHub repository: monty

7. div
#advanced

Implement the div opcode.

The div opcode

The opcode div divides the second top element of the stack by the top element of the stack.

    Usage: div
    If the stack contains less than two elements, print the error message L<line_number>: can't div, stack too short, followed by a new line, and exit with the status EXIT_FAILURE
    The result is stored in the second top element of the stack, and the top element is removed, so that at the end:
        The top element of the stack contains the result
        The stack is one element shor
17. Add two digits
#advanced

Add two digits given by the user.

    Read the two digits from stdin, add them, and print the result
    The total of the two digits with be one digit-long (<10)

julien@ubuntu:~/monty/bf$ bf ./1001-add.bf
81
9julien@ubuntu:~/monty/bf$

Repo:

    GitHub repository: monty
    Directory: bf
    File: 1001-add.bf

18. Multiplication
#advanced

Multiply two digits given by the user.

    Read the two digits from stdin, multiply them, and print the result
    The result of the multiplication will be one digit-long (<10)

julien@ubuntu:~/monty/bf$ bf 1002-mul.bf
24
8julien@ubuntu:~/monty/bf$

Repo:

    GitHub repository: monty
    Directory: bf
    File: 1002-mul.bf

19. Multiplication level up
#advanced

Multiply two digits given by the user.



    Read the two digits from stdin, multiply them, and print the result, followed by a new line

julien@ubuntu:~/monty/bf$ bf 1003-mul.bf 
77
49
julien@ubuntu:~/monty/bf$ 

Repo:

    GitHub repository: monty
    Directory: bf
    File: 1003-mul.bf

    GitHub repository: monty


## Author

Achieng Brian