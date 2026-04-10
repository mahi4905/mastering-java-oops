# ☕ Java OOPs — Complete Interview Notes (Part 3)

> **Topics Covered:** Encapsulation, Getters & Setters, `this` Keyword, Constructors, super() & this() methods, Object Class

---

## 📌 Table of Contents
1. [Encapsulation](#1-encapsulation)
2. [Getters & Setters](#2-getters--setters)
3. [Instance vs Local Variables & `this` Keyword](#3-instance-vs-local-variables--this-keyword)
4. [Constructors in Java](#4-constructors-in-java)
5. [Types of Constructors](#5-types-of-constructors)
6. [super(), this() & Object Class](#6-super-this--object-class)
7. [Quick Revision Cheatsheet](#7-quick-revision-cheatsheet)
8. [Interview Questions & Answers](#8-interview-questions--answers)

---

## 1. Encapsulation

### 🔑 What is Encapsulation?
**Encapsulation** is the process of **binding data (variables) with methods** inside a class to make the program secure.

> Think of it like a **capsule** — everything (data + behavior) is wrapped together inside the class.

```
┌─────────────────────────────┐
│         Class A  (Capsule)  │
│  ┌─────────────────────┐    │
│  │  private int a;     │    │  ← Data (hidden)
│  ├─────────────────────┤    │
│  │  public setA(num)   │    │  ← Methods (exposed)
│  │  public getA()      │    │
│  └─────────────────────┘    │
└─────────────────────────────┘
```

### 🛡️ How to Achieve Encapsulation?
Using **access specifiers**:
| Access Specifier | Visibility |
|-----------------|------------|
| `private` | Only within the same class |
| `default` | Within the same package |
| `protected` | Same package + subclasses |
| `public` | Everywhere |

> ✅ **Best Practice:** Make variables `private` and methods `public`.

### 🎯 Benefits of Encapsulation
1. **Security** — Data is hidden from outside access
2. **Abstraction** — Helps achieve abstraction (hide implementation details)
3. **Logging/Control** — You can add validation or logging inside setters
4. **Maintainability** — Easy to change internal implementation without affecting outside code

### 💻 Example
```java
class BankAccount {
    private double balance;   // hidden from outside

    // Setter with validation
    public void setBalance(double amount) {
        if (amount >= 0) {
            balance = amount;
        } else {
            System.out.println("Invalid amount!");
        }
    }

    // Getter
    public double getBalance() {
        return balance;
    }
}

class Main {
    public static void main(String[] args) {
        BankAccount acc = new BankAccount();
        acc.setBalance(5000);
        System.out.println(acc.getBalance());   // 5000.0
        acc.setBalance(-100);                   // Invalid amount!
        // acc.balance = -100;                  // ❌ ERROR — private!
    }
}
```

---

## 2. Getters & Setters

### 🔑 What are Getters and Setters?
- **Getter** — A method used to **get/read** the value of a private variable
- **Setter** — A method used to **set/write** the value of a private variable

They **protect your data** and make your code more secure and maintainable.

### 📝 Naming Convention
- First letter of variable name is **capitalized** in method name
- Getter: `get` + `VariableName` → `getAge()`
- Setter: `set` + `VariableName` → `setAge(int age)`

### 💻 Example
```java
class Student {
    private String name;
    private int age;
    private double marks;

    // Getter for name
    public String getName() {
        return name;
    }

    // Setter for name
    public void setName(String name) {
        this.name = name;
    }

    // Getter for age
    public int getAge() {
        return age;
    }

    // Setter for age
    public void setAge(int age) {
        if (age > 0) {
            this.age = age;
        }
    }

    // Getter for marks
    public double getMarks() {
        return marks;
    }

    // Setter for marks
    public void setMarks(double marks) {
        this.marks = marks;
    }
}

class Main {
    public static void main(String[] args) {
        Student s = new Student();
        s.setName("Arjun");
        s.setAge(20);
        s.setMarks(95.5);

        System.out.println(s.getName());    // Arjun
        System.out.println(s.getAge());     // 20
        System.out.println(s.getMarks());   // 95.5
    }
}
```

### ⚡ Eclipse Shortcut
> Right-click on editor → **Source Action** or **Insert Code** → **Generate Getters and Setters**

> 💡 **Note:** It is NOT compulsory to have getters/setters for ALL variables. Only create them as needed.

---

## 3. Instance vs Local Variables & `this` Keyword

### 🔑 Instance Variable vs Local Variable

| | Instance Variable | Local Variable |
|--|-----------------|---------------|
| **Declared** | Inside class, outside method | Inside method/constructor |
| **Default value** | Yes (0, null, false) | ❌ No default value |
| **Created** | When object is created | When method is called |
| **Destroyed** | When object is destroyed | When method returns |
| **Stored in** | Heap (inside object) | Stack (inside stack frame) |

```java
class Example {
    int instanceVar = 10;   // instance variable — has default value

    public void method() {
        int localVar = 20;  // local variable — MUST be initialized before use
        System.out.println(instanceVar);  // ✅
        System.out.println(localVar);     // ✅ (initialized above)
    }
}
```

### ⚠️ Name Conflict Problem
```java
class Student {
    int age = 25;   // instance variable

    public void setAge(int age) {
        // Problem: both instance var and parameter are named 'age'
        age = age;   // ❌ This assigns parameter to itself! Bug!
    }
}
```

### ✅ Solution — `this` Keyword

### 🔑 What is `this`?
`this` refers to the **current object** — the object that is calling the method.

```java
class Student {
    int age;

    public void setAge(int age) {
        this.age = age;   // ✅ this.age = instance variable, age = parameter
    }
}
```

### 🛠️ Uses of `this` Keyword

#### 1. Resolve name conflict (instance vs local variable)
```java
class Person {
    String name;

    public void setName(String name) {
        this.name = name;   // this.name = instance, name = parameter
    }
}
```

#### 2. Pass current object as argument
```java
class Printer {
    public void print(Person p) {
        System.out.println(p.name);
    }
}

class Person {
    String name = "Arjun";

    public void display(Printer printer) {
        printer.print(this);   // passing current object
    }
}
```

#### 3. Return current class instance
```java
class Builder {
    int x;

    public Builder setX(int x) {
        this.x = x;
        return this;   // returns current object (method chaining)
    }
}
```

#### 4. Call current class constructor — `this()`
```java
class Demo {
    int a, b;

    Demo() {
        this(0, 0);   // calls parameterized constructor
    }

    Demo(int a, int b) {
        this.a = a;
        this.b = b;
    }
}
```

> ⚠️ **Rule:** `this()` must be the **first statement** in a constructor.

---

## 4. Constructors in Java

### 🔑 What is a Constructor?
A constructor is a **special method** that is automatically called when an object is created. It is used to **initialize the object**.

### 🧠 What Happens Without a Constructor?
```java
Student s = new Student();
// s.name = null (String default)
// s.age  = 0    (int default)
// s.gpa  = 0.0  (double default)
```
Default values are assigned automatically.

### 📋 Properties of a Constructor

| Property | Detail |
|----------|--------|
| Name | Must be **same as class name** |
| Return type | **None** (not even void) |
| Called | **Automatically** at object creation |
| Called how many times | **Only once** per object |
| Methods | Can be called **any number of times** |
| Memory | Memory for object is allocated when constructor is called |

### 📝 Syntax
```java
class Human {
    // Constructor
    public Human() {
        // initialization code
        System.out.println("Human object created!");
    }
}

class Main {
    public static void main(String[] args) {
        Human h = new Human();   // Constructor called automatically
    }
}
```

### 💻 Constructor with Initialization
```java
class Student {
    String name;
    int age;

    // Constructor sets initial values
    public Student() {
        name = "Unknown";
        age = 0;
    }
}
```

---

## 5. Types of Constructors

### Two Types of Constructors

| | Default Constructor | Parameterized Constructor |
|--|--------------------|-----------------------------|
| **Parameters** | None | One or more |
| **Purpose** | Assigns default values | Assigns custom values |
| **Created by Java** | Yes, if no constructor defined | No |
| **Values** | 0, null, false | Whatever you pass |

### 🔑 Default Constructor
```java
class Car {
    String color;
    int speed;

    // Default constructor — no parameters
    public Car() {
        color = "White";
        speed = 0;
        System.out.println("Default Car created");
    }
}
```

> 💡 If you **don't write any constructor**, Java **automatically creates** a blank default constructor:
> ```java
> public Car() { }   // Java adds this invisibly
> ```

### 🔑 Parameterized Constructor
```java
class Car {
    String color;
    int speed;

    // Parameterized constructor
    public Car(String color, int speed) {
        this.color = color;
        this.speed = speed;
    }
}

class Main {
    public static void main(String[] args) {
        Car c1 = new Car("Red", 120);    // custom values
        Car c2 = new Car("Blue", 100);   // different values
        System.out.println(c1.color);    // Red
        System.out.println(c2.color);    // Blue
    }
}
```

### ⚠️ Important Rule
> If you define a **parameterized constructor**, Java will **NOT** automatically create a default constructor.
> You must explicitly define the default constructor if you need it.

```java
class Car {
    Car(String color) { }   // parameterized defined

    // Car() { }  ← Java no longer auto-creates this!
}

Car c = new Car();          // ❌ ERROR — no default constructor!
Car c = new Car("Red");     // ✅ OK
```

### Constructor Overloading
```java
class Student {
    String name;
    int age;

    Student() {
        name = "Unknown";
        age = 0;
    }

    Student(String name) {
        this.name = name;
        age = 0;
    }

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

---

## 6. super(), this() & Object Class

### 🔑 Object Class
> **Every class in Java automatically extends the `Object` class**, even if you don't write `extends Object`.

```java
class Animal { }
// Java internally treats this as:
// class Animal extends Object { }
```

- `Object` is the **root class** of all Java classes
- It contains useful methods like `toString()`, `equals()`, `hashCode()`, `getClass()`, etc.

### 🏗️ Class Hierarchy
```
Object
  └── Animal (extends Object implicitly)
        └── Dog (extends Animal)
```

### 🔑 super() Method

`super()` calls the **constructor of the parent/superclass**.

```java
class Animal {
    Animal() {
        System.out.println("Animal constructor");
    }
    Animal(String name) {
        System.out.println("Animal: " + name);
    }
}

class Dog extends Animal {
    Dog() {
        super();            // calls Animal() — default constructor of parent
        System.out.println("Dog constructor");
    }

    Dog(String name) {
        super(name);        // calls Animal(String) — parameterized constructor of parent
        System.out.println("Dog: " + name);
    }
}
```

> 💡 **By default**, the **first statement** of every constructor is `super()` — even if you don't write it. Java adds it automatically.

### 🔑 this() Method

`this()` calls **another constructor of the same class**.

```java
class Student {
    String name;
    int age;

    Student() {
        this("Unknown", 0);   // calls Student(String, int)
        System.out.println("Default Student created");
    }

    Student(String name, int age) {
        this.name = name;
        this.age = age;
        System.out.println("Student: " + name + ", " + age);
    }
}
```

### ⚔️ this() vs super() — Comparison

| Feature | `this()` | `super()` |
|---------|----------|-----------|
| Calls | Same class constructor | Parent class constructor |
| Must be | First statement in constructor | First statement in constructor |
| Can use in static? | ❌ No | ❌ No |
| How many times in constructor | Only **once** | Only **once** |
| Can use elsewhere? | Yes (anywhere except static) | Yes (anywhere except static) |
| Both are | Non-static keywords | Non-static keywords |

### 💻 Full Inheritance Chain Example
```java
class Object {
    // root class — every class extends this
}

class Animal {
    Animal() {
        // super() called here → calls Object constructor
        System.out.println("Animal created");
    }
}

class Dog extends Animal {
    Dog() {
        // super() called here → calls Animal constructor
        System.out.println("Dog created");
    }
}

class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        // Output:
        // Animal created
        // Dog created
    }
}
```

### ⚠️ Important Rules
```
✅ super() must be the FIRST statement in a constructor
✅ this() must be the FIRST statement in a constructor
❌ You CANNOT use both super() and this() in the same constructor
    (since only one can be the first statement)
❌ Neither this() nor super() can be used in static methods/blocks
```

---

## 7. Quick Revision Cheatsheet

```
ENCAPSULATION
├── Bind data + methods inside class for security
├── Use private variables + public methods
└── Achieved via access specifiers (private, public, protected, default)

GETTERS & SETTERS
├── getter: public ReturnType getVarName() { return varName; }
├── setter: public void setVarName(Type varName) { this.varName = varName; }
└── Naming: first letter of variable capitalized

this KEYWORD
├── Refers to current object
├── Resolves name conflict (instance vs local variable)
├── this() → calls same class constructor (must be 1st statement)
└── Cannot be used in static context

CONSTRUCTORS
├── Same name as class, no return type
├── Called automatically once at object creation
├── Default: no params, auto-created by Java if none defined
├── Parameterized: takes params, gives custom values
└── If you define parameterized → Java stops auto-creating default

super() vs this()
├── super() → parent class constructor
├── this() → same class constructor
├── Both must be FIRST statement in constructor
├── Both non-static, cannot use in static context
└── Only ONE can appear in a constructor

OBJECT CLASS
└── Every class extends Object implicitly
    Object → methods: toString(), equals(), hashCode(), getClass()
```

---

## 8. Interview Questions & Answers

### Q1. What is encapsulation in Java?
**A:** Encapsulation is the process of binding data (variables) and methods together inside a class and restricting direct access to the data using access specifiers (typically `private`). It improves security and maintainability.

### Q2. How do you achieve encapsulation in Java?
**A:** By declaring variables as `private` and providing `public` getter and setter methods to access and modify them.

### Q3. What is the difference between instance and local variables?
**A:**
| Instance Variable | Local Variable |
|------------------|---------------|
| Declared in class, outside method | Declared inside method |
| Has default value | No default value |
| Lives as long as object lives | Lives only during method execution |
| Stored in Heap | Stored in Stack |

### Q4. What is the `this` keyword in Java?
**A:** `this` refers to the **current object** (the object invoking the method). It is used to resolve name conflicts between instance and local variables, pass the current object as an argument, and call other constructors of the same class using `this()`.

### Q5. What is a constructor in Java?
**A:** A constructor is a special method with the same name as the class and no return type. It is called automatically when an object is created and is used to initialize the object's state.

### Q6. What is the difference between a constructor and a method?
**A:**
| Constructor | Method |
|-------------|--------|
| Same name as class | Any name |
| No return type | Must have return type (even void) |
| Called automatically on object creation | Called explicitly |
| Called only once per object | Can be called multiple times |

### Q7. What is a default constructor?
**A:** A constructor with no parameters. If you don't define any constructor, Java automatically provides a blank default constructor. It assigns default values (0, null, false) to instance variables.

### Q8. What happens if you define only a parameterized constructor?
**A:** Java will **not** auto-generate a default constructor. Calling `new ClassName()` without arguments will cause a **compilation error**.

### Q9. What is `super()` in Java?
**A:** `super()` calls the constructor of the parent (super) class. It must be the **first statement** in a constructor. Java adds `super()` automatically as the first statement of every constructor if you don't explicitly write it.

### Q10. What is the difference between `this()` and `super()`?
**A:** `this()` calls a constructor of the **same class**, while `super()` calls a constructor of the **parent class**. Both must be the first statement in a constructor, so they **cannot be used together** in the same constructor.

### Q11. What is the Object class in Java?
**A:** `Object` is the **root class** of all Java classes. Every class implicitly extends `Object`. It provides common methods like `toString()`, `equals()`, `hashCode()`, and `getClass()`.

### Q12. Can we use `this` or `super` in a static method?
**A:** **No.** Both `this` and `super` are non-static keywords that refer to object instances. Static methods belong to the class (not an object), so using `this` or `super` inside static methods causes a compilation error.

### Q13. What are the benefits of using getters and setters?
**A:** They provide controlled access to private data, allow input validation inside setters, enable logging/tracking of data changes, and maintain encapsulation without exposing internal implementation.

### Q14. What is constructor overloading?
**A:** Having multiple constructors in the same class with different parameter lists. Java decides which constructor to call based on the arguments passed at object creation.

---

*📝 Notes compiled from lecture transcripts | Java OOPs Interview Preparation — Part 3*
