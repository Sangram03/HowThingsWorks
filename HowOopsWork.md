# 🧠 **What is OOP? (Very Simple)**

OOP = Organizing your code like **real-world objects**.

Example:
A **Car** has:

* Properties → color, model, speed
* Behaviors → start(), stop()

So in OOP we create:

* **Class** = blueprint (Car design)
* **Object** = real item created from class (BMW car, Tesla car)

---

# 🧩 **4 Pillars of OOP**

![Image](https://miro.medium.com/0%2AlBYKi1x-16ueEVzk?utm_source=chatgpt.com)

![Image](https://miro.medium.com/1%2AGDZKZyaSfQGm8HL-CtYWtA.jpeg?utm_source=chatgpt.com)

OOP works using these **4 concepts**:

1. **Encapsulation**
2. **Inheritance**
3. **Polymorphism**
4. **Abstraction**

Let’s understand each one in very easy words.

---

# 1️⃣ **Encapsulation (Data + Methods packed together)**

**Wrapping data and methods inside a class.**

Example (Java):

```java
class Student {
    private int age;  // hidden data

    public void setAge(int a) {
        age = a;
    }

    public int getAge() {
        return age;
    }
}
```

👉 `private` hides data
👉 `setAge()` and `getAge()` control access
👉 This is **encapsulation**

**Real life example:**
ATM hides your account balance, allows access with PIN (methods).

---

# 2️⃣ **Inheritance (Reusing classes)**

One class (child) takes features of another (parent).

Example:

```java
class Animal {
    void eat() { System.out.println("eating"); }
}

class Dog extends Animal {
    void bark() { System.out.println("barking"); }
}
```

`Dog` gets:

* dog.bark()
* dog.eat() → from parent

**Real life:**
Father’s properties → Son
Company employee → Manager (child class with extra features)

---

# 3️⃣ **Polymorphism (Same action, different behavior)**

### Two types:

### **A. Compile-time (Method Overloading)**

Same function name, different parameters.

```java
void show(int a) {}
void show(String a) {}
```

### **B. Runtime (Method Overriding)**

Child class changes parent class method.

```java
class Animal {
    void sound() { System.out.println("Animal sound"); }
}

class Dog extends Animal {
    void sound() { System.out.println("Dog barks"); }
}
```

---

# 4️⃣ **Abstraction (Hiding internal details)**

Show only essentials, hide complexity.

Example:

```java
abstract class Car {
    abstract void start();
}
```

When using a car:

* You press start
* You don’t see engine logic inside → hidden

**Real life example:**
Using mobile
→ You dial a number
→ You don’t know internal circuit
→ That is **abstraction**

---

# 🛠 **How OOP Works Together (Flow)**

![Image](https://creately.com/static/assets/guides/class-diagram-relationships/uml-class-diagram-relationships.webp?utm_source=chatgpt.com)

![Image](https://www.conceptdraw.com/How-To-Guide/picture/IDEF-Business-Process-Diagrams-Final-Object-Schematic.png?utm_source=chatgpt.com)

1. You create a **class** (blueprint).
2. You create **objects** from that class.
3. You apply OOP concepts for structure:

   * Encapsulation → hide data
   * Inheritance → reuse
   * Polymorphism → flexibility
   * Abstraction → hide complexity

---

# 📦 **Example in Java (Complete OOP)**

```java
abstract class Car {               // abstraction
    private String color;          // encapsulation

    public void setColor(String c) {
        color = c;
    }

    public String getColor() {
        return color;
    }

    abstract void start();
}

class Tesla extends Car {          // inheritance
    void start() {                 // polymorphism (override)
        System.out.println("Tesla starts silently");
    }
}

public class Main {
    public static void main(String[] args) {
        Tesla t = new Tesla();     // object
        t.setColor("Black");
        t.start();
        System.out.println(t.getColor());
    }
}
```

---

# 🎯 Summary (Super Easy)

| OOP Concept       | Meaning                         | Real Life Example       |
| ----------------- | ------------------------------- | ----------------------- |
| **Class**         | Blueprint                       | Car design              |
| **Object**        | Real instance                   | Real car                |
| **Encapsulation** | Data hiding                     | ATM PIN                 |
| **Inheritance**   | Reuse                           | Father → Son            |
| **Polymorphism**  | Same function, different result | Brake: Bike vs Car      |
| **Abstraction**   | Hide complexity                 | Phone calling interface |

---
