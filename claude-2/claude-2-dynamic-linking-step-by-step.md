# Provide detailed step-by-step explanation of how dynamic linking works in context of system programming

Here is a detailed step-by-step explanation of how dynamic linking works in the context of system programming:

1. Compilation
When source code is compiled into an executable file, any functions or libraries that are called but defined elsewhere are left as unresolved references. The compiler generates object code with placeholders for all unresolved references.

2. Linking 
When the executable is linked, a dynamic linker is included in the final executable file. The dynamic linker's job will be to resolve the unresolved references at runtime.

3. Runtime 
When the executable file is loaded into memory and executed, the dynamic linker goes through the following steps:

(a) It loads any shared libraries (.so files in Linux or .dll files in Windows) that are required to resolve unresolved references into memory.

(b) It checks if the symbols (functions or variables) referenced by the placeholders are available in any recently loaded shared libraries. 

(c) If a match is found, it updates the code to replace the placeholders with the actual memory addresses of the symbols. This process is called symbol resolution.

(d) If any symbols are still missing, the dynamic linker repeats steps (a) to (c) to load more shared libraries and resolve symbols until no placeholders remain unresolved.

4. Execution
Once all placeholders have been resolved to actual memory addresses, the dynamic linker jumps to the start of the program code and begins execution. 

When function calls or variable accesses are made, control is transferred directly from the program's code to the code in the shared library - no further involvement of the dynamic linker is needed at this point during execution.

This allows executables to share common libraries, reducing memory usage and executable file size. It also allows libraries to be updated without needing to re-link executables.
