---
title: statically-typed
date: 2024-12-09T21:43:33
categories: [General]
tags: []
---
Here’s a **comprehensive cheat sheet** covering a wide range of keywords and features for **C#, Java, and C++**. It includes categories like classes, inheritance, memory management, concurrency, and special features.

---

### **General Keywords and Features Cheat Sheet**

#### **Classes and Inheritance**

| **Concept**                  | **Java**                              | **C#**                               | **C++**                              | **Notes**                                                                 |
|-------------------------------|---------------------------------------|---------------------------------------|---------------------------------------|---------------------------------------------------------------------------|
| Define a class               | `class`                              | `class`                              | `class`                              | Common keyword to define classes in all three languages.                 |
| Define an abstract class     | `abstract`                           | `abstract`                           | None, use `= 0`                      | Abstract classes cannot be instantiated directly.                        |
| Prevent inheritance          | `final`                              | `sealed`                             | `final`                              | Prevents further inheritance.                                             |
| Allow overriding             | Implicit (`virtual` by default)       | `virtual`                            | `virtual`                            | Methods must be explicitly marked `virtual` in C# and C++.               |
| Force overriding             | `@Override` (annotation)             | `override`                           | `override`                           | C++11 introduced `override` for clarity.                                 |
| Constructor                  | Same name as the class               | Same name as the class               | Same name as the class               | Initializes an object.                                                   |
| Destructor                   | `finalize()`                         | `~ClassName()`                       | `~ClassName()`                       | Handles cleanup. Use sparingly, favor RAII in C++.                       |
| Interface                    | `interface`                          | `interface`                          | Pure virtual class                   | Interfaces enforce implementation of methods.                            |
| Default methods in interface | `default`                            | No equivalent                        | No equivalent                        | Java allows default methods; others do not.                              |
| Multiple inheritance         | Not supported (use interfaces)       | Not supported (use interfaces)       | Supported                            | C++ supports multiple inheritance natively.                              |

---

#### **Memory Management**

| **Concept**                  | **Java**                              | **C#**                               | **C++**                              | **Notes**                                                                 |
|-------------------------------|---------------------------------------|---------------------------------------|---------------------------------------|---------------------------------------------------------------------------|
| Manual memory management     | Not available                        | Not available                        | `new`, `delete`, `malloc`, `free`    | Java and C# have garbage collection; C++ requires manual memory management. |
| Garbage collection           | Automatic                            | Automatic                            | Not available                        | Java and C# automatically reclaim unused memory.                         |
| Stack vs Heap                | Abstracted                           | Abstracted                           | Explicit                              | C++ allows explicit allocation on stack or heap.                         |
| `const` keyword              | `final`                              | `const`                              | `const`, `constexpr`                 | C++ provides more control with `constexpr` (compile-time constants).     |
| Pointer support              | No                                   | Limited                              | Yes                                  | Pointers are a core feature in C++.                                      |
| Smart pointers               | Not available                        | Not available                        | `std::shared_ptr`, `std::unique_ptr` | C++ offers RAII-compliant memory management via smart pointers.          |

---

#### **Concurrency**

| **Concept**                  | **Java**                              | **C#**                               | **C++**                              | **Notes**                                                                 |
|-------------------------------|---------------------------------------|---------------------------------------|---------------------------------------|---------------------------------------------------------------------------|
| Threads                      | `Thread` class, `Runnable` interface | `Thread` class, `Task` class         | `std::thread`                        | All three support threads via standard libraries.                        |
| Synchronization              | `synchronized`                       | `lock`, `Monitor`                    | `std::mutex`, `std::lock_guard`      | C++ requires explicit synchronization primitives.                        |
| Asynchronous programming     | `CompletableFuture`, `Future`        | `async`, `await`                     | `std::future`, `std::async`          | Async programming is native to C# and C++11 onward.                      |
| Volatile keyword             | `volatile`                           | `volatile`                           | `volatile`                           | Used to prevent compiler optimizations on variables.                     |

---

#### **Modules and Imports**

| **Concept**                  | **Java**                              | **C#**                               | **C++**                              | **Notes**                                                                 |
|-------------------------------|---------------------------------------|---------------------------------------|---------------------------------------|---------------------------------------------------------------------------|
| Import                       | `import`                             | `using`                              | `#include`                           | Each language uses a different keyword for importing dependencies.       |
| Namespace management         | `package`                            | `namespace`                          | `namespace`                          | Both C# and C++ use `namespace`; Java uses `package`.                    |
| Modules                      | `module` (Java 9+)                   | No explicit module system            | `module` (C++20)                     | C++20 introduced modules for cleaner imports and encapsulation.          |

---

#### **Special Features**

| **Feature**                  | **Java**                              | **C#**                               | **C++**                              | **Notes**                                                                 |
|-------------------------------|---------------------------------------|---------------------------------------|---------------------------------------|---------------------------------------------------------------------------|
| Lambda expressions           | `->`                                 | `=>`                                 | `[ ]( ) { }`                         | All three support functional programming paradigms.                      |
| Properties                   | Getters/setters manually             | `get` and `set` keywords             | Not native (use functions)           | C# has built-in support for properties.                                  |
| Enums                        | `enum`                               | `enum`                               | `enum`, `enum class`                 | C++ has strongly-typed `enum class` for safety.                          |
| Reflection                   | `Class.forName`, `getMethods()`      | `Type`, `GetMethods()`               | Limited (`typeid`, RTTI)             | Reflection is more powerful in Java and C#.                              |
| Generics                     | `<T>`                                | `<T>`                                | `<T>`                                | Supported in all three languages.                                        |
| Tuples                       | `Pair`, `Tuple` (Java 8+)            | `Tuple`                              | `std::tuple`                         | All three support tuples for grouped data.                               |
| Attributes/Annotations       | `@Annotation`                       | `[Attribute]`                        | Limited macros                       | Java and C# support extensive metadata with annotations/attributes.      |

---
Here's a **Data Structures Table** for **C++**, **C#**, and **Java**, focusing on their usage, characteristics, and native support.

---

### **Data Structures Comparison: C++, C#, and Java**

| **Structure**           | **C++**                                    | **C#**                                   | **Java**                                | **Notes**                                                                 |
|--------------------------|--------------------------------------------|------------------------------------------|-----------------------------------------|---------------------------------------------------------------------------|
| **Arrays**              | `std::array`, native arrays (`int arr[]`)  | `Array`                                  | `Array`, `ArrayList`                   | Fixed-size arrays in all; dynamic arrays (e.g., `ArrayList`) in Java and `List<T>` in C#. |
| **Lists**               | `std::list`                                | `List<T>`                                | `LinkedList`                           | C++ has `std::list` for doubly linked lists; C# and Java provide generic and linked list support. |
| **Vectors**             | `std::vector`                              | `List<T>`                                | `ArrayList`                            | `std::vector` in C++ is resizable; in C# and Java, dynamic arrays serve similar purposes. |
| **Sets**                | `std::set`, `std::unordered_set`           | `HashSet<T>`, `SortedSet<T>`             | `HashSet`, `TreeSet`                   | All support sets; unordered in C++/C# (`HashSet`), sorted (`TreeSet`).   |
| **Maps/Dictionaries**   | `std::map`, `std::unordered_map`           | `Dictionary<TKey, TValue>`, `SortedList` | `HashMap`, `TreeMap`                   | Support for key-value stores in all; sorted maps are `TreeMap` (Java) and `std::map` (C++). |
| **Queues**              | `std::queue`, `std::priority_queue`        | `Queue<T>`, `PriorityQueue<T>`           | `Queue`, `PriorityQueue`               | All three support both standard and priority queues.                     |
| **Stacks**              | `std::stack`                               | `Stack<T>`                               | `Stack`                                | Similar stack implementations in all languages.                         |
| **Deques**              | `std::deque`                               | `Deque<T>`                               | `ArrayDeque`                           | Double-ended queues in all languages, with high efficiency for both ends. |
| **Graphs**              | Custom (via adjacency list or matrix)      | Custom (via adjacency list or matrix)    | Custom (via adjacency list or matrix)  | No native graph structure; libraries like Boost (C++) or external packages are used. |
| **Trees**               | Custom                                     | Custom                                   | Custom                                 | Trees are implemented manually or via libraries.                        |
| **Hash Tables**         | `std::unordered_map`, `std::unordered_set` | `Dictionary<TKey, TValue>`               | `HashMap`, `HashSet`                   | C++ uses `std::unordered_*`; C# and Java have similar hash-based collections. |

---


### **Coding Examples for Each Category**

#### **Classes and Inheritance**

**Java**
```java
abstract class Animal {
    abstract void sound();
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Bark");
    }
}
```

**C#**
```csharp
abstract class Animal {
    public abstract void Sound();
}

class Dog : Animal {
    public override void Sound() {
        Console.WriteLine("Bark");
    }
}
```

**C++**
```cpp
class Animal {
public:
    virtual void Sound() = 0; // Pure virtual function
};

class Dog : public Animal {
public:
    void Sound() override {
        std::cout << "Bark" << std::endl;
    }
};
```

---

#### **Memory Management**

**Java**
```java
final int MAX = 10; // Constant
String name = new String("John"); // Allocated on heap
```

**C#**
```csharp
const int MAX = 10; // Constant
string name = new string("John"); // Allocated on heap
```

**C++**
```cpp
const int MAX = 10; // Constant
std::string name = "John"; // On stack
std::string* namePtr = new std::string("John"); // On heap
delete namePtr; // Manual cleanup
```

---

#### **Concurrency**

**Java**
```java
Thread thread = new Thread(() -> System.out.println("Hello"));
thread.start();
```

**C#**
```csharp
Task.Run(() => Console.WriteLine("Hello"));
```

**C++**
```cpp
std::thread t([]() { std::cout << "Hello" << std::endl; });
t.join();
```

---

#### **Modules and Imports**

**Java**
```java
import java.util.ArrayList;
```

**C#**
```csharp
using System.Collections.Generic;
```

**C++**
```cpp
#include <vector>
```

---

This cheat sheet is designed to cover **wide-ranging concepts and keywords** comprehensively across **Java**, **C#**, and **C++**, helping you refer to it as an all-in-one guide. Let me know if you’d like to expand on any section!