# 📘 OOP in Java – Day 1 Notes

---

## 🔹 1. Class & Object

### 📌 Definition
- Java is an Object-Oriented Programming language
- Object = Properties + Behavior
- Class = Blueprint of object

### 🧾 Pseudocode
```
DEFINE class Car
    VARIABLE color
    FUNCTION drive()
        PRINT "Car is moving"
END CLASS
```

### 💻 Java Code
```java
class Car {
    String color;

    void drive() {
        System.out.println("Car is moving");
    }
}
```

---

## 🔹 2. Methods

### 📌 Definition
A method is a collection of statements that performs a task.

### 🧾 Pseudocode
```
FUNCTION add(a, b)
    RETURN a + b
END FUNCTION
```

### 💻 Java Code
```java
int add(int a, int b) {
    return a + b;
}
```

---

## 🔹 3. Method Overloading

- Same method name, different parameters

### 💻 Java Code
```java
int add(int a, int b) {
    return a + b;
}

int add(int a, int b, int c) {
    return a + b + c;
}
```

---

## 🔹 4. JDK, JRE, JVM

- JDK = JRE + JVM
- JVM executes code

---

## 🔹 5. Stack vs Heap

- Stack → local variables
- Heap → objects

---

## 🔹 6. Arrays

- Collection of similar data
- Stored in continuous memory

---

# ⚡ Quick Revision

- Class = Blueprint  
- Object = Instance  
- Heap = Objects  
- Stack = Local variables  
