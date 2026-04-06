# ☕ Java OOPs — Complete Interview Notes

> **Purpose:** Study + Revision notes for Java OOP Interview Preparation  
> **Topics Covered:** OOP Basics, Classes, Objects, Methods, Overloading, Memory Management, Arrays

---

## 📌 Table of Contents
1. [Object-Oriented Programming (OOP)](#1-object-oriented-programming-oop)
2. [Classes in Java](#2-classes-in-java)
3. [Objects in Java](#3-objects-in-java)
4. [Methods in Java](#4-methods-in-java)
5. [Method Overloading](#5-method-overloading)
6. [Memory Management — Stack & Heap](#6-memory-management--stack--heap)
7. [Arrays in Java](#7-arrays-in-java)
8. [Quick Revision Cheatsheet](#8-quick-revision-cheatsheet)
9. [Interview Questions & Answers](#9-interview-questions--answers)

---

## 1. Object-Oriented Programming (OOP)

### 🔑 What is OOP?
Java is an **Object-Oriented Programming language**, which means it models real-world entities as **objects**.

### 🌍 Real World Analogy
Everything around us is an object — a pen, a mouse, a glass.

Every object has two things:
| Property | Meaning | Example |
|----------|---------|---------|
| **Knows something** | Has properties/attributes | A car has color, speed |
| **Does something** | Has behavior/methods | A car can drive, brake |

### 🏗️ How are Objects Created in Java?
```
Source Code (.java) → Compiler → Byte Code (.class) → JVM → Object
```
- You write a **class** (blueprint)
- **JVM** uses that blueprint to create an **object**
- The class file is compiled to **bytecode**, which JVM reads

> 💡 **Key Point:** JVM creates objects, but it needs a blueprint (class) to do so.

---

## 2. Classes in Java

### 🔑 What is a Class?
A class is a **user-defined blueprint/prototype** from which objects are created.

- Contains **methods** (behavior) and **variables** (properties)
- **Does NOT occupy memory** by itself
- You can create **any number of classes** in a program
- Everything in Java is written **inside a class**

### 📝 Syntax
```java
class ClassName {
    // variables (properties)
    // methods (behavior)
}
```

### 💻 Example
```java
class Car {
    String color;   // property
    int speed;      // property

    public void drive() {       // behavior
        System.out.println("Car is driving!");
    }
}
```

---

## 3. Objects in Java

### 🔑 What is an Object?
When a class is instantiated (an object is created from it), it is called an **instance** of the class.

- All instances **share the same attributes and behavior** defined in the class
- Objects are created in the **Heap** memory (more on this in Memory Management)

### 📝 Syntax to Create an Object
```java
ClassName referenceVariable = new ClassName();
```

| Part | Purpose |
|------|---------|
| `ClassName` | The blueprint |
| `referenceVariable` | Holds the address of the object |
| `new` | Allocates space in heap memory |
| `ClassName()` | Calls the constructor |

### 💻 Example
```java
class Car {
    public void drive() {
        System.out.println("Driving...");
    }
}

class Main {
    public static void main(String[] args) {
        Car myCar = new Car();   // object created
        myCar.drive();           // calling method using reference variable
    }
}
```

> 💡 **Key Point:** A **reference variable** stores the **address** of the object in heap, not the object itself.

---

## 4. Methods in Java

### 🔑 What is a Method?
A method is a **collection of statements** that perform a specific task and optionally return a result.

- Allows **code reuse** without retyping
- Every class has behavior defined through methods
- Methods are identified by `()` (round brackets)
- You must specify **access modifier** and **return type**

### 📝 Syntax
```java
accessModifier returnType methodName(parameters) {
    // statements
    return value; // if return type is not void
}
```

### 🔄 Return Types
| Return Type | Use Case |
|-------------|----------|
| `void` | Method returns nothing |
| `int` | Returns an integer |
| `String` | Returns a string |
| `boolean` | Returns true/false |
| `double` | Returns a decimal |

### 💻 Example
```java
class Computer {

    // void method - returns nothing
    public void playMusic() {
        System.out.println("Music Playing...");
    }

    // method with return type
    public int add(int a, int b) {
        return a + b;   // 'return' stops execution here
    }

    // method with String return
    public String greet(String name) {
        return "Hello, " + name;
    }
}

class Main {
    public static void main(String[] args) {
        Computer c = new Computer();
        c.playMusic();                          // Output: Music Playing...
        System.out.println(c.add(3, 5));        // Output: 8
        System.out.println(c.greet("Arjun"));   // Output: Hello, Arjun
    }
}
```

> ⚠️ **Important:** `return` keyword **stops execution** of the method. No statements after `return` will run.

### 🏁 The Main Method
```java
public static void main(String[] args)
```
- This is the **entry point** of every Java program
- Execution **always begins** from the main method

---

## 5. Method Overloading

### 🔑 What is Method Overloading?
Having **more than one method with the same name** in a class, but with **different parameters**.

> Also called: **Compile-time Polymorphism / Static Polymorphism / Early Binding**

### ✅ Rules for Overloading
| Condition | Valid? |
|-----------|--------|
| Same name, different number of parameters | ✅ Yes |
| Same name, different parameter types | ✅ Yes |
| Same name, different parameter order | ✅ Yes |
| Same name, same parameters, different return type | ❌ No |

> 💡 **Return type does NOT matter** for overloading. Only **method name + parameters** matter.

### 💻 Example
```java
class Calculator {

    // 1. Different number of parameters
    public int add(int a, int b) {
        return a + b;
    }

    public int add(int a, int b, int c) {
        return a + b + c;
    }

    // 2. Different parameter types
    public double add(double a, double b) {
        return a + b;
    }

    // 3. Different order of parameter types
    public void display(int a, String b) {
        System.out.println(a + " " + b);
    }

    public void display(String a, int b) {
        System.out.println(a + " " + b);
    }
}

class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(2, 3));         // 5
        System.out.println(calc.add(2, 3, 4));      // 9
        System.out.println(calc.add(2.5, 3.5));     // 6.0
    }
}
```

### 🧠 Priority Rule
> In method overloading, **child argument gets higher priority** over parent argument when both match.

---

## 6. Memory Management — Stack & Heap

### 🔑 Two Types of Memory in Java
Java manages memory using two data structures:

| Memory | Data Structure | Stores |
|--------|---------------|--------|
| **Stack** | LIFO (Last In First Out) | Local variables, method calls, reference variables |
| **Heap** | Object storage | Objects, instance variables |

### 📦 Stack Memory
- Follows **LIFO** principle
- Each method call creates a **stack frame**
- **Local variables** are stored in the stack frame
- When method finishes, its stack frame is **removed**

### 🏗️ Heap Memory
- Stores **objects** (collection of data + methods)
- **Instance variables** live inside objects → so they live in the heap
- Objects remain until **garbage collected**

### 💻 Example — Where Does Each Variable Live?
```java
class Student {
    int instVariable;   // instance variable → stored in HEAP (inside object)

    public static void main(String[] args) {
        int localVariable = 0;          // local variable → stored in STACK
        Student st = new Student();     // 'st' is reference variable → STACK
                                        // new Student() object → HEAP
    }

    public int add(int num1, int num2) {
        return num1 + num2;             // num1, num2 are local → STACK
    }
}
```

### 🗺️ Memory Diagram
```
STACK                          HEAP
┌─────────────────┐           ┌──────────────────────┐
│  main() frame   │           │   Student Object      │
│  localVariable=0│           │   instVariable = 0    │
│  st ──────────────────────► │                       │
└─────────────────┘           └──────────────────────┘
```

### 📋 Summary Table
| What | Where |
|------|-------|
| Local variables | Stack |
| Reference variables | Stack |
| Objects | Heap |
| Instance variables | Heap (inside object) |
| Method declarations | Object (Heap) |
| Method execution / implementation | Stack frame |

---

## 7. Arrays in Java

### 🔑 What is an Array?
An array is a **collection of similar type of data** stored in **contiguous (adjacent) memory locations**.

```
marks = {24, 25, 26, 27}
Memory: [24][25][26][27]  ← stored side by side
```

### 🤔 Why Use Arrays?
Without arrays:
```java
int m1 = 24;
int m2 = 25;
int m3 = 26;   // Tedious! Hard to manage!
int m4 = 27;
```
With arrays:
```java
int[] marks = {24, 25, 26, 27};  // Clean and manageable ✅
```

### 📝 Declaration Syntax
```java
int nums[];    // style 1
int[] nums;    // style 2 (preferred)
```
Both are valid!

### 🏗️ Ways to Create Arrays

#### a) Literal Notation
```java
int[] arr = {1, 2, 3};   // values assigned directly
```

#### b) Object Notation — with values
```java
int[] arr = new int[]{1, 2, 3};
```

#### c) Object Notation — with size only
```java
int[] arr = new int[3];   // default values assigned
arr[0] = 1;
arr[1] = 2;
arr[2] = 3;
```

### 🎯 Default Values (Object Notation)
| Data Type | Default Value |
|-----------|--------------|
| `int`, `byte`, `short`, `long` | `0` |
| `float` | `0.0f` |
| `double` | `0.0d` |
| `boolean` | `false` |
| `char` | `'\u0000'` (null character) |

### 🔍 Accessing & Modifying Array Elements

- Array index starts from **0**
- Last index = **n-1** (where n = length)
- **nth element** is at index `n-1`

```java
int[] nums = {2, 3, 4, 5};

// Accessing elements
System.out.println(nums[0]);   // 2 (1st element)
System.out.println(nums[3]);   // 5 (4th element)

// Modifying elements
nums[0] = 10;
nums[1] = 11;

// Traversing the array
for (int i = 0; i < nums.length; i++) {
    System.out.println(nums[i]);
}

// Enhanced for loop (cleaner)
for (int n : nums) {
    System.out.println(n);
}
```

### 💻 Default Value Check Example
```java
char ch[] = new char[3];   // default: '\u0000'

for (int i = 0; i < ch.length; i++) {
    System.out.println(ch[i]);   // prints empty/null character
}
```

### 📋 Array Quick Reference
| Operation | Code |
|-----------|------|
| Declare | `int[] arr;` |
| Create with size | `arr = new int[5];` |
| Create with values | `int[] arr = {1,2,3};` |
| Access element | `arr[i]` |
| Modify element | `arr[i] = value;` |
| Get length | `arr.length` |
| First element | `arr[0]` |
| Last element | `arr[arr.length - 1]` |

---

## 8. Quick Revision Cheatsheet

```
OOP
├── Class       → Blueprint, no memory, has methods & variables
├── Object      → Instance of class, created in Heap by JVM
├── Method      → Behavior, has return type + access modifier
└── Overloading → Same name, different params (Compile-time polymorphism)

Memory
├── Stack → LIFO, local variables, reference variables, method frames
└── Heap  → Objects, instance variables

Arrays
├── Contiguous memory, same data type
├── Index starts at 0, ends at n-1
└── Default values assigned when created with new keyword
```

---

## 9. Interview Questions & Answers

### Q1. What is OOP?
**A:** OOP is a programming paradigm based on the concept of objects that contain data (properties) and code (behavior/methods). Java is an object-oriented language where everything is modeled as objects.

### Q2. What is the difference between a Class and an Object?
**A:**
| Class | Object |
|-------|--------|
| Blueprint/template | Instance of a class |
| Does not occupy memory | Occupies memory in Heap |
| Defined once | Can be created multiple times |
| `class Car {}` | `Car c = new Car();` |

### Q3. What is Method Overloading? Is it compile-time or runtime?
**A:** Method overloading is having multiple methods with the same name but different parameters (number, type, or order). It is resolved at **compile time**, so it's called **Compile-time Polymorphism** or **Static Polymorphism**.

### Q4. Can we overload methods by changing only the return type?
**A:** **No.** Return type alone is not sufficient for overloading. The compiler uses the method name and parameter list to distinguish methods, not the return type.

### Q5. What is the difference between Stack and Heap memory?
**A:**
| Stack | Heap |
|-------|------|
| LIFO structure | Random access |
| Stores local variables, method calls | Stores objects |
| Memory freed when method returns | Memory freed by Garbage Collector |
| Faster access | Slower access |
| Fixed size | Dynamic size |

### Q6. Where are instance variables stored?
**A:** Instance variables are stored inside the **object**, and objects are stored in the **Heap**. So instance variables are stored in Heap memory.

### Q7. What is a reference variable?
**A:** A reference variable stores the **memory address** (reference) of an object in the heap. It is itself stored in the **Stack**.

### Q8. What are the ways to create an array in Java?
**A:** Three ways:
1. Literal: `int[] arr = {1, 2, 3};`
2. Object with values: `int[] arr = new int[]{1, 2, 3};`
3. Object with size: `int[] arr = new int[3];` (then assign values manually)

### Q9. What is the default value of an int array in Java?
**A:** `0`. When an array is created using `new int[n]`, all elements are initialized to `0` by default.

### Q10. What does the `return` keyword do in a method?
**A:** The `return` keyword **stops the execution** of the method and returns the specified value to the caller. No statements after `return` are executed.

### Q11. What is the main method in Java?
**A:** `public static void main(String[] args)` is the **entry point** of every Java program. The JVM starts execution from this method.

### Q12. What is compile-time polymorphism?
**A:** Compile-time polymorphism (also called static polymorphism or early binding) is when the method to be called is determined at **compile time**. Method overloading is an example of this.

---

*📝 Notes compiled from lecture transcripts | Java OOPs Interview Preparation*
