# Alpha Language Compiler

Members:

- Varsamis Haralampos csd3744
- Apostolos Mavrogiannakis csd3799
- Georgia Rapousi csd3836

## Introduction

The project is the complete creation of a compiler for the alpha language. It consists of 5 phases,

1. The implementation of a lexical analyzer using the generator of lexical analyzers Lex/Flex
2. The implementation of a syntax analyzer using YACC(or Bison) with C and the the lexical analyzer from Phase 1
3. The integration of the syntax analyzer from Phase 2 along with the semantic rules provided to generate the intermediate code.
4. The completion of the compiler with the production of the final code
5. The construction of the virtual machine that will load and execute machine code.
