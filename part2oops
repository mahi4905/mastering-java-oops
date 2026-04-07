# ☕ Java OOPs — Complete Interview Notes (Part 2)

> **Topics Covered:** Jagged Arrays, Array Drawbacks, Array of Objects, Enhanced For Loop, StringBuffer & StringBuilder, Static Keyword (Variables, Blocks, Methods)

---

## 📌 Table of Contents
1. [Jagged Arrays](#1-jagged-arrays)
2. [Drawbacks of Arrays](#2-drawbacks-of-arrays)
3. [Array of Objects](#3-array-of-objects)
4. [Enhanced For Loop](#4-enhanced-for-loop)
5. [StringBuffer & StringBuilder](#5-stringbuffer--stringbuilder)
6. [Static Keyword — Variables](#6-static-keyword--variables)
7. [Static Keyword — Blocks & Methods](#7-static-keyword--blocks--methods)
8. [Quick Revision Cheatsheet](#8-quick-revision-cheatsheet)
9. [Interview Questions & Answers](#9-interview-questions--answers)

---

## 1. Jagged Arrays

### 🔑 What is a Jagged Array?
A **jagged array** is a multidimensional array where **each row can have a different number of columns** (unlike a regular 2D array where all rows have the same size).

> Jagged array concept was introduced in **Java 8**.

### 🖼️ Visual Representation
```
Row 0: | 1 | 2 | 3 |              → 3 elements
Row 1: | 4 | 5 | 6 | 7 | 8 |     → 5 elements
Row 2: | 1 | 5 | 9 | 2 | 4 | 7 | → 6 elements
```

### 📝 Syntax — 2D Jagged Array
```java
// Step 1: Declare rows, leave columns undefined
int nums[][] = new int[3][];

// Step 2: Assign different column sizes per row
nums[0] = new int[3];
nums[1] = new int[5];
nums[2] = new int[6];
```

### 💻 Initialize with Random Values
```java
for (int i = 0; i < nums.length; i++) {
    for (int j = 0; j < nums[i].length; j++) {
        nums[i][j] = (int)(Math.random() * 10);  // random 0-9
    }
}
```

### 🔍 Traversal — Regular For Loop
```java
for (int i = 0; i < nums.length; i++) {
    for (int j = 0; j < nums[i].length; j++) {
        System.out.print(nums[i][j] + " ");
    }
    System.out.println(); // new line after each row
}
```

### 🔍 Traversal — Enhanced For Loop
```java
for (int[] x : nums) {
    for (int y : x) {
        System.out.print(y + " ");
    }
    System.out.println();
}
```

### 🧊 3D Jagged Array (For Curiosity)
```java
int num[][][] = new int[3][][];
num[0] = new int[2][];
num[1] = new int[3][];
num[2] = new int[4][];

num[0][0] = new int[2];
num[0][1] = new int[3];
num[1][0] = new int[4];
num[1][1] = new int[5];
num[1][2] = new int[6];
num[2][0] = new int[7];
num[2][1] = new int[8];
num[2][2] = new int[9];
num[2][3] = new int[10];

// Initialize
for (int i = 0; i < num.length; i++)
    for (int j = 0; j < num[i].length; j++)
        for (int k = 0; k < num[i][j].length; k++)
            num[i][j][k] = (int)(Math.random() * 10);

// Traverse
for (int i = 0; i < num.length; i++)
    for (int j = 0; j < num[i].length; j++)
        for (int k = 0; k < num[i][j].length; k++)
            System.out.print(num[i][j][k] + " ");
```

> 💡 **Key Point:** Always use `nums[i].length` (not a fixed column size) when traversing jagged arrays.

---

## 2. Drawbacks of Arrays

### ⚠️ Limitations of Arrays in Java

| # | Drawback | Explanation |
|---|----------|-------------|
| 1 | **Contiguous memory required** | Array needs a continuous block of memory in heap |
| 2 | **Fixed size** | Once created, array size cannot be increased |
| 3 | **Poor insertion/search performance** | Slower compared to HashSet, LinkedList, etc. |
| 4 | **Homogeneous data only** | Only one data type allowed (e.g. int array can't store String) |
| 5 | **No built-in methods** | Arrays lack powerful built-in utility methods |

### 💡 Solution → Collections Framework
Java's **Collections** (ArrayList, LinkedList, HashSet, etc.) solve all these problems:
- Dynamic sizing
- Heterogeneous data (with generics)
- Better performance for insertion/search
- Rich set of utility methods

```java
// Array — fixed size, one type
int[] arr = new int[5];

// ArrayList — dynamic, flexible
ArrayList<Integer> list = new ArrayList<>();
list.add(10);
list.add(20);  // grows automatically!
```

> 📌 **Remember:** Collections will be covered in upcoming lectures.

---

## 3. Array of Objects

### 🔑 What is an Array of Objects?
Just like we create arrays of `int`, `float`, `char` — we can create an **array of object references**.

An array of objects holds **references** to objects, not the objects themselves.

### 🧠 Understanding References First
```java
class Student { }

Student st = new Student();
// st → reference variable (stored in Stack)
// new Student() → actual object (stored in Heap)
// st holds the address/reference of the object
```

### 📝 Creating Array of Objects
```java
// Creates array that can hold 5 Student references
// Default value = null (reference type default)
Student[] sts = new Student[5];

// Now create actual objects and assign
sts[0] = new Student();
sts[1] = new Student();
sts[2] = new Student();
sts[3] = new Student();
sts[4] = new Student();
```

### 🗺️ Memory Diagram
```
Stack                    Heap
┌─────────┐             ┌──────────────────────────────┐
│  sts ───┼────────────►│ [ref0][ref1][ref2][ref3][ref4]│ ← array object
└─────────┘             └──┬───┬───┬───┬───┬───────────┘
                           │   │   │   │   │
                           ▼   ▼   ▼   ▼   ▼
                          S0  S1  S2  S3  S4  ← Student objects
```

### 💻 Full Example with Properties
```java
class Student {
    String name;
    int marks;
}

class Main {
    public static void main(String[] args) {
        Student[] sts = new Student[3];

        sts[0] = new Student();
        sts[0].name = "Arjun";
        sts[0].marks = 90;

        sts[1] = new Student();
        sts[1].name = "Priya";
        sts[1].marks = 85;

        // Traverse
        for (Student s : sts) {
            if (s != null)  // check for null before accessing
                System.out.println(s.name + ": " + s.marks);
        }
    }
}
```

> ⚠️ **ArrayIndexOutOfBoundsException** is thrown when you access an index outside the array bounds. Always use `array.length` to stay safe.

> 💡 **Default value** for object arrays is `null` (not 0), since they are reference types.

---

## 4. Enhanced For Loop

### 🔑 What is Enhanced For Loop?
Introduced in **Java 5**, the enhanced for loop (also called **for-each loop**) is used to **iterate over arrays and collections** without needing an index.

### ✅ Why Use It?
| Regular For Loop | Enhanced For Loop |
|-----------------|------------------|
| Needs index variable | No index needed |
| Needs condition check | No condition needed |
| Needs increment | No increment needed |
| Can modify elements | Read-only (cannot modify) |
| Can iterate partially | Always full traversal |

### 📝 Syntax
```java
for (dataType variable : arrayOrCollection) {
    // use variable
}
```

### 💻 Example — Array
```java
int[] nums = new int[]{10, 20, 30, 40};

// Regular for loop
for (int i = 0; i < nums.length; i++) {
    System.out.println(nums[i]);
}

// Enhanced for loop — cleaner!
for (int n : nums) {
    System.out.println(n);
}
```

### 💻 Example — Collection (For Curiosity)
```java
ArrayList al = new ArrayList();
al.add(10);
al.add(20);
al.add(30);

for (Object o : al) {
    System.out.println(o);
}
```

> 📌 Collections will be discussed in upcoming lectures.

> ⚠️ **Limitation:** Enhanced for loop cannot be used when you need the **index** of elements or want to **modify** elements during iteration.

---

## 5. StringBuffer & StringBuilder

### 🔑 Why StringBuffer / StringBuilder?
Regular `String` in Java is **immutable** (cannot be changed once created). Every modification creates a new String object.

`StringBuffer` and `StringBuilder` create **mutable strings** — they can be modified without creating new objects.

### 📝 Creating a StringBuffer Object
```java
StringBuffer sb = new StringBuffer("Hello");
```

### 🛠️ Important Methods

#### `capacity()` — Default is 16 + length of string
```java
StringBuffer sb = new StringBuffer("Hello");
System.out.println(sb.capacity());  // 16 + 5 = 21
```

#### `length()` — Number of characters
```java
System.out.println(sb.length());  // 5
```

#### `append()` — Add content at end
```java
sb.append(" World");
System.out.println(sb);  // Hello World
```

#### `insert()` — Insert at specific index
```java
sb.insert(0, "Hi ");
System.out.println(sb);  // Hi Hello World
```

#### `deleteCharAt()` — Delete character at index
```java
sb.deleteCharAt(3);  // removes character at index 3
```

#### `toString()` — Convert to String
```java
String str = sb.toString();
System.out.println(str);
```

### 💻 Complete Example
```java
StringBuffer sb = new StringBuffer("Hello");

System.out.println(sb.capacity());    // 21 (16 + 5)
System.out.println(sb.length());      // 5

sb.append(" World");
System.out.println(sb);               // Hello World

sb.insert(0, "Say: ");
System.out.println(sb);               // Say: Hello World

sb.deleteCharAt(0);
System.out.println(sb);               // ay: Hello World

String str = sb.toString();
System.out.println(str);              // ay: Hello World
```

### ⚔️ StringBuffer vs StringBuilder

| Feature | StringBuffer | StringBuilder |
|---------|-------------|---------------|
| **Thread Safety** | ✅ Thread-safe (synchronized) | ❌ Not thread-safe |
| **Performance** | Slower (due to synchronization) | Faster |
| **Use Case** | Multi-threaded environments | Single-threaded environments |
| **Introduced** | Java 1.0 | Java 5 |

> 📌 **Thread safety** will be discussed in detail in the Multithreading lecture.

### 📋 Other Methods to Explore
- `reverse()` — reverses the string
- `replace(start, end, str)` — replaces substring
- `delete(start, end)` — deletes substring
- `charAt(index)` — returns character at index
- `indexOf(str)` — returns index of first occurrence

---

## 6. Static Keyword — Variables

### 🔑 What is the `static` Keyword?
When `static` is used with a variable, block, or method, it becomes **independent of any object**. It belongs to the **class itself**, not to any instance.

### 4 Places to Use `static`
| Place | Example |
|-------|---------|
| Variable | `static int count = 0;` |
| Block | `static { System.out.println("loaded"); }` |
| Method | `public static void main(String[] args) {}` |
| Inner Class | `static class InnerClass {}` |

### 🧠 When Does Memory Get Allocated?

```
Compile → .class file
         ↓
Execute (java MainClass)
         ↓
Class Loader loads .class file
         ↓
Static variables initialized  ← HERE (before object creation!)
Static blocks executed        ← HERE
         ↓
main() method runs
         ↓
Objects created (new keyword)
```

> 💡 Static variables get memory in **heap** during **class loading**, before any object is created.

### ⚔️ Static Variable vs Instance Variable

```java
class Calc {
    static int stA = 100;  // static — shared by ALL objects
    int inB = 100;         // instance — separate copy per object

    public static void main(String[] args) {
        Calc obj1 = new Calc();
        Calc obj2 = new Calc();

        // Accessing static variable
        System.out.println(Calc.stA);   // via class name ✅
        System.out.println(obj1.stA);   // via object ✅

        // Accessing instance variable
        // System.out.println(Calc.inB); // ❌ ERROR!
        System.out.println(obj1.inB);   // via object only ✅

        // Changing values
        obj1.stA = 2000;  // changes for ALL objects!
        obj1.inB = 1000;  // changes only for obj1

        System.out.println(obj1.stA);   // 2000
        System.out.println(obj2.stA);   // 2000 ← also changed!

        System.out.println(obj1.inB);   // 1000
        System.out.println(obj2.inB);   // 100 ← unchanged
    }
}
```

### 📋 Static vs Instance — Summary Table

| Feature | Static Variable | Instance Variable |
|---------|----------------|------------------|
| Belongs to | Class | Object |
| Memory | Allocated at class loading | Allocated at object creation |
| Shared | Yes, all objects share one copy | No, each object has its own |
| Access | `ClassName.var` or `obj.var` | `obj.var` only |
| Default value | Yes (0, false, null) | Yes (0, false, null) |

### ⚠️ Golden Rules
```
✅ Static method/block CAN access static variables directly
❌ Static method/block CANNOT access instance variables without an object
✅ Non-static method CAN access both static and instance variables
```

---

## 7. Static Keyword — Blocks & Methods

### 🔑 Static Block vs Non-Static Block

| | Static Block | Non-Static Block |
|--|-------------|-----------------|
| **Syntax** | `static { }` | `{ }` (just curly braces) |
| **When executed** | During class loading (before `main`) | Every time an object is created |
| **Runs before** | `main()` method | Constructor |
| **Purpose** | One-time static initialization | Instance initialization |

### 💻 Execution Order Example
```java
class Calc {
    static {
        System.out.println("1. Static Block");
        System.out.println("2. Executed before main");
    }

    {
        // non-static block
        System.out.println("4. Non-static block — before constructor");
    }

    public static void main(String[] args) {
        System.out.println("3. main() method starts");
        Calc c = new Calc();       // triggers non-static block
        Help.wish();               // triggers Help's static block
    }
}

class Help {
    static {
        System.out.println("5. Static block of Help class");
    }

    static void wish() {
        System.out.println("6. Hello from Help!");
    }
}
```

### 📤 Output
```
1. Static Block
2. Executed before main
3. main() method starts
4. Non-static block — before constructor
5. Static block of Help class
6. Hello from Help!
```

> 💡 The static block of `Help` class runs when `Help` is first **used** (not just declared).
> ```java
> Help h;           // ❌ static block NOT triggered (just declaration)
> Help h = new Help(); // ✅ static block triggered
> Help.wish();      // ✅ static block triggered (class is accessed)
> ```

### 🔑 Static Method vs Non-Static Method

```java
class Demo {
    static void staticMethod() {
        System.out.println("Static method");
    }

    void nonStaticMethod() {
        System.out.println("Non-static method");
    }

    public static void main(String[] args) {
        // Static method — call via class name OR object
        Demo.staticMethod();       // ✅ via class name
        Demo obj = new Demo();
        obj.staticMethod();        // ✅ via object (not recommended)

        // Non-static method — ONLY via object
        obj.nonStaticMethod();     // ✅
        // Demo.nonStaticMethod(); // ❌ ERROR
    }
}
```

### ⚠️ Critical Rules — Static vs Non-Static Access

```java
class Example {
    static int staticVar = 10;
    int instanceVar = 20;

    static void staticMethod() {
        System.out.println(staticVar);      // ✅ OK
        // System.out.println(instanceVar); // ❌ ERROR — needs object
        Example e = new Example();
        System.out.println(e.instanceVar);  // ✅ OK with object
    }

    void nonStaticMethod() {
        System.out.println(staticVar);      // ✅ OK
        System.out.println(instanceVar);    // ✅ OK
    }
}
```

> 📌 **Remember:**
> - Static context → can use static members directly, needs object for instance members
> - Non-static context → can use both freely

---

## 8. Quick Revision Cheatsheet

```
JAGGED ARRAY
├── Array of arrays with different column sizes
├── int[][] arr = new int[3][];  then assign each row separately
└── Use arr[i].length (not fixed column size) for traversal

ARRAY DRAWBACKS
├── Fixed size, contiguous memory, homogeneous only
└── Solution → Collections Framework

ARRAY OF OBJECTS
├── Holds references, not actual objects
├── Default value = null
└── Must create each object individually with 'new'

ENHANCED FOR LOOP
├── Introduced in Java 5
├── for(type var : array) { }
└── No index, no condition, no increment — read-only

STRING BUFFER vs STRING BUILDER
├── Both create mutable strings
├── StringBuffer = thread-safe (slower)
└── StringBuilder = not thread-safe (faster)

STATIC KEYWORD
├── Independent of object, belongs to class
├── Memory allocated at class loading (before objects)
├── Static block → runs before main()
├── Non-static block → runs before constructor (on object creation)
└── Static method → call via ClassName.method() or object
```

---

## 9. Interview Questions & Answers

### Q1. What is a Jagged Array?
**A:** A jagged array is a multidimensional array where each row (member array) can have a **different number of columns**. It is an array of arrays with varying sizes. Example:
```java
int[][] arr = new int[3][];
arr[0] = new int[2];
arr[1] = new int[4];
arr[2] = new int[3];
```

### Q2. What are the drawbacks of arrays in Java?
**A:** Key drawbacks are: fixed size (cannot grow/shrink), requires contiguous memory, allows only homogeneous data types, poor insertion/deletion performance, and no built-in utility methods. The Collections Framework solves these problems.

### Q3. What is the default value for an array of objects?
**A:** `null`. When you create an array of reference types (objects), each element is initialized to `null` by default since no objects have been created yet.

### Q4. What is the difference between `for` loop and enhanced `for` loop?
**A:**
| | Regular For | Enhanced For |
|--|-------------|-------------|
| Index needed | Yes | No |
| Can modify elements | Yes | No |
| Partial traversal | Yes | No (always full) |
| Works with | Arrays | Arrays + Collections |

### Q5. What is the difference between String, StringBuffer, and StringBuilder?
**A:**
| | String | StringBuffer | StringBuilder |
|--|--------|-------------|---------------|
| Mutability | Immutable | Mutable | Mutable |
| Thread-safe | Yes | Yes | No |
| Performance | Slow (new object each time) | Medium | Fast |

### Q6. What is the default capacity of StringBuffer?
**A:** The default capacity is **16**. If you initialize it with a string, the capacity becomes `16 + length of string`.

### Q7. What does the `static` keyword mean in Java?
**A:** `static` makes a member (variable, method, block) **independent of any object** — it belongs to the class itself. Static members are shared across all instances and are initialized during class loading, before any object is created.

### Q8. When is a static block executed?
**A:** A static block is executed **during class loading**, which happens before the `main()` method runs. It runs only **once** per class load.

### Q9. When is a non-static block executed?
**A:** A non-static (instance initializer) block is executed **every time an object is created**, just **before the constructor** runs.

### Q10. Can we access instance variables inside a static method?
**A:** **Not directly.** Since static methods belong to the class (not an object), they can't access instance variables without creating an object first. You must create an object and use it to access instance variables.

### Q11. What is the order of execution in Java?
**A:**
```
Static block → main() → Non-static block → Constructor → Method body
```

### Q12. What is the difference between static and instance variables?
**A:**
| Static Variable | Instance Variable |
|----------------|-----------------|
| One shared copy for all objects | Each object has its own copy |
| Accessed via class name or object | Accessed only via object |
| Memory in heap at class loading | Memory in heap at object creation |
| Changing it affects all objects | Changing it affects only that object |

### Q13. Why is StringBuilder faster than StringBuffer?
**A:** StringBuffer methods are **synchronized** (thread-safe), which adds overhead. StringBuilder methods are **not synchronized**, making it faster in single-threaded environments where thread safety isn't needed.

### Q14. What happens when you access a static block of another class?
**A:** The static block of a class runs the **first time that class is used** — whether by creating an object or calling a static method. Simply declaring a reference variable (without `new`) does **not** trigger the static block.

---

*📝 Notes compiled from lecture transcripts | Java OOPs Interview Preparation — Part 2*
