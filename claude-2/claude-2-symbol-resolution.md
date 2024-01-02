# Provide detailed explanation of what symbol resolution is in context of linking of object files

Symbol resolution refers to the process of resolving symbolic references during the linking of object files into an executable program. Here is a more detailed explanation:

- Object files contain different types of symbols - function names, global variables, labels, etc. These symbols are not assigned actual memory addresses in the object files, rather they are symbolic references.

- When the linker combines multiple object files into a single executable, it needs to connect all the references to these symbolic names and assign final memory locations. This is known as symbol resolution.

- For example, one object file may contain a call to a function "foo()". Another object file contains the actual definition of "foo()". The linker will connect the call site to the actual function definition and update the reference to point to the correct memory location.

- Similarly, if one object file uses a global variable called "bar", but another object file contains the definition with storage allocation for "bar", the linker resolves the symbol and points the references to "bar" in the correct storage location.

- The linker maintains a symbol table containing all exported names from object files and libraries. As it encounters symbolic references, it searches this table to find the location where the symbol is defined. Based on that, it assigns the addresses.

- If a symbol cannot be resolved, the linker treats it as an external reference and allows the runtime dynamic linker to handle the resolution of the symbol. This enables linking against libraries which may contain symbols that won't resolve until runtime.

In summary, symbol resolution is a key part of linking where symbolic names used across multiple object files are assigned definite memory locations so that all the references can be connected accurately.

# How are symbol, reference and definition represented technically? Provide c code example

Symbols, references and definitions are represented in the following technical ways in C code:

Symbols:
- Symbols represent named functions or global variables that can be accessed across source files. 

- They are declared like:

```c
// math.h
int add(int a, int b); // Function declaration 
extern int x; // External variable declaration
```

- The declarations tell the compiler about the symbol name and attributes, but not the implementation details.

References:

- A reference is made when a symbol is used in the code without defining it. This serves as a call site that needs to be connected to an implementation.

```c  
// main.c
#include "math.h" 

int main() {
  int sum = add(2, 3); // Reference to add() 
  x = 10; // Reference to external variable x
}
```

Definitions:

- The definition contains the actual implementation (or allocation in case of variables) for a symbol.

```c
// math.c
int add(int a, int b) {
  return a + b; 
}

int x; // Definition with allocation
```

So in summary, declarations introduce symbols, references/calls are made to those symbols, and definitions contain the symbol implementation. The linker matches references to definitions during build.

# But what is the symbol if function is declared and referenced, but not defined, in particular piece of code?

Good question! If a function is declared and referenced but not defined in a particular piece of code, it is considered an undefined symbol. Here is what happens in this case:

```c
// header.h
int foo(int x); // function foo declared 

// source.c
#include "header.h"

int main() {
  int y = foo(10); // foo referenced but not defined  
}
```

In this code:

- `foo` is declared in the header, so the compiler knows about it.

- It is referenced and invoked inside `main()`. However, its definition is not provided.

- For the compiler, `foo` acts as an undefined symbol. It does not know the location or implementation of this symbol.

- But since it is declared, the compiler expects its definition to be provided by some other file during the linking stage.

- So when the object file is created from `source.c`, there will be a reference to the symbol `foo`, but no definition for it.

- It is the job of the linker to resolve this undefined symbol, either by finding its definition in another file within the program, or by linking to an external library.

- If the linker does not find the definition, it will throw an "undefined symbol" error.

In summary, such unresolved symbols are tracked as undefined references in object files emitted by the compiler. The linker attempts to find their definitions across all provided inputs.

# Provide detailed explanation of what is the difference between symbol and reference?

The main differences between a symbol and a reference are:

Symbol:
- A symbol is a name used to identify a function, variable, class etc. in code. It is just a textual name.
- For example, foo, myFunction, myVar are symbols.
- Symbols are declared at the top. Declarations just announce that the symbol exists, without defining what exactly it contains.

Reference:  
- A reference refers to the usage of a symbol within code. It tries to access the underlying entity (function/variable) represented by the symbol.
- When you call a function or access a variable, you are creating references to those symbols. 
- References don't have their own definition. They refer to symbols which are defined somewhere else.

In terms of code representation:

- Symbols appear as textual names in declarations at the top of files/classes.
- References appear where functions are called or variables accessed within bodies of code.

Key Differences:

- Symbol is a name, reference is the usage of that name.
- Symbols are textual labels, references try to resolve to actual definitions.  
- Symbols are declared, references are used at runtime.
- Compilers/linkers try to link references to symbols during builds.

In summary, a symbol is a purely symbolic name or label, while a reference is the active usage of that symbol in code during execution. Symbols can exist without references, but references depend on symbols resolving correctly.
