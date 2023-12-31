# Alpha Language Compiler - Phase 3

Members:

- Apostolos Mavrogiannakis csd3799
- Varsamis Haralampos csd3744
- Georgia Rapousi csd3836

- **Changes for phase 3 at the end of the file**

## Phase 2

### Introduction

Hello,

This is a readme file with 3 sections.

1. How to run the program,
2. Some info about the way we handle some errors
3. Rules recognized

## How to run the program

You need to use 3 arguments.It works only if you give 3 arguments.

1. 1st argument is the program to run . e.g. ./syntax

2. 2nd argument has 2 possible valid values:
   - '-' input comes from stdin.
   - File(e.g. test1.txt) input comes from a file
3. 3rd argument has 2 possible valid values:
   - '-' output is stdout.
   - File(e.g. results.txt) output gets written to the results.txt

Correct syntax example :

- ./syntax - output_file
- ./syntax input_file -
- ./syntax - -
- ./syntax in_file out_file

In case you are wondering why we made it like that,it is because if you run it as:

./syntax file

The file is the input or the output? So to avoid confusion we insert the data as described above.

Also,in case you choose to run the program from command line after giving your input you must type "EXIT;" so that you can exit the parser and finish the processing successfully.

## Info about the way we handle some errors

The informative printing of syntax errors that derive from grammar input mistakes have been handled in a simple manner.

E.g. unction(a,b){} | {local x; | function x(a b){}  .

We mostly return the line where the error occured and that it might be a missing bracket or a missing semicolon or a bad formation of the code.

Other than syntax errors from grammar input mistakes,everyting else is handled with precision.Which means that errors like redeclaration,shadowning, accessibility checking is handled carefully.

All the errors that are found are printed at the stderr.In case of an error, the table of scopes is not printed.We chose to do it like that because errors ussually change the flow of the program and we decided that it should be printed only if the program processed everything correctly. But in case you want to see the table of scopes even if errors are found in the input,you can go in line 786 in the .y file and comment the if(!error_flag).

## Rules recognized

The rules that are recognized are always written to the file rules.txt.We don't give the option to print them to stdout because if the program recognized 1000 rules,the final printage will cause a mess in the command line.

For each run you must delete rules.txt because it is in append mode.

## Phase 3

Coming across with an error, our implementation doesn't allow the error statement to be inserted in the symbol table,
so, for instance lets say we want to compile the code below

x=8;

function x() {
 return 1;
}

This will print error, function name x already exists in this scope, which means that there will be no insertion for function x in the symbol table,
so an additional error will pop-up saying that return statement isn't referring to a function.

Thank you.
