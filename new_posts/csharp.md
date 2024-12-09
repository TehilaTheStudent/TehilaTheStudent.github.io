### **Nullable Types and Features in C#**

**Nullable types** in C# are a way to handle the absence of a value for value types (like `int`, `double`, `DateTime`, etc.) and improve type safety when working with `null`.

---

### **1. Nullable Value Types**

- **What It Is**: Normally, value types (like `int`, `bool`, `double`) cannot be `null`. Nullable value types (`int?`, `double?`) allow value types to hold a `null` value.
- **Syntax**: Use `?` after the type.
  ```csharp
  int? age = null; // Nullable int
  if (age.HasValue)
      Console.WriteLine($"Age: {age.Value}");
  else
      Console.WriteLine("Age is not set.");
  ```

#### **Key Properties and Methods**
- `.HasValue`: Returns `true` if the variable contains a value, `false` otherwise.
- `.Value`: Retrieves the value (throws an exception if `null`).

---

### **2. Nullable Reference Types (`null` Safety)**

Introduced in **C# 8.0**, nullable reference types aim to reduce `NullReferenceException` by providing **compile-time null-safety**.

- **What It Is**: Reference types (`string`, `object`) are nullable by default. Enabling nullable reference types introduces warnings when a nullable value might be used unsafely.
- **Syntax**:
  - Add `?` after a reference type to make it nullable.
  - Use `!` (null-forgiving operator) to suppress warnings when you are sure a value is not `null`.

**Example**:
```csharp
#nullable enable // Enable nullable reference types
string? name = null; // Nullable
Console.WriteLine(name?.Length); // Safe: Will not throw NullReferenceException
Console.WriteLine(name.Length); // Warning: Possible null dereference
```

#### **Key Keywords**
- `?`: Marks a type as nullable.
- `!`: Suppresses nullability warnings.

---

### **3. Cool New Features in C#**

#### **A. Records (C# 9.0)**
- **What It Is**: Immutable data types that are value-based, ideal for defining simple data containers.
- **Syntax**:
  ```csharp
  public record Person(string FirstName, string LastName);
  var person = new Person("John", "Doe");
  Console.WriteLine(person.FirstName); // Output: John
  ```

#### **B. Pattern Matching Enhancements**
- **Switch Expressions (C# 8.0)**:
  ```csharp
  string GetDayType(int day) => day switch
  {
      0 => "Sunday",
      1 => "Monday",
      _ => "Other",
  };
  ```

- **Property Patterns (C# 8.0)**:
  ```csharp
  if (person is { FirstName: "John", LastName: "Doe" })
      Console.WriteLine("It's John Doe!");
  ```

#### **C. Default Interface Methods (C# 8.0)**
- Interfaces can now provide default implementations for methods.
- **Example**:
  ```csharp
  public interface ILogger
  {
      void Log(string message) => Console.WriteLine($"Log: {message}");
  }
  ```

#### **D. Init-Only Properties (C# 9.0)**
- Allows properties to be set only during object initialization.
- **Example**:
  ```csharp
  public class Car
  {
      public string Model { get; init; }
  }

  var car = new Car { Model = "Tesla" };
  ```

#### **E. Top-Level Statements (C# 9.0)**
- Simplifies `Main` method for small programs.
- **Example**:
  ```csharp
  Console.WriteLine("Hello, World!");
  ```

#### **F. Global Using Directives (C# 10.0)**
- Eliminates repetitive `using` statements across files.
- **Example**:
  ```csharp
  // In a single file (e.g., `GlobalUsings.cs`)
  global using System;
  global using System.Collections.Generic;
  ```

#### **G. File-Scoped Namespaces (C# 10.0)**
- Simplifies namespace declaration.
- **Example**:
  ```csharp
  namespace MyApp;

  public class MyClass
  {
      // Code here
  }
  ```

#### **H. Null-Coalescing Assignment (`??=`)**
- Assigns a value only if the variable is `null`.
- **Example**:
  ```csharp
  string? name = null;
  name ??= "Default Name";
  Console.WriteLine(name); // Output: Default Name
  ```

#### **I. Async Streams (C# 8.0)**
- Provides asynchronous iteration over data streams.
- **Example**:
  ```csharp
  await foreach (var item in GetDataAsync())
  {
      Console.WriteLine(item);
  }
  ```

#### **J. Lambda Improvements (C# 10.0)**
- **Lambda Return Types**: Lambdas can now have explicit return types.
  ```csharp
  Func<int, int> square = (int x) => x * x;
  ```

---

### **Summary**

| **Feature**                | **Description**                                              | **Introduced In** |
|-----------------------------|-------------------------------------------------------------|-------------------|
| **Nullable Value Types**    | Allows value types to hold `null`.                          | C# 2.0           |
| **Nullable Reference Types**| Enables compile-time null safety.                          | C# 8.0           |
| **Records**                 | Immutable, value-based types.                              | C# 9.0           |
| **Pattern Matching**        | Enhancements for cleaner condition checks.                 | C# 8.0+          |
| **Default Interface Methods** | Methods with default implementations in interfaces.       | C# 8.0           |
| **Init-Only Properties**    | Immutable properties after initialization.                 | C# 9.0           |
| **Top-Level Statements**    | Simplifies entry-point programs.                           | C# 9.0           |
| **Global Usings**           | Eliminates repetitive `using` statements.                  | C# 10.0          |
| **Async Streams**           | Asynchronous iteration with `IAsyncEnumerable`.            | C# 8.0           |
| **Null-Coalescing Assignment** | Assign a default value if the variable is `null`.        | C# 8.0           |

These features make C# a modern, feature-rich, and developer-friendly language, especially with its focus on immutability, null safety, and functional paradigms. Let me know if you want examples or deeper dives into specific features!