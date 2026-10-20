# Alpha Language Compiler

Course project for the Compilers course (HY-340), Computer Science Department, University of Crete.

A complete compiler and virtual machine for *alpha*, a small dynamically typed scripting language with functions, tables (objects), functors, and a set of library functions. The pipeline goes from source text to tokens, to a parse tree with a scoped symbol table, to intermediate code (quads), to target code executed on a purpose-built virtual machine.

## Pipeline

The project is built in phases, each in its own folder:

1. **Phase1** — Lexical analyzer (Flex): tokens, strings with escapes, nested block comments.
2. **Phase2** — Syntax analysis (Bison) with a hash-table symbol table and scoping rules: redeclarations, shadowing of library functions, access to inactive scopes.
3. **Phase3** — Intermediate code generation: quads for arithmetic, relational and boolean expressions with short-circuit evaluation, loops with break/continue backpatching, functions, and table operations.
4. **Phase4_5** — Target code generation and the alpha virtual machine: quads are translated to VM instructions with jump backpatching and constant tables, written to a binary (`tbinary.abc`), then loaded and executed by the VM (stack-based activation records, hashed tables, library functions such as `print`, `typeof`, `input`, `objectcopy`, `argument`, `strtonum`, `sqrt`, `cos`, `sin`).

## Tech stack

C (gcc), Flex, Bison, Make.

## Build and run

Prerequisites: `gcc`, `flex`, `bison`, `make`.

```
cd Phase4_5
make syntax                          # build the compiler
./syntax program.alpha output.txt    # compile an alpha program (writes tbinary.abc)
make load
./load                               # run the compiled binary on the VM
```

Earlier phases build the same way (`make`) inside their own folder.

## Example

`examples/factorial_and_tables.alpha`:

```
function fact(n) {
    if (n < 2) return 1;
    return n * fact(n - 1);
}
print("5! = ", fact(5), "\n");
t = [ { "lang" : "alpha" }, { "answer" : 42 } ];
print(t.lang, " ", t.answer, "\n");
```

```
$ ./syntax examples/factorial_and_tables.alpha quads.txt && ./load
5! = 120
alpha 42
```

## Authors

Apostolos Mavrogiannakis, Haralambos Varsamis, Georgia Rapousi
