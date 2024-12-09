---
title: "ecosystem"
date: 2024-11-30 10:00:00 +0000
categories: [General]
tags: []
toc: true
---
## Key Terms

**Compiler**: A tool that translates your high-level source code into another form, typically either machine code (native executables) or an intermediate language. Example: `javac` for Java, `csc` for C#, `gcc` for C/C++.

**Interpreter**: A program that directly executes instructions written in a programming language without previously converting them into machine code. Example: the standard Python interpreter that runs `.py` files.

**Runtime**: The environment and libraries needed to actually run the compiled or interpreted code. This often includes memory management, type systems, and base libraries. Example: The Java Runtime Environment (JRE) includes the JVM that runs Java bytecode.

**SDK (Software Development Kit)**: A collection of tools, libraries, headers, and documentation that you need to develop (not just run) software in a certain language or framework. Typically includes the runtime, compiler, and additional tooling such as debuggers, linters, project scaffolding tools.

**JVM (Java Virtual Machine)**: A virtual machine that executes Java bytecode. It’s part of the Java runtime environment. Other languages like Kotlin and Scala also run on the JVM.

---

## By Language

### 1. Java
- **Source Code**: `.java` files
- **Compiler**: `javac` (converts `.java` to `.class` bytecode files)
- **Runtime**: **JVM + JRE**  
  - **JRE (Java Runtime Environment)** includes the JVM and standard libraries. It’s what you need to run `.class` and `.jar` files.
- **SDK**: **JDK (Java Development Kit)**  
  - JDK = JRE + Compiler (javac) + Development Tools (like `javadoc`, `jar`).

To **run** a Java app: JRE is needed.  
To **develop** a Java app: JDK is needed (which includes the JRE).

---

### 2. C#
- **Source Code**: `.cs` files
- **Compiler**: Roslyn C# compiler (invoked by `dotnet build` or `csc`)
- **Runtime**: **.NET Runtime** (CLR – Common Language Runtime)  
  - The CLR executes the Intermediate Language (IL) code produced by the compiler.
- **SDK**: **.NET SDK**  
  - Includes the C# compiler, runtime, and tools like `dotnet` CLI, plus libraries and templates.

To **run** a C# (and generally .NET) app: .NET Runtime is needed.  
To **develop** a C# app: .NET SDK is needed (includes compiler + runtime).

---

### 3. Python
- **Source Code**: `.py` files
- **Interpreter**: The Python interpreter (e.g., CPython)
- **Runtime**: The interpreter itself acts as the runtime environment. It includes the Python standard library.
- **SDK**: Typically just the interpreter installation (Python.org install) which includes the standard library and pip. There’s no separate “SDK” term commonly used; the interpreter + standard library = full environment.

To **run** Python code: Python interpreter is enough.  
To **develop** Python code: Same as running; just the interpreter plus any editor/IDE you like.

---

### 4. JavaScript (Node.js)
- **Source Code**: `.js` files
- **Compiler**: Not traditionally compiled; V8 engine JIT-compiles JS at runtime.
- **Runtime**: **Node.js runtime** (includes V8 JavaScript engine and Node standard libraries)
- **SDK**: Not typically called an SDK. Installing Node.js gives you the runtime, `npm`, and all that’s needed to develop and run JS apps outside the browser.

To **run** JS on server: Node.js runtime.  
To **develop** JS apps (server-side): Just Node.js runtime + npm/yarn.

For browser-based JavaScript, the **browser** provides the runtime (JavaScript engine + Web APIs). No separate installation is needed.

---

### 5. Go (Golang)
- **Source Code**: `.go` files
- **Compiler**: The Go compiler (part of the Go toolchain) compiles `.go` into a native executable.
- **Runtime**: Go has a small built-in runtime (for memory management, garbage collection) that’s statically linked into the final binary. No separate runtime installation is needed after compilation.
- **SDK**: The Go installation (often called the Go toolchain) includes the compiler, `go` command, and standard library.

To **run** a Go program: Once compiled, the binary runs natively without extra installs.  
To **develop** in Go: Install the Go toolchain (which includes compiler, runtime, tools).

---

### 6. C/C++
- **Source Code**: `.c`/`.cpp` files
- **Compiler**: `gcc`/`clang`/`msvc` compiles code to native machine code.
- **Runtime**: C and C++ rely mostly on the operating system and the C/C++ standard libraries. There’s no special runtime environment like JVM or CLR. The OS and standard libs are enough.
- **SDK**: Typically you just have a compiler (like GCC or Clang) and standard library headers. The term SDK is not commonly used. On Windows, you might have a Windows SDK for system libraries.

To **run** a C/C++ program: Just the compiled binary and standard libraries (which come with the OS).  
To **develop**: A compiler toolchain (GCC or Clang), plus any needed headers and libraries.

---

### 7. Other .NET Languages (F#, VB.NET)
- Same ecosystem as C#:  
  - Use the **.NET SDK** for development (compiler + runtime),  
  - The **.NET runtime (CLR)** for execution.

---

### 8. JVM Languages (Kotlin, Scala)
- **Compiler**: Language-specific compilers that produce Java bytecode.
- **Runtime**: **JVM**
- **SDK**: JDK is typically sufficient (Kotlin and Scala can be installed via package managers to integrate with the JVM).  
They rely on the same underlying JVM runtime and standard JDK environment.

---

## General Patterns

- **Interpreted Languages** (Python, JavaScript in browser) need:
  - An Interpreter that also acts as the runtime.

- **Compiled-to-VM Languages** (Java, C#):
  - You write code → Compiler produces intermediate code (bytecode/IL) → A runtime VM (JVM, CLR) executes it.
  - You need an SDK during development (includes compiler + tools).
  - You need a runtime (JRE, .NET runtime) to run the resulting program.

- **Compiled-to-Native Languages** (C, C++, Go):
  - You write code → Compiler produces a native executable.
  - Running the executable just needs the OS (and possibly some system libraries).
  - During development, you need the compiler and possibly an SDK or toolchain.

---

## Terminology Quick Reference

- **Interpreter**: Executes source code directly.  
- **Compiler**: Transforms source code into another form (bytecode or machine code) before execution.  
- **Runtime**: The environment that supports code execution at run time (memory management, libraries). Examples: JVM, CLR, Python interpreter itself.
- **SDK**: A collection of tools, compilers, and libraries needed to develop and build applications in a certain language/framework.

This cheatsheet should help you understand what each language’s ecosystem requires to develop (SDK, compiler) and to run (runtime, interpreter, VM). It also explains where these terms fit into the bigger picture of software development.