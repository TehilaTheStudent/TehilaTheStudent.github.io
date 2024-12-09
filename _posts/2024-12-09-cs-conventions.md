---
title: cs-conventions
date: 2024-12-09T21:43:33
categories: [General]
tags: []
---
Here’s a **comprehensive cheat sheet** for **C# coding conventions**, focusing on **file and directory names** with examples, and the standard **comment styles** that integrate well with IDEs like Visual Studio or Visual Studio Code.

---

### **C# File and Directory Naming Conventions**

#### **1. File Names**
- File names should match the name of the class, interface, or enum they contain.
- Use **PascalCase** for file names.
- Keep file names concise yet descriptive.

**Examples**:
```
UserService.cs         // Contains the UserService class
IUserRepository.cs     // Contains the IUserRepository interface
AppSettings.json       // JSON configuration file
Program.cs             // Entry point for the application
```

---

#### **2. Directory Names**
- Use **PascalCase** for directory names.
- Organize directories by feature or functionality.
- Avoid abbreviations unless they are widely recognized.

**Examples**:
```
/Controllers/          // For Web API controllers
/Models/               // For data models
/Services/             // For service classes
/Repositories/         // For repository interfaces and implementations
/Helpers/              // For utility or helper functions
```

**Sample Structure**:
```
MyApplication/
├── MyApplication.sln      // Solution file
├── Program.cs             // Entry point
├── AppSettings.json       // Configuration file
├── Controllers/
│   └── UserController.cs
├── Models/
│   └── UserModel.cs
├── Services/
│   ├── UserService.cs
│   └── AuthenticationService.cs
├── Repositories/
│   ├── IUserRepository.cs
│   └── UserRepository.cs
```

---

### **C# Comment Conventions**

C# uses **XML documentation comments**, which are directly visible in IDEs like Visual Studio. These comments allow tools to generate API documentation and provide IntelliSense support.

#### **1. XML Documentation Comments**
- Use `///` to document classes, methods, and properties.
- Common tags include:
  - `<summary>`: Describes the class, method, or property.
  - `<param>`: Describes a method parameter.
  - `<returns>`: Describes the return value.
  - `<exception>`: Documents exceptions thrown by a method.

---

#### **2. XML Comment Examples**

##### **Class Documentation**
```csharp
/// <summary>
/// Provides methods to manage user-related operations.
/// </summary>
public class UserService {
    // Class implementation
}
```

##### **Method Documentation**
```csharp
/// <summary>
/// Retrieves user data based on the provided user ID.
/// </summary>
/// <param name="userId">The unique identifier of the user.</param>
/// <returns>A User object containing the user's details.</returns>
/// <exception cref="ArgumentNullException">Thrown when userId is null.</exception>
public User GetUser(int userId) {
    // Method implementation
}
```

##### **Property Documentation**
```csharp
/// <summary>
/// Gets or sets the user's first name.
/// </summary>
public string FirstName { get; set; }
```

##### **Constructor Documentation**
```csharp
/// <summary>
/// Initializes a new instance of the <see cref="UserService"/> class.
/// </summary>
/// <param name="repository">The user repository instance.</param>
public UserService(IUserRepository repository) {
    // Constructor implementation
}
```

---

#### **3. Inline and Block Comments**

- **Single-Line Comments**: Use `//` for brief explanations.
```csharp
// This is a single-line comment
int userCount = 0;
```

- **Multi-Line Comments**: Use `/* */` for larger explanations.
```csharp
/*
 * This block of code initializes the application settings
 * and validates the configuration files.
 */
```

---

### **General C# Coding Style**

#### **1. Naming Conventions**
- **Classes and Interfaces**: Use `PascalCase`.
  - Class: `UserService`
  - Interface: `IUserRepository`
- **Methods**: Use `PascalCase`.
  - Example: `GetUserById`
- **Variables**: Use `camelCase`.
  - Example: `userName`, `totalCount`
- **Constants**: Use `UPPER_SNAKE_CASE`.
  - Example: `MAX_RETRIES`, `DEFAULT_TIMEOUT`

#### **2. Indentation**
- Use **4 spaces** per indentation level.
```csharp
if (user.IsActive) {
    Console.WriteLine("User is active.");
}
```

#### **3. Line Length**
- Keep lines under **120 characters** for better readability.

---

### **Summary**

- **File and Directory Naming**:
  - File names and directory names should use **PascalCase**.
  - Organize directories by functionality (e.g., `/Controllers`, `/Models`, `/Services`).

- **Commenting Style**:
  - Use XML comments (`///`) for documentation visible in the IDE.
  - Use `<summary>`, `<param>`, and `<returns>` tags to describe code functionality.
  - Use inline (`//`) or block comments (`/* */`) for internal logic explanations.

- **Code Readability**:
  - Follow consistent naming conventions.
  - Use proper indentation and line breaks.

By adhering to these conventions, your code will remain clean, maintainable, and well-documented, improving collaboration and readability. Let me know if you'd like further clarifications or examples!