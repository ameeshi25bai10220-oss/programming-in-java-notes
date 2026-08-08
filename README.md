# Programming in Java; Exam Study Guide
### Based on *Java: The Complete Reference, 7th Edition* (Herbert Schildt) —explained and expanded with extra examples for exam prep

> This guide covers my teacher's 7 marked topics in full depth, PLUS the rest of your syllabus (Module 1 and Module 2) so nothing is missed. Every topic has: **theory → definitions → logic → code examples**.

---

## How this guide is organized

- **PART A** — the teacher's marked topics (1, 2, 3, 4, 5, 6, 8) — deep detail
- **PART B** — Remaining Module 1 items (JVM/JRE/JDK, I/O) — folded into Part A where they belong
- **PART C** — Module 2: full Object-Oriented Programming syllabus (Classes, Constructors, Strings, Access Modifiers, this/final, Recursion, instanceof, Nested/Inner/Anonymous classes, enums, Inheritance, Overriding, super, Abstract classes, Interfaces, Polymorphism, Encapsulation, Static/Singleton classes, Reflection)

---

# PART A — TEACHER'S MARKED TOPICS

# TOPIC 1: The History and Evolution of Java

## Why history matters for exams
Exam questions here usually ask you to: (a) list Java's lineage, (b) explain why Java was created, (c) list and explain the **Java buzzwords/features**, and (d) explain **bytecode** and **portability**. This is a theory-only topic — no code — so focus on definitions you can reproduce precisely.

## 1.1 Java's Lineage (C → C++ → Java)

Java did not appear out of nowhere. It is a direct descendant of a lineage of languages:

- **C (early 1970s, Dennis Ritchie)**: The first truly modern, structured, high-level system-programming language. Before C, programmers had to choose between languages that were *powerful but hard to use* (like assembly) or *easy but weak* (like BASIC). C gave programmers the structure, speed, and control needed to write operating systems (it was used to write UNIX) while still being portable across machines.
- **C++ (early 1980s, Bjarne Stroustrup)**: Built as an enhancement to C, adding **object-oriented programming (OOP)**. C++ is technically a *superset* of C — nearly all valid C code is valid C++ code — with classes, objects, inheritance, and other OOP features layered on top.
- **Java (1991–1995, James Gosling and team at Sun Microsystems)**: Originally called "Oak," created for embedded consumer electronics (like set-top boxes), where portability across many different CPUs was critical, since manufacturers used a variety of processors. The project was renamed **Java** in 1995. When the World Wide Web took off at the same time, Sun realized Java's "write once, run anywhere" design was perfect for the Internet, and retargeted it toward web/Internet programming.

**Key definition (exam-safe):**
> Java derives its **syntax** from C, and many of its **object-oriented features** were influenced by C++. It was designed to fix specific weaknesses in C++ for distributed, network-based, and portable environments.

### Why not just use C++ for the Internet?
C++ has several features that make it unsuitable for a *portable, secure, distributed* environment:
1. **No garbage collection** — C++ requires manual memory management (`new`/`delete`), which causes memory leaks and crashes if done wrong.
2. **Multiple inheritance** — makes C++ programs complex and its runtime model heavy.
3. **Pointers** — direct memory-address manipulation in C++ is a major security hole; it lets a program access arbitrary memory.
4. **Platform dependence** — C++ programs are compiled to native machine code for one specific CPU/OS combination, so a compiled program can't just be sent across the Internet and run anywhere.

Java's designers deliberately removed or changed each of these.

## 1.2 The C# Connection (short, often asked)
Years later, Microsoft created **C#** for the .NET framework. C# is closely related to Java — same general "curly-brace," object-oriented, garbage-collected style — but was designed independently to work tightly with the Windows/.NET ecosystem. Examiners sometimes ask you to note that C# was influenced by Java in the same way Java was influenced by C++.

## 1.3 How Java changed the Internet — Applets, Security, Portability

- **Java Applets**: small Java programs that could be embedded in a web page and would run inside the browser. This was Java's original "killer app" — dynamic, executable content on static web pages. (Applets are now obsolete/deprecated in modern Java, but the *concept* is exam-relevant history.)
- **Security**: Because an applet from an unknown website runs on your machine, it must be untrusted by default. Java achieves this using the **sandbox** model — applets run inside a restricted execution environment that cannot touch the local file system or other resources without explicit permission.
- **Portability**: The same compiled program must run correctly across different processors and operating systems (Windows, Linux, Mac, embedded chips) — no recompilation needed.

## 1.4 Java's Magic — Bytecode

This is one of the most commonly asked *definition* questions.

> **Bytecode** is a highly optimized, intermediate set of instructions produced when a Java compiler (`javac`) compiles Java source code. It is *not* native machine code for any specific CPU. Instead, bytecode is executed by the **Java Virtual Machine (JVM)**, which translates it (via interpretation or JIT compilation) into native instructions for whatever machine it's running on.

**Why this matters:** Because bytecode is CPU-independent, a `.class` file compiled once can run on *any* device that has a JVM — this is the basis of Java's famous slogan:

> **"Write Once, Run Anywhere" (WORA)**

Flow to memorize for diagrams:
```
Java source code (.java)
        │  compiled by javac
        ▼
   Bytecode (.class)
        │  executed by JVM (interpreter / JIT compiler)
        ▼
 Native machine code (runs on any OS/CPU with a JVM)
```

The JVM also enables **Just-In-Time (JIT) compilation**: frequently executed bytecode is compiled to native machine code at run time for speed, combining bytecode's portability with near-native performance.

## 1.5 Servlets — Java on the server side
Just as an applet runs on the client (browser), a **servlet** is a small Java program that runs on the **server** and dynamically extends the functionality of a web server (e.g., generating dynamic web page content, processing form data). This was Java's answer to needing portable, secure server-side code.

## 1.6 The Java Buzzwords (VERY frequently asked — memorize all of these with one-line meanings)

| Buzzword | Meaning |
|---|---|
| **Simple** | Small, familiar syntax (close to C/C++) with confusing features (pointers, multiple inheritance, operator overloading) removed. |
| **Object-Oriented** | Follows the modern, streamlined OOP model based on objects and classes; has a rich set of pre-built classes. |
| **Robust** | Encourages error-free programming: strong compile-time and run-time checking, exception handling, no explicit pointers, automatic garbage collection. |
| **Multithreaded** | Built-in support for multiple threads of execution (multiple tasks running "simultaneously") to handle interactive, networked programs. |
| **Architecture-Neutral** | Compiler generates bytecode, an architecture-neutral intermediate format that runs on any processor with a Java runtime. |
| **Interpreted and High Performance** | Bytecode can be interpreted on any machine; the JIT compiler translates bytecode to native code on the fly for high performance. |
| **Distributed** | Designed for the distributed environment of the Internet; handles TCP/IP protocols, can access remote resources as easily as local ones. |
| **Dynamic** | Programs can carry substantial run-time type information used to verify/resolve access to objects at run time; linking is done dynamically as new classes are loaded. |
| **Secure** | Bytecode is verified before execution; no direct pointer manipulation; sandboxed execution for untrusted code. |
| **Portable** | Because it is architecture-neutral, there are no implementation-dependent aspects of the specification (e.g., `int` is always 32-bit in Java, unlike C). |

**One-liner to remember them all:** *"Java is a Simple, Object-Oriented, Robust, Multithreaded, Architecture-neutral, Interpreted, Distributed, Dynamic, Secure, Portable, High-performance language."*

## 1.7 The Evolution of Java (brief timeline — know the trend, not every exact date)
- **Oak (1991)** → renamed **Java (1995)**
- **Java 1.0 / 1.1** — early releases, AWT, inner classes
- **Java 2 (J2SE 1.2 onward)** — introduced Swing, Collections Framework
- **J2SE 5 (Java 5)** — major update: **generics**, **enhanced for-loop (for-each)**, **autoboxing/unboxing**, **enumerations (enum)**, **varargs**, **annotations**
- **Java SE 6** — performance and library improvements
- (Later versions beyond the book add lambdas, streams, modules, records, etc. — good to mention if your course goes beyond the textbook, but not covered by this book.)

**Exam tip:** If asked "what changed in Java 5," the answer set is: **generics, for-each loop, autoboxing/unboxing, enum, varargs, static import, annotations**.

---

# TOPIC 2: An Overview of Java

This topic bridges pure theory (OOP paradigms) with your first real code (Hello World). It maps directly to Module 1's "Java Hello World, JVM, JRE, JDK" items.

## 2.1 Two Programming Paradigms

- **Process-oriented (procedural) model**: Older style (e.g., plain C). Thinks of a program as *"code acting on data."* The program itself is a series of linear steps — first do this, then do that. As programs grow large, this model becomes hard to manage because there's no strong link between the data and the functions that operate on it.
- **Object-oriented model**: Thinks of a program as *"data controlling access to code."* You define **objects** — self-contained units combining data (state) and the functions that operate on that data (behavior) — and the program is a set of objects interacting with each other.

## 2.2 Abstraction
> **Abstraction** means managing complexity by exposing only the essential features of an object while hiding the background implementation details.

Classic analogy (use this in exams): A car's *accelerator pedal* is an abstraction — you press it to go faster, without knowing the internal combustion/fuel-injection details happening underneath. In Java, a **class** is exactly this kind of abstraction: it defines a new data type, and users of that class interact with it through its public interface without needing to know its internal implementation.

## 2.3 The Three OOP Principles (extremely important — always asked)

All object-oriented languages, including Java, are built on **three foundational principles**:

### 1. Encapsulation
> The mechanism that binds together code and the data it manipulates, and keeps both safe from outside interference and misuse.

In Java, encapsulation is achieved via the **class**: a class's variables (fields) are typically kept `private`, and access is only allowed through the class's own (usually `public`) methods. This is often called **data hiding**.

```java
class Account {
    private double balance;   // hidden data — cannot be accessed directly from outside

    public double getBalance() {      // controlled access
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) balance += amount;  // rules enforced here
    }
}
```
Why it matters: outside code cannot set `balance = -5000;` directly because `balance` is private — it must go through `deposit()`, which can enforce validation rules. This protects the integrity of the data.

### 2. Inheritance
> The process by which one object acquires the properties (fields and methods) of another object.

Inheritance supports the idea of **hierarchical classification** — instead of writing every class from scratch, a new class (**subclass**/**child**) can inherit the general attributes of an existing class (**superclass**/**parent**) and add its own specialized features. (Covered in full detail in Topic 8.)

```java
class Animal {           // superclass
    void eat() { System.out.println("This animal eats food."); }
}
class Dog extends Animal {   // subclass inherits eat()
    void bark() { System.out.println("The dog barks."); }
}
```

### 3. Polymorphism
> A feature (Greek for "many forms") that allows one interface to be used for a general class of actions; the specific action is determined by the exact nature of the situation.

The classic example: a "steering wheel" is one interface — whether the car has power steering or not, turning the wheel still steers the vehicle. In Java, polymorphism appears as:
- **Method Overloading** (compile-time / static polymorphism) — same method name, different parameter lists.
- **Method Overriding** (run-time / dynamic polymorphism) — subclass redefines a method inherited from its superclass.

*(Full detail with code is in Part C.)*

**Exam one-liner to memorize:**
> Encapsulation binds data and code together and hides it; Inheritance enables reuse and hierarchical classification; Polymorphism lets one interface serve many implementations.

## 2.4 JDK, JRE, and JVM (very frequently asked, Module 1 explicit topic)

| Term | Full form | What it is |
|---|---|---|
| **JVM** | Java Virtual Machine | The engine that actually **runs** Java bytecode. It loads `.class` files, verifies the bytecode for security, interprets/JIT-compiles it into native machine instructions, and manages memory (via garbage collection). The JVM is what makes Java platform-independent — every OS/CPU has its own JVM implementation, but the same bytecode runs on all of them. |
| **JRE** | Java Runtime Environment | The JVM **plus** the core class libraries (like `java.lang`, `java.util`) and supporting files needed to **run** already-compiled Java applications. If you only want to *run* Java programs (not develop them), the JRE is enough. |
| **JDK** | Java Development Kit | The full package needed to **develop** Java programs. It contains the JRE **plus** development tools: the compiler (`javac`), the debugger, `javadoc`, `jar`, etc. |

**Relationship (draw this as a diagram in your exam):**
```
 JDK
 ┌───────────────────────────────────────────┐
 │  Development tools: javac, javadoc, jar…   │
 │  ┌───────────────────────────────────────┐ │
 │  │  JRE                                   │ │
 │  │  Core class libraries (java.lang, ...) │ │
 │  │  ┌───────────────────────────────────┐ │ │
 │  │  │  JVM — loads/verifies/executes     │ │ │
 │  │  │  bytecode, memory management, GC   │ │ │
 │  │  └───────────────────────────────────┘ │ │
 │  └───────────────────────────────────────┘ │
 └───────────────────────────────────────────┘
```
**One-liner:** JDK ⊃ JRE ⊃ JVM (JDK contains JRE, JRE contains JVM + libraries).

## 2.5 Difference between C, C++, and Java (Module 1 explicit topic)

| Feature | C | C++ | Java |
|---|---|---|---|
| Paradigm | Procedural | Procedural + Object-Oriented | Purely Object-Oriented (except primitives) |
| Compilation | Compiles to native machine code | Compiles to native machine code | Compiles to **bytecode**, run by JVM |
| Platform dependence | Platform-dependent (recompile per OS/CPU) | Platform-dependent | **Platform-independent** ("Write Once, Run Anywhere") |
| Pointers | Full pointer arithmetic | Full pointer arithmetic | **No explicit pointers** (references only, no pointer arithmetic) — for security |
| Memory management | Manual (`malloc`/`free`) | Manual (`new`/`delete`) | **Automatic** — Garbage Collector |
| Multiple inheritance | N/A (no classes) | Supported (classes can extend multiple classes) | **Not supported for classes** (avoids ambiguity); achieved safely via **interfaces** |
| Header files | Uses `#include` header files | Uses `#include` header files | Uses `import` — no separate header files |
| Operator overloading | Not applicable | Supported | **Not supported** (kept out for simplicity) |
| goto statement | Supported | Supported | **Not supported** (`goto` is a reserved but unused keyword) |
| Thread support | No built-in support (needs OS libraries) | No built-in support (needs OS libraries) | **Built-in** multithreading support |
| Security | Low (direct memory access) | Low (direct memory access) | High (bytecode verification, sandboxing, no pointers) |

## 2.6 A First Simple Program (Java Hello World)

```java
class Example {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

### Line-by-line, exam-style breakdown

- `class Example { ... }` — Everything in a Java program happens inside a **class**. `Example` is the class name; by convention it should match the filename (`Example.java`).
- `public static void main(String[] args)` — This is the **entry point** of every standalone Java application. The JVM looks specifically for a method with this exact signature to begin execution.
  - `public` — access modifier; `main` must be public so the JVM (from outside the class) can call it.
  - `static` — means the method belongs to the **class itself**, not to an instance/object. This lets the JVM invoke `main()` without first creating an object of `Example`.
  - `void` — `main()` does not return any value back to the JVM.
  - `main` — the fixed, required method name for the entry point.
  - `String[] args` — an array of `String`s that holds any **command-line arguments** passed to the program.
- `System.out.println("Hello World");`
  - `System` — a built-in class in `java.lang`.
  - `out` — a static field of `System`, an object of type `PrintStream`, representing standard output (the console).
  - `println()` — a method of `PrintStream` that prints its argument followed by a newline.

### Compiling and running
```
javac Example.java     → produces Example.class (bytecode)
java Example            → JVM loads Example.class and runs main()
```
**Note:** the file must be named `Example.java` (matching the public class name exactly, including case) or the compiler will error.

## 2.7 A Second Short Program — Variables and simple math
```java
class Example2 {
    public static void main(String[] args) {
        int num;       // declare an integer variable
        num = 100;      // assign
        System.out.println("This is num: " + num);
        num = num * 2;
        System.out.print("The value of num * 2 is ");
        System.out.println(num);
    }
}
```
This demonstrates: variable declaration, assignment, string concatenation with `+`, and the difference between `print()` (no newline) and `println()` (adds newline).

## 2.8 Two control statements previewed here (full detail in Topic 5)

**`if` statement:**
```java
if (num < 0)
    System.out.println("Number is negative");
```

**`for` loop:**
```java
for (int i = 0; i < 5; i++) {
    System.out.println("Count: " + i);
}
```

## 2.9 Blocks of code
Java lets you group two or more statements into a **block** using `{ }`. A block defines a scope — every variable declared inside a block is local to that block.
```java
if (x < y) {
    x = 0;
    y = y - x;
}   // multi-statement block, executes as one unit
```

## 2.10 Lexical Issues (Module 1: comments, identifiers)

- **Whitespace**: Java ignores extra spaces, tabs, and newlines between tokens (a "free-form" language).
- **Identifiers**: names for variables, methods, classes. Rules: must start with a letter, underscore `_`, or dollar sign `$`; can be followed by letters/digits; are **case-sensitive** (`total` ≠ `Total`); cannot be a reserved keyword.
- **Literals**: constant values fixed at compile time, e.g. `100`, `98.6`, `'X'`, `"This is a string"`, `true`.
- **Comments** (Java Comment — explicit Module 1 topic): three styles —
  ```java
  // single-line comment
  /* multi-line
     comment */
  /** documentation comment — used by the javadoc tool
      to auto-generate HTML documentation */
  ```
- **Separators**: symbols like `( )`, `{ }`, `[ ]`, `;`, `,`, `.` used to organize code structure.
- **Java Keywords**: reserved words with special meaning (`class`, `if`, `while`, `public`, `static`, `void`, `int`, etc.) — cannot be used as identifiers.

## 2.11 The Java Class Libraries
Java programs rely heavily on **pre-built, standard class libraries** (also called the API — Application Programming Interface), such as `java.lang` (core classes, imported automatically), `java.util` (collections, utilities), `java.io` (input/output), etc. This is unlike C, where you must write most functionality yourself.

---

# TOPIC 3: Data Types, Variables, and Arrays

## 3.1 Java Is a Strongly Typed Language
Three key implications (an exam favorite):
1. Every variable has a **type**, every expression has a type, and every type is **strictly defined**.
2. All assignments — between types, and when passing parameters to methods — are **checked for type compatibility** by the compiler.
3. There is **no automatic, unchecked coercion** between incompatible types (unlike some looser languages).

## 3.2 The Primitive Types (Module 1: Java Data Types)

Java has exactly **8 primitive types**, divided into four groups:

| Group | Types |
|---|---|
| Integers | `byte`, `short`, `int`, `long` |
| Floating-point | `float`, `double` |
| Character | `char` |
| Boolean | `boolean` |

These are **not objects** — they are predefined by the language and named by a reserved keyword. Crucially, Java defines the **exact size and range** of each type (unlike C/C++, where `int` size can vary by machine) — this is part of what makes Java portable.

### Integer types

| Type | Size | Range |
|---|---|---|
| `byte` | 8-bit | –128 to 127 |
| `short` | 16-bit | –32,768 to 32,767 |
| `int` | 32-bit | –2,147,483,648 to 2,147,483,647 |
| `long` | 64-bit | –9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |

All Java integer types are **signed** (positive and negative) — there is no `unsigned` keyword in Java.

```java
byte  b  = 100;
short s  = 20000;
int   i  = 100000;
long  l  = 100000000L;   // 'L' suffix required for long literals beyond int range
```

### Floating-point types

| Type | Size | Precision |
|---|---|---|
| `float` | 32-bit | single precision, ~6-7 significant decimal digits |
| `double` | 64-bit | double precision, faster for many computations on modern CPUs, default choice |

```java
double pi = 3.14159265358979;
float  f  = 3.14f;    // 'f' suffix required — otherwise Java treats decimal literals as double
```

### `char` type
Unlike C/C++ where `char` is typically 8-bit, **Java's `char` is 16-bit unsigned**, used to represent Unicode characters (supporting international character sets, not just ASCII/Latin).
```java
char ch1 = 'X';
char ch2 = 88;        // char can be treated as an integer (Unicode code point)
ch2++;                 // ch2 now represents 'Y'
```

### `boolean` type
Can only hold the values `true` or `false`. In Java (unlike C), integers **cannot** be substituted for boolean — `if (1)` is a compile error.
```java
boolean flag = true;
if (flag) System.out.println("This is executed.");
```

## 3.3 A Closer Look at Literals

- **Integer literals**: default type `int`. Prefix `0x`/`0X` = hexadecimal, `0` = octal (legacy). Suffix `L`/`l` makes it a `long`.
- **Floating-point literals**: default type `double`. Suffix `F`/`f` = float, `D`/`d` = double (optional, redundant since double is default).
- **Boolean literals**: only `true` and `false` — these are keywords, not the integers 1/0 as in C.
- **Character literals**: single character in single quotes, e.g. `'a'`. Special **escape sequences**: `\n` (newline), `\t` (tab), `\\` (backslash), `\'` (single quote), `\"` (double quote), `\uxxxx` (Unicode).
- **String literals**: sequence of characters in double quotes, e.g. `"Hello"`. In Java, `String` is technically a class/object, but string literals get special compiler support.

## 3.4 Variables

### Declaring a variable
```java
type identifier [ = value ][, identifier [ = value ] ...];
// examples:
int a, b, c;
int d = 3, e, f = 5;
byte z = 22;
double pi = 3.14159;
char x = 'x';
```

### Dynamic Initialization
Java allows variables to be initialized **dynamically**, using any expression valid at the time the variable is declared (not just constants):
```java
double a = 3.0, b = 4.0;
double c = Math.sqrt(a * a + b * b);   // computed at run time, not a fixed literal
```

### Scope and Lifetime of Variables
- Java's scopes are defined by **blocks** (`{ }`).
- A variable declared inside a block is **not visible** outside that block (it goes out of scope), and does not exist (its lifetime ends) once the block finishes executing.
- Variables are **not** automatically initialized to zero/default in local scope — a local variable must be explicitly initialized before use, or the compiler throws an error. (Instance/class fields *are* auto-initialized to default values like 0, false, null.)

```java
int x = 10;
{                       // start new nested block
    int y = 20;         // y is local to this block only
    System.out.println(x + y);   // OK — x is visible here (outer scope)
}
// y is not accessible here — out of scope
```

## 3.5 Type Conversion and Casting

### Automatic (widening) conversion
Java performs automatic type conversion when: (a) the two types are compatible, and (b) the destination type is **larger** (wider) than the source type — no data is lost.
```java
int i = 100;
long l = i;      // automatic widening — int -> long, no cast needed
float f = l;      // long -> float, automatic
```
Widening order (memorize): `byte → short → int → long → float → double` (also `char → int`).

### Casting incompatible types (narrowing)
When converting from a **larger** type to a **smaller** one (or between incompatible types), you must use an explicit **cast** — data may be lost/truncated.
```java
int i = 300;
byte b = (byte) i;    // explicit cast required; result may overflow (b = 44 here, due to truncation)

double d = 100.04;
int x = (int) d;       // x = 100 — fractional part is simply dropped, not rounded
```
General cast syntax: `(target-type) value`

### Automatic Type Promotion in Expressions
Within expressions, Java automatically promotes smaller integer types (`byte`, `short`, `char`) to `int` before performing the operation:
```java
byte b = 10;
byte c = 20;
// byte d = b + c;      // ERROR — b + c is promoted to int, cannot assign int to byte directly
int d = b + c;           // OK
byte e = (byte)(b + c);  // OK with explicit cast
```

## 3.6 Arrays

> An **array** is a group of like-typed variables referred to by a common name; a fixed-size, ordered collection of elements of the same type, accessed via an index (starting at 0).

### One-Dimensional Arrays
```java
int[] month_days;                       // declaration (no size yet — arrays are reference types)
month_days = new int[12];               // allocation — creates array of 12 ints, default value 0
month_days[0] = 31;                     // access via index
month_days[1] = 28;

// declare + initialize together:
int[] nums = {10, 20, 30, 40};          // array literal / initializer
System.out.println(nums.length);        // 4 — 'length' is a public final field of every array

for (int i = 0; i < nums.length; i++) {
    System.out.println(nums[i]);
}
```
Key points: array indices run from `0` to `length-1`; accessing an out-of-range index throws `ArrayIndexOutOfBoundsException` at run time; `array.length` gives the size (no parentheses — it's a field, not a method).

### Multidimensional Arrays
Java implements multidimensional arrays as "arrays of arrays."
```java
int[][] twoD = new int[4][5];   // 4 rows, 5 columns
int counter = 0;
for (int i = 0; i < 4; i++)
    for (int j = 0; j < 5; j++) {
        twoD[i][j] = counter;
        counter++;
    }

// Irregular (jagged) arrays are legal in Java — rows can have different lengths:
int[][] triangle = new int[4][];
triangle[0] = new int[1];
triangle[1] = new int[2];
triangle[2] = new int[3];
triangle[3] = new int[4];

// array-of-arrays literal
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

### Alternative Array Declaration Syntax
Both of these are valid and equivalent (the second is the C-style syntax, also allowed in Java):
```java
int[] a1 = new int[3];   // preferred Java style
int a2[] = new int[3];   // also legal
```

## 3.7 A Few Words About Strings
Although not a primitive type, `String` is used constantly. A `String` object is **immutable** — once created, its contents cannot be changed. (Full detail on `String` methods is in Part C.)
```java
String str = "Java strings are immutable objects, not primitive types.";
System.out.println(str.length());
```

## 3.8 Java Input and Output (Module 1 explicit topic)

Java's console I/O is stream-based (`java.io`), and modern code typically uses the `Scanner` class from `java.util` for input.

```java
import java.util.Scanner;

class InputDemo {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = sc.nextLine();

        System.out.print("Enter your age: ");
        int age = sc.nextInt();

        System.out.println("Hello " + name + ", you are " + age + " years old.");
        sc.close();
    }
}
```
Common `Scanner` methods: `nextInt()`, `nextDouble()`, `nextLine()` (reads a full line), `next()` (reads one token/word), `nextBoolean()`.

**Output** is done via the predefined `System.out` object (a `PrintStream`):
- `System.out.print(x)` — prints without a newline
- `System.out.println(x)` — prints with a trailing newline
- `System.out.printf("%d %s", x, y)` — formatted output, C-style format specifiers

## 3.9 Java Expressions and Blocks (Module 1 explicit topic)
- An **expression** is any valid combination of variables, literals, operators, and method calls that evaluates to a single value, e.g. `a + b * 2`, `x > 5`, `getBalance()`.
- A **block** is a group of statements enclosed in `{ }`, treated syntactically as a single statement (used in `if`, loops, methods, classes).

---

# TOPIC 4: Operators

Java provides a rich operator set, grouped into: **arithmetic**, **bitwise**, **relational**, **boolean logical**, and **assignment**, plus the special **ternary (`?:`)** operator.

## 4.1 Arithmetic Operators

| Operator | Meaning |
|---|---|
| `+` | Addition (also string concatenation) |
| `-` | Subtraction (also unary minus) |
| `*` | Multiplication |
| `/` | Division |
| `%` | Modulus (remainder) |
| `++` | Increment |
| `--` | Decrement |
| `+=`, `-=`, `*=`, `/=`, `%=` | Compound assignment |

```java
int a = 10, b = 3;
System.out.println(a + b);   // 13
System.out.println(a - b);   // 7
System.out.println(a * b);   // 30
System.out.println(a / b);   // 3   (integer division truncates)
System.out.println(a % b);   // 1   (remainder)

double x = 10.0, y = 3.0;
System.out.println(x / y);   // 3.3333333333333335 (floating division)
```

### The Modulus Operator
`%` returns the remainder of a division. Works for both integer and floating-point operands.
```java
System.out.println(10 % 3);     // 1
System.out.println(10.5 % 3);   // 1.5
```

### Compound Assignment
```java
int a = 10;
a += 5;   // same as a = a + 5;  → a = 15
a -= 3;   // a = 12
a *= 2;   // a = 24
```
Benefit: more compact, and for complex expressions like `a = a + b`, more efficient (some compilers can optimize compound assignment for array indexing).

### Increment / Decrement (`++` / `--`)
```java
int x = 10;
int y = ++x;   // pre-increment: x becomes 11 FIRST, then y = 11
int z = x++;   // post-increment: z = 11 (old value used) FIRST, then x becomes 12
```
**Exam rule to memorize:** *Pre*-increment/decrement changes the value **before** it's used in the expression. *Post*-increment/decrement changes the value **after** it's used.

## 4.2 The Bitwise Operators
Apply directly to the individual bits of integer types (`long`, `int`, `short`, `char`, `byte`).

| Operator | Meaning |
|---|---|
| `&` | Bitwise AND |
| `\|` | Bitwise OR |
| `^` | Bitwise XOR |
| `~` | Bitwise complement (unary NOT) |
| `<<` | Left shift |
| `>>` | Signed (arithmetic) right shift |
| `>>>` | Unsigned right shift |

```java
int a = 6;    // binary: 0110
int b = 5;    // binary: 0101
System.out.println(a & b);   // 0100 = 4  (AND)
System.out.println(a | b);   // 0111 = 7  (OR)
System.out.println(a ^ b);   // 0011 = 2  (XOR — 1 where bits differ)
System.out.println(~a);      // -7        (bitwise NOT, flips every bit)

int val = 8;
System.out.println(val << 2);   // 32  (8 * 2^2 — left shift multiplies by powers of 2)
System.out.println(val >> 2);   // 2   (8 / 2^2 — right shift divides by powers of 2)

int neg = -8;
System.out.println(neg >> 1);    // -4  (sign bit preserved — arithmetic shift)
System.out.println(neg >>> 1);   // large positive number (zero-fills from the left, ignores sign)
```
**Key distinction (frequently tested):** `>>` preserves the sign bit (fills with 1s for negative numbers), while `>>>` always fills with 0s regardless of sign — so `>>>` is Java-specific (C/C++ doesn't have it) and only makes sense for signed types where you want an unsigned-style shift.

Bitwise compound assignment also exists: `&=`, `|=`, `^=`, `<<=`, `>>=`, `>>>=`.

## 4.3 Relational Operators
Compare two values and produce a `boolean` result.

| Operator | Meaning |
|---|---|
| `==` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

```java
int a = 5, b = 10;
System.out.println(a == b);   // false
System.out.println(a < b);    // true
```
**Warning (exam trap):** for objects (like `String`), `==` compares **references** (memory addresses), not content. Use `.equals()` to compare content:
```java
String s1 = new String("hi");
String s2 = new String("hi");
System.out.println(s1 == s2);        // false — different objects
System.out.println(s1.equals(s2));   // true  — same content
```

## 4.4 Boolean Logical Operators
Operate only on `boolean` operands.

| Operator | Meaning |
|---|---|
| `&` | Logical AND (evaluates both sides always) |
| `\|` | Logical OR (evaluates both sides always) |
| `^` | Logical XOR (true if operands differ) |
| `!` | Logical NOT (unary) |
| `&&` | Short-circuit AND |
| `\|\|` | Short-circuit OR |

### Short-Circuit Logical Operators (commonly tested)
`&&` and `||` do **not** evaluate the right-hand operand if the result is already determined by the left-hand operand:
- `&&`: if the left side is `false`, the whole expression is `false` — right side is skipped.
- `||`: if the left side is `true`, the whole expression is `true` — right side is skipped.

```java
int a = 0;
if (a != 0 && (10 / a > 1)) {   // short-circuit prevents divide-by-zero:
    System.out.println("won't reach here safely if a==0, but && protects us");
}
```
This is used defensively — e.g., checking `obj != null && obj.value() > 0` safely avoids a `NullPointerException`.

## 4.5 The Assignment Operator
`=` assigns the value of the right-hand expression to the variable on the left. Java allows **chained assignment**:
```java
int a, b, c;
a = b = c = 100;   // all three variables get 100
```

## 4.6 The `?:` (Ternary) Operator
A compact shorthand for a simple `if-else`.
```java
result = condition ? expression1 : expression2;
// example:
int a = 10, b = 20;
int min = (a < b) ? a : b;   // min = 10
```
Read as: "if condition is true, the value is expression1; otherwise the value is expression2."

## 4.7 Operator Precedence (know the general order for exams)

Highest → Lowest (simplified, commonly tested subset):
```
()  []  .                          (highest)
++  --  ~  !  (unary)
*   /   %
+   -
<<  >>  >>>
<  <=  >  >=  instanceof
==  !=
&
^
|
&&
||
?:
=  +=  -=  *=  /=  %=  &=  ^=  |=  <<=  >>=  >>>=   (lowest)
```
**Using Parentheses:** When in doubt (or to make code clearer), use explicit parentheses `()` — they never hurt, and they override default precedence to force your intended order of evaluation. E.g. `a + b * c` is `a + (b*c)`, but `(a + b) * c` changes the result entirely.

---

# TOPIC 5: Control Statements

Java's control statements are grouped into three categories: **selection** (`if`, `switch`), **iteration** (`while`, `do-while`, `for`, for-each), and **jump** (`break`, `continue`, `return`).

## 5.1 Selection Statements

### `if`
```java
if (condition) {
    // executes if condition is true
} else if (anotherCondition) {
    // executes if first is false, this is true
} else {
    // executes if none are true
}
```
Example — nested if / if-else-if ladder:
```java
int marks = 75;
if (marks >= 90) {
    System.out.println("Grade A");
} else if (marks >= 75) {
    System.out.println("Grade B");
} else if (marks >= 50) {
    System.out.println("Grade C");
} else {
    System.out.println("Fail");
}
```

### `switch` (Module 1: Java switch Statement)
A multi-way branch statement, cleaner than a long `if-else-if` ladder when comparing **one variable** against several **constant** values.

```java
int day = 3;
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    default:
        System.out.println("Invalid day");
}
```

**Rules to memorize:**
- The switch expression must evaluate to `byte`, `short`, `char`, `int`, an enum type, or `String` (String support added in Java 7 — beyond this book, but standard now).
- `case` values must be **constant expressions** (literals or `final` constants) — no ranges, no variables.
- `break` exits the switch; **without `break`, execution "falls through"** into the next case — this is a very common exam trick question.
- `default` is optional, executed when no `case` matches; can appear anywhere but usually placed last.

**Fall-through example (exam favorite):**
```java
int x = 2;
switch (x) {
    case 1:
    case 2:
    case 3:
        System.out.println("1, 2, or 3");   // grouped cases — no break needed between them
        break;
    case 4:
        System.out.println("4");
        break;
}
// Output: "1, 2, or 3" — because case 2 falls through with no code until the break
```

**Nested switch statements** are allowed — a `switch` can be inside a `case` of an outer `switch`, and Java correctly resolves each switch's own `case` constants independently, even if constants are reused.

## 5.2 Iteration Statements (Loops)

### `while`
Tests the condition **before** each iteration — may execute zero times.
```java
int n = 5;
while (n > 0) {
    System.out.println(n);
    n--;
}
```

### `do-while`
Tests the condition **after** each iteration — guaranteed to execute **at least once**.
```java
int n = 5;
do {
    System.out.println(n);
    n--;
} while (n > 0);
```
Useful when you need code (e.g., a menu prompt) to run at least once before checking whether to repeat.

### `for`
```java
for (initialization; condition; iteration) {
    // body
}
// example:
for (int i = 1; i <= 5; i++) {
    System.out.println("i = " + i);
}
```
Execution order: `initialization` runs once → `condition` checked → if true, body runs → `iteration` runs → condition checked again → repeat until `condition` is false.

Java's `for` is flexible: you can declare multiple loop variables, omit any of the three sections (e.g. `for (;;) { }` is an infinite loop), and use commas to combine multiple statements in the init/iteration clauses:
```java
for (int i = 0, j = 10; i < j; i++, j--) {
    System.out.println(i + " " + j);
}
```

### The For-Each Version of the `for` Loop (Module 1: for-each loop)
Introduced in Java 5, designed to cycle through a collection or array in strictly sequential order, from start to finish.
```java
int[] nums = {10, 20, 30, 40};
for (int x : nums) {          // read as "for each x in nums"
    System.out.println(x);
}
```
**Key limitation (exam trap):** the for-each loop variable is a **copy** of each element — modifying it does **not** change the original array/collection.
```java
int[] nums = {1, 2, 3};
for (int x : nums) {
    x = x * 10;    // this does NOT change nums[] itself
}
// nums is still {1, 2, 3}
```
Also useful for iterating multidimensional arrays and any class implementing `Iterable` (like `ArrayList`).

### Nested Loops
A loop inside another loop — the inner loop completes all its iterations for each single iteration of the outer loop.
```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        System.out.print(i * j + " ");
    }
    System.out.println();
}
```

## 5.3 Jump Statements

### `break`
Two uses:
1. **Terminate a loop** — exits the innermost enclosing loop immediately.
2. **Exit a `switch`** — as shown above.

```java
for (int i = 0; i < 10; i++) {
    if (i == 5) break;   // loop stops entirely when i == 5
    System.out.println(i);
}
// prints 0 1 2 3 4
```

**Labeled `break`** — Java has no `goto`, but a labeled `break` lets you jump out of *nested* loops directly:
```java
outer:
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (j == 1) break outer;   // breaks BOTH loops, not just the inner one
        System.out.println(i + " " + j);
    }
}
```

### `continue`
Skips the **rest of the current iteration** and moves directly to the next iteration test (does not exit the loop, unlike `break`).
```java
for (int i = 0; i < 5; i++) {
    if (i % 2 == 0) continue;   // skip even numbers
    System.out.println(i);
}
// prints 1 3
```
Labeled `continue` also exists, for skipping to the next iteration of an *outer* loop from inside a nested loop.

### `return`
Exits the current method immediately and, if the method is non-void, sends a value back to the caller.
```java
int square(int x) {
    return x * x;   // exits the method here, returns the computed value
}
```

---

# TOPIC 6: Introducing Classes

This is the heart of Java OOP. Classes are the mechanism through which encapsulation (Topic 2.3) is implemented.

## 6.1 Class Fundamentals

> A **class** is a template/blueprint that defines the form of an object — it specifies both the **data** (fields/instance variables) and the **code** (methods) that will operate on that data. An **object** is an *instance* of a class.

### General form of a class
```java
class ClassName {
    // fields (instance variables / state)
    type instanceVar1;
    type instanceVar2;

    // methods (behavior)
    returnType methodName1(parameters) {
        // method body
    }
    returnType methodName2(parameters) {
        // method body
    }
}
```

### A simple class example
```java
class Box {
    double width;
    double height;
    double depth;
}

class BoxDemo {
    public static void main(String[] args) {
        Box mybox = new Box();     // create an object of Box
        mybox.width  = 10;
        mybox.height = 20;
        mybox.depth  = 15;

        double vol = mybox.width * mybox.height * mybox.depth;
        System.out.println("Volume is " + vol);
    }
}
```

## 6.2 Declaring Objects — Two Steps
Declaring an object of a class is a **two-step process** — this is a critically important concept (frequently tested):

1. **Declare a variable of the class type** — this creates only a **reference** to an object (currently pointing to nothing, i.e. `null`); no object exists yet.
2. **Acquire an actual, physical copy of the object using `new`** and assign it to that reference.

```java
Box mybox;             // Step 1: mybox is a reference variable, currently null
mybox = new Box();     // Step 2: actual Box object created in memory; mybox now refers to it
// (often combined:)
Box mybox2 = new Box();
```
This two-step process explains why Java's class variables are called "reference variables" — they store a *reference* (memory address) to the object, not the object's data directly.

### A Closer Look at `new`
`new` dynamically allocates memory for an object at run time and returns a reference to it. Java handles all memory management automatically — you never need to explicitly free the memory (that's the Garbage Collector's job — see 6.7).

### Assigning Object Reference Variables — the sharing trap (very common exam trick)
```java
Box b1 = new Box();
Box b2 = b1;     // b2 now refers to the SAME object as b1, NOT a copy!

b2.width = 100;
System.out.println(b1.width);   // prints 100, because b1 and b2 point to the same object
```
Setting `b2 = null` afterward would only make `b2` stop referring to the object — `b1` would be unaffected, because it's a separate reference to the same object.

## 6.3 Introducing Methods

### General form
```java
type name(parameter-list) {
    // body of method
    // includes 'return value;' if type is not void
}
```

### Adding a method to the Box class
```java
class Box {
    double width, height, depth;

    void volume() {                      // method with no return value
        System.out.println("Volume is " + (width * height * depth));
    }
}
// call it:
Box mybox = new Box();
mybox.width = 10; mybox.height = 5; mybox.depth = 2;
mybox.volume();     // "Volume is 100.0"
```

### Returning a value
```java
double volume() {
    return width * height * depth;    // returns a double
}
// usage:
double vol = mybox.volume();
```

### Adding a method that takes parameters
```java
void setDim(double w, double h, double d) {
    width = w;
    height = h;
    depth = d;
}
// usage:
Box mybox = new Box();
mybox.setDim(10, 5, 2);
```
A **parameter** is a variable defined by a method that receives a value when the method is called; the value passed in the call is called an **argument**.

## 6.4 Constructors

> A **constructor** is a special method that is automatically called immediately after an object is created (right after `new`), used to initialize the object's state.

**Rules:**
- Has the **exact same name as the class**.
- Has **no return type** (not even `void`) — specifying a return type would make it a normal method, not a constructor.
- If you don't define any constructor, Java automatically supplies a **default constructor** (no arguments, does nothing but zero-initialize fields).

```java
class Box {
    double width, height, depth;

    Box() {                       // constructor — same name as class, no return type
        System.out.println("Constructing Box");
        width = height = depth = 1;
    }
}
// usage:
Box mybox1 = new Box();   // "Constructing Box" is printed automatically
```

### Parameterized Constructors
Constructors can take parameters, letting you initialize an object with custom values at creation time — this is far more efficient than setting fields one by one after construction.
```java
class Box {
    double width, height, depth;

    Box(double w, double h, double d) {
        width = w;
        height = h;
        depth = d;
    }
}
// usage:
Box mybox1 = new Box(10, 20, 15);
```
**Important:** the moment you define ANY constructor, Java **no longer** supplies the default no-argument constructor automatically — if you still need a no-arg constructor, you must write it explicitly.

## 6.5 The `this` Keyword

> `this` refers to **the current object** — the object whose method or constructor is currently being executed. It is used inside an instance method or constructor to refer to the current object.

Most common use: resolving naming conflicts between instance variables and parameters (**instance variable hiding**):
```java
class Box {
    double width, height, depth;

    Box(double width, double height, double depth) {   // parameters SAME name as fields
        this.width  = width;    // 'this.width' = the field, 'width' = the parameter
        this.height = height;
        this.depth  = depth;
    }
}
```
Without `this`, `width = width;` would just assign the parameter to itself and leave the actual field untouched — a classic beginner bug. `this` disambiguates: "the field belonging to *this* object" vs. the local parameter.

## 6.6 Garbage Collection

Because objects are dynamically allocated via `new`, Java needs a way to free memory that is no longer used. Unlike C++ (manual `delete`), Java handles this **automatically**:

> **Garbage collection** works by tracking which objects are no longer referenced by anything in the running program (i.e., unreachable), and automatically reclaiming their memory. This happens transparently — you never explicitly destroy an object.

```java
Box b = new Box();
b = null;   // the original Box object is now unreferenced -> eligible for garbage collection
```

## 6.7 The `finalize()` Method
Historically, Java allowed a class to define a `finalize()` method that the garbage collector would call on an object right before reclaiming its memory, to perform cleanup. **Exam note:** this mechanism is largely deprecated/unreliable in modern Java, but the textbook covers it as part of the GC discussion — know the concept (cleanup before collection) even though it's rarely used in practice today.

## 6.8 A Complete Worked Example — A Stack Class
This example (a classic from the book, rewritten here) ties fields + constructor + methods together:
```java
class MyStack {
    private int[] stck;
    private int tos;

    MyStack(int size) {              // constructor
        stck = new int[size];
        tos = -1;
    }

    void push(int item) {            // method: add to stack
        if (tos == stck.length - 1)
            System.out.println("Stack is full.");
        else
            stck[++tos] = item;
    }

    int pop() {                      // method: remove from stack
        if (tos < 0) {
            System.out.println("Stack underflow.");
            return 0;
        } else
            return stck[tos--];
    }
}

class StackDemo {
    public static void main(String[] args) {
        MyStack s1 = new MyStack(10);
        for (int i = 0; i < 10; i++) s1.push(i);
        for (int i = 0; i < 10; i++) System.out.println(s1.pop());
    }
}
```
This shows encapsulation in action: `stck` and `tos` are `private` (hidden), and all interaction happens through `push()`/`pop()`.

---

# TOPIC 8: Inheritance

## 8.1 Inheritance Basics

> **Inheritance** is the process by which a new class (the **subclass**, or **derived class**) acquires the members (fields and methods) of an existing class (the **superclass**, or **base class**), using the keyword `extends`. It supports the concept of hierarchical classification and enables **code reuse**.

```java
class A {
    int i, j;
    void showij() {
        System.out.println("i and j: " + i + " " + j);
    }
}

// B is a subclass of A. B includes all of A's members, plus its own.
class B extends A {
    int k;
    void showk() {
        System.out.println("k: " + k);
    }
    void sum() {
        System.out.println("i+j+k: " + (i + j + k));   // B can use i and j, inherited from A
    }
}

class SimpleInheritance {
    public static void main(String[] args) {
        A superOb = new A();
        B subOb = new B();

        superOb.i = 10; superOb.j = 20;
        subOb.i = 7; subOb.j = 8; subOb.k = 9;   // subOb has access to inherited i, j PLUS its own k

        subOb.sum();   // "i+j+k: 24"
    }
}
```
**Key rule:** Java does **not** support multiple inheritance of classes — a class can only `extends` **one** superclass directly (unlike C++). This avoids the ambiguity problems of multiple inheritance (e.g., the "diamond problem"). Java achieves similar flexibility safely through **interfaces** (see Part C).

## 8.2 Member Access and Inheritance
A subclass includes all of the members of its superclass, **but it cannot access those members of the superclass that are declared `private`.**
```java
class A {
    int i;         // default access — accessible to subclass
    private int j; // private — NOT accessible to subclass B
    void setij(int x, int y) { i = x; j = y; }
}
class B extends A {
    int total;
    void sum() {
        total = i;      // OK
        // total = i + j;  // ERROR — j is private to A, invisible to B
    }
}
```
This is why access modifiers matter so much in inheritance design (see Part C, Access Modifiers).

## 8.3 A Superclass Variable Can Reference a Subclass Object (very important — foundation of polymorphism)

> A reference variable of a superclass type can be used to refer to an object of any subclass derived from that superclass. This is called **upcasting**, and it is legal because every subclass object "IS-A" superclass object too.

```java
class A { int i = 10; }
class B extends A { int k = 20; }

A a;
B b = new B();
a = b;    // legal — a superclass reference can point to a subclass object
// a.k = 99;  // ERROR — 'a' is declared as type A, so it can only see members defined in A
```
The reverse is **not** automatically allowed: a subclass reference cannot refer to a superclass object without an explicit (and potentially unsafe) cast — a superclass object does not necessarily have the extra members a subclass adds.

## 8.4 Using `super`

`super` has **two general forms** in Java — both extremely commonly tested.

### Form 1: Calling the superclass's constructor
```java
class Box {
    double width, height, depth;
    Box(double w, double h, double d) {
        width = w; height = h; depth = d;
    }
}

class BoxWeight extends Box {
    double weight;
    BoxWeight(double w, double h, double d, double m) {
        super(w, h, d);   // calls Box's constructor — MUST be the first statement in the subclass constructor
        weight = m;
    }
}
```
**Rule:** `super(parameter-list)` must be the **first statement executed** in a subclass constructor. If a subclass constructor doesn't explicitly call `super()`, Java automatically calls the superclass's **no-argument** constructor before the subclass constructor's own body runs.

### Form 2: Accessing a superclass member hidden/overridden by the subclass
```java
class A {
    int i = 10;
    void show() { System.out.println("A's show(), i = " + i); }
}
class B extends A {
    int i = 20;                    // B's own 'i' hides A's 'i'
    void show() {
        super.show();               // explicitly calls A's version of show()
        System.out.println("B's show(), i = " + i);
        System.out.println("super.i = " + super.i);   // access A's hidden 'i'
    }
}
```
`super.member` lets a subclass explicitly access a field or method of its immediate superclass, even if the subclass has redefined a member with the same name.

## 8.5 Creating a Multilevel Hierarchy
A class can serve as both a superclass (to something below it) and a subclass (of something above it) — chains like `A → B → C` are fully supported and inherit transitively.
```java
class A { int i; }
class B extends A { int j; }
class C extends B { int k; }   // C inherits from B, which inherits from A
                                 // -> C has access to i (from A), j (from B), and k (its own)
```

## 8.6 When Constructors Are Called (important, always tested with a "predict the output" question)

> In a class hierarchy, constructors are called in **order of derivation, from superclass to subclass** — the superclass constructor always completes *before* the subclass constructor's own body executes.

```java
class A {
    A() { System.out.println("Inside A's constructor."); }
}
class B extends A {
    B() { System.out.println("Inside B's constructor."); }
}
class C extends B {
    C() { System.out.println("Inside C's constructor."); }
}
class CallingCons {
    public static void main(String[] args) {
        C c = new C();
    }
}
```
**Output:**
```
Inside A's constructor.
Inside B's constructor.
Inside C's constructor.
```
Makes sense logically: a subclass often depends on members initialized by its superclass, so the superclass must be fully constructed first.

## 8.7 Method Overriding (core polymorphism mechanism — extremely important)

> **Method overriding** occurs when a method in a subclass has the **same name, same return type, and same parameter list** as a method in its superclass. The subclass's version then **overrides** (replaces) the superclass's version for objects of the subclass type.

```java
class A {
    int i, j;
    A(int a, int b) { i = a; j = b; }
    void show() {
        System.out.println("i and j: " + i + " " + j);
    }
}
class B extends A {
    int k;
    B(int a, int b, int c) {
        super(a, b);
        k = c;
    }
    @Override
    void show() {                                  // OVERRIDES A's show(), not overloads
        System.out.println("k: " + k);
    }
}
class Override {
    public static void main(String[] args) {
        B subOb = new B(1, 2, 3);
        subOb.show();   // calls B's show() -- "k: 3" only, A's show() is completely replaced
    }
}
```
**Overriding vs. Overloading (a top exam-comparison question):**

| | Method Overloading | Method Overriding |
|---|---|---|
| Where | Within the same class (or a subclass adding new variants) | Between superclass and subclass |
| Signature | Same name, **different** parameter list | Same name, **same** return type & parameter list |
| Binding | Resolved at **compile time** (static polymorphism) | Resolved at **run time** (dynamic polymorphism) |
| Purpose | Provide multiple ways to call a method with different inputs | Provide a specialized implementation in a subclass |

**Note:** if the subclass method's signature is even slightly different (different parameters), it is **not** overriding — it becomes a separate overloaded method instead, and both versions would coexist.

## 8.8 Dynamic Method Dispatch (THE most important OOP mechanism for exams)

> **Dynamic method dispatch** is the mechanism by which a call to an overridden method is resolved at **run time**, rather than compile time. Java determines *which* version of an overridden method to call based on the **actual type of the object being referred to at the time the call occurs** — not the type of the reference variable.

This is how Java implements **run-time polymorphism**.

```java
class Figure {
    double dim1, dim2;
    Figure(double a, double b) { dim1 = a; dim2 = b; }
    double area() {
        System.out.println("Area for Figure is undefined.");
        return 0;
    }
}
class Rectangle extends Figure {
    Rectangle(double a, double b) { super(a, b); }
    @Override
    double area() { return dim1 * dim2; }
}
class Triangle extends Figure {
    Triangle(double a, double b) { super(a, b); }
    @Override
    double area() { return dim1 * dim2 / 2; }
}

class FindAreas {
    public static void main(String[] args) {
        Figure figref;                        // superclass reference variable
        Rectangle r = new Rectangle(9, 5);
        Triangle t = new Triangle(10, 8);

        figref = r;
        System.out.println("Area is " + figref.area());   // calls Rectangle's area() -> 45.0

        figref = t;
        System.out.println("Area is " + figref.area());   // calls Triangle's area() -> 40.0
    }
}
```
**Why this matters (write this in exams verbatim-style):** Even though `figref` is declared as type `Figure`, the JVM looks at the **actual object** `figref` currently points to at run time, and calls **that object's** version of `area()`. This is why overridden methods are said to be resolved dynamically, at run time — it's the foundation that makes polymorphism useful (e.g., processing a list of different `Figure` subtypes uniformly, letting each one compute its own area correctly).

### Why Overridden Methods? (design justification, often an essay question)
Dynamic dispatch lets you define a **general interface** in the superclass (like `area()`), and let each subclass implement its own specific behavior. Code that works with the superclass type automatically works correctly with *any* subclass, without needing to know which one — this is the essence of extensible, maintainable OOP design.

## 8.9 Using Abstract Classes

Sometimes you want a superclass to define a common interface (method signature) for all of its subclasses, **without providing any meaningful implementation itself**, because the general case doesn't have one (e.g., a generic `Figure.area()` has no sensible default). Java handles this with **abstract classes and methods**.

```java
abstract class Figure {
    double dim1, dim2;
    Figure(double a, double b) { dim1 = a; dim2 = b; }

    abstract double area();     // abstract method — no body, just a signature
}

class Rectangle extends Figure {
    Rectangle(double a, double b) { super(a, b); }
    @Override
    double area() { return dim1 * dim2; }    // MUST be overridden — compile error otherwise
}
```

**Rules for `abstract`:**
- An `abstract` method has **no body** — only a declaration ending in `;`.
- Any class containing at least one abstract method **must itself** be declared `abstract`.
- You **cannot instantiate** an abstract class directly (`new Figure(...)` is a compile error) — it can only be used as a superclass reference type.
- Any concrete (non-abstract) subclass **must override and implement all** inherited abstract methods, or it too must be declared `abstract`.
- An abstract class **can still contain regular (non-abstract) methods and fields** — it's not purely a signature list (that's what an interface is for; see Part C).

## 8.10 Using `final` with Inheritance

The `final` keyword prevents further change in two inheritance-related ways:

### Preventing Overriding
```java
class A {
    final void show() {           // 'final' method — cannot be overridden by any subclass
        System.out.println("This is a final method.");
    }
}
class B extends A {
    // void show() { }   // ERROR — cannot override a final method
}
```

### Preventing Inheritance
```java
final class A {                   // 'final' class — cannot be subclassed at all
    // ...
}
// class B extends A { }   // ERROR — cannot extend a final class
```
Real-world example: Java's own `String` class is declared `final` specifically so no one can create a subclass that breaks its guaranteed immutability.

## 8.11 The `Object` Class

> `Object` is a special class defined in `java.lang` that is the **implicit superclass of every other class in Java** — every class you write, even if it doesn't explicitly `extends` anything, automatically inherits from `Object`.

Useful methods every Java object inherits from `Object` (know a few for exams):

| Method | Purpose |
|---|---|
| `boolean equals(Object obj)` | Compares this object to another for equality (default: reference comparison; commonly overridden). |
| `String toString()` | Returns a string representation of the object (default prints class name + hash code; commonly overridden). |
| `int hashCode()` | Returns a hash code, used by hash-based collections. |
| `Class getClass()` | Returns the runtime class of the object (used with reflection — Part C). |
| `void finalize()` | Called by the garbage collector before reclaiming the object (see 6.7). |

```java
class Point {
    int x, y;
    Point(int x, int y) { this.x = x; this.y = y; }

    @Override
    public String toString() {
        return "(" + x + ", " + y + ")";
    }
}
Point p = new Point(3, 4);
System.out.println(p);    // automatically calls p.toString() -> "(3, 4)"
```

---

# PART C — MODULE 2: FULL OOP SYLLABUS COVERAGE

*(These extend what you already learned in Part A. Each is presented in the same theory → definition → code format.)*

# C1. Java Methods (deeper) & Method Overloading

## Overloading Methods
> **Method overloading** lets two or more methods within the **same class** share the same name, as long as their **parameter lists differ** (in number, type, or order of parameters). Return type alone is NOT enough to distinguish overloaded methods.

```java
class OverloadDemo {
    void test() {
        System.out.println("No parameters");
    }
    void test(int a) {
        System.out.println("One int parameter: " + a);
    }
    void test(int a, int b) {
        System.out.println("Two int parameters: " + a + ", " + b);
    }
    double test(double a) {
        System.out.println("One double parameter: " + a);
        return a * a;
    }
}
class OverloadDemoMain {
    public static void main(String[] args) {
        OverloadDemo ob = new OverloadDemo();
        ob.test();
        ob.test(10);
        ob.test(10, 20);
        ob.test(2.5);          // calls the double version — Java resolves using best type match
    }
}
```
When there's no exact match, Java uses its automatic type conversion rules to find the closest matching overloaded version (e.g., an `int` argument can match a `double` parameter through automatic widening if no `int`-specific version exists).

### Overloading Constructors
Just like methods, constructors can be overloaded to give multiple ways to initialize an object:
```java
class Box {
    double width, height, depth;

    Box() { width = height = depth = 1; }                       // no-arg
    Box(double side) { width = height = depth = side; }          // cube
    Box(double w, double h, double d) { width=w; height=h; depth=d; } // full
}
```

## Using Objects as Parameters
Objects can be passed to methods just like primitive types:
```java
class Box {
    double width, height, depth;
    Box(double w, double h, double d) { width = w; height = h; depth = d; }

    boolean equalTo(Box ob) {         // takes another Box object as a parameter
        return this.width == ob.width && this.height == ob.height && this.depth == ob.depth;
    }
}
```

## A Closer Look at Argument Passing
Java uses **pass-by-value** for everything — but this is subtle for objects:
- **Primitive types** are passed by value — a *copy* of the value is passed; changes inside the method don't affect the caller's original variable.
- **Object references** are also passed by value — but the "value" being copied is the *reference (address)* itself. So the method receives a copy of the reference, which still points to the **same object**. This means the method **can** modify the object's fields (they're shared), but **cannot** make the caller's reference point to a different object.

```java
void modify(int x, Box b) {
    x = 100;              // does NOT affect caller's variable — primitive, pass-by-value
    b.width = 100;         // DOES affect caller's object — reference copy points to same object
    b = new Box(1,1,1);   // does NOT affect caller's reference — only the local copy changes
}
```

## Returning Objects
A method can return an object, just like it returns any other type:
```java
class Box {
    double side;
    Box(double s) { side = s; }
    Box incrementSide() {
        return new Box(side + 1);   // returns a brand-new Box object
    }
}
```

---

# C2. Recursion

> **Recursion** is the process of a method calling **itself**, directly or indirectly, to solve a problem by breaking it into smaller sub-problems of the same type. A recursive method must have a **base case** (a condition that stops the recursion) to avoid infinite recursion (which causes a `StackOverflowError`).

```java
class Recursion {
    // factorial: classic recursion example
    static int factR(int n) {
        if (n == 0) return 1;              // base case — stops recursion
        else return n * factR(n - 1);       // recursive case — calls itself with a smaller problem
    }

    public static void main(String[] args) {
        System.out.println("Factorial of 4 is " + factR(4));   // 24
    }
}
```
**Trace for `factR(4)`** (good to draw in exams):
```
factR(4) = 4 * factR(3)
         = 4 * (3 * factR(2))
         = 4 * (3 * (2 * factR(1)))
         = 4 * (3 * (2 * (1 * factR(0))))
         = 4 * (3 * (2 * (1 * 1)))
         = 24
```
Each recursive call is pushed onto the **call stack**; when the base case is hit, the calls "unwind" back up, computing the final result. Recursion is often a cleaner alternative to iteration for problems that are naturally self-similar (factorial, Fibonacci, tree traversal, Tower of Hanoi), though it can be less memory-efficient than a loop due to stack usage.

---

# C3. Exploring the String Class

Strings are sequences of characters, but in Java, `String` is a **class**, not a primitive — every string literal creates a `String` object.

## Key property: Immutability
> Once a `String` object is created, its contents can **never** be changed. Every "modifying" operation (like `concat`, `replace`, `toUpperCase`) actually returns a **brand-new** `String` object, leaving the original untouched.

```java
String s = "hello";
s.toUpperCase();               // does NOT change s — the returned new String is discarded here!
System.out.println(s);         // still prints "hello"

String upper = s.toUpperCase(); // correct way — capture the returned new object
System.out.println(upper);      // "HELLO"
```

## Commonly used String methods
```java
String s = "Java Programming";

System.out.println(s.length());              // 17
System.out.println(s.charAt(0));              // 'J'
System.out.println(s.substring(5));            // "Programming"
System.out.println(s.substring(0, 4));          // "Java"
System.out.println(s.indexOf("Pro"));           // 5
System.out.println(s.toUpperCase());            // "JAVA PROGRAMMING"
System.out.println(s.toLowerCase());            // "java programming"
System.out.println(s.replace('a', 'X'));         // "JXvX ProgrXmming"
System.out.println(s.trim());                    // removes leading/trailing whitespace
System.out.println(s.equals("Java Programming")); // true — content comparison
System.out.println(s.equalsIgnoreCase("JAVA PROGRAMMING")); // true
System.out.println(s.contains("Prog"));          // true
System.out.println(s.startsWith("Java"));        // true
System.out.println(s.endsWith("ing"));            // true
System.out.println(s.compareTo("Java"));          // > 0 (lexicographic comparison)
System.out.println("abc".concat("def"));          // "abcdef"

char[] chars = s.toCharArray();      // convert String -> char array
String fromChars = new String(chars); // convert char array -> String
```

## String concatenation with `+`
```java
String name = "John";
int age = 25;
String info = "Name: " + name + ", Age: " + age;   // "+" overloaded for String concatenation
```

## `StringBuffer` / `StringBuilder` — the mutable alternative
Because `String` is immutable, repeatedly modifying strings in a loop (e.g., building a long string) is inefficient (creates many throwaway objects). `StringBuffer` (thread-safe) and `StringBuilder` (faster, not thread-safe) provide a **mutable** sequence of characters instead.
```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");           // modifies the SAME object in place
sb.insert(5, ",");
sb.reverse();
System.out.println(sb.toString());
```

---

# C4. Java Access Modifiers & Encapsulation

## Access Modifiers (Module 1 & 2 explicit topic)

Java provides four levels of access control, applied to classes, fields, methods, and constructors:

| Modifier | Same class | Same package | Subclass (different package) | Different package (non-subclass) |
|---|:---:|:---:|:---:|:---:|
| `private` | ✅ | ❌ | ❌ | ❌ |
| *(default / package-private, no keyword)* | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

```java
class Account {
    private double balance;      // only accessible within Account itself
    protected String type;        // accessible within package + by subclasses elsewhere
    public String owner;          // accessible from anywhere
    String branch;                 // default/package-private — only within the same package
}
```
**Exam tip:** `private` is the strongest form of encapsulation (data hiding) — this is exactly the mechanism referenced in Topic 2.3's definition of Encapsulation.

## Encapsulation Recap with a Complete Example
```java
class Employee {
    private String name;
    private double salary;

    public Employee(String name, double salary) {
        this.name = name;
        setSalary(salary);              // validation goes through the setter
    }
    public String getName() { return name; }
    public double getSalary() { return salary; }
    public void setSalary(double salary) {
        if (salary >= 0) this.salary = salary;   // enforced rule — outside code can't bypass it
        else System.out.println("Invalid salary");
    }
}
```
This "private fields + public getters/setters" pattern **is** encapsulation in practice — the internal representation of `Employee` can even change later without breaking any code that uses `getSalary()`/`setSalary()`.

---

# C5. The `this` Keyword (deeper) and `final` Keyword (deeper)

## `this` — additional uses beyond field disambiguation (Topic 6.5)

### Invoking overloaded constructors via `this()`
A constructor can call **another constructor of the same class** using `this(...)`, avoiding duplicated initialization code:
```java
class Box {
    double width, height, depth;

    Box(double w, double h, double d) {
        width = w; height = h; depth = d;
    }
    Box(double side) {
        this(side, side, side);   // calls the 3-argument constructor above
    }
    Box() {
        this(1);                  // calls the 1-argument constructor above
    }
}
```
**Rule:** `this(...)`, like `super(...)`, must be the **first statement** in the constructor.

### Passing `this` as an argument
A method can pass a reference to its own current object using `this`, e.g., to register itself as a listener with another object.

## `final` Keyword — all three uses (frequently asked to "list all uses of final")

| Use | Meaning | Example |
|---|---|---|
| **`final` variable** | Creates a constant — value cannot be changed once assigned | `final double PI = 3.14159;` |
| **`final` method** | Cannot be overridden by any subclass (Topic 8.10) | `final void show() { ... }` |
| **`final` class** | Cannot be subclassed/extended at all (Topic 8.10) | `final class Utility { ... }` |

```java
final int MAX = 100;
// MAX = 200;   // ERROR — cannot reassign a final variable
```
A `final` field can also be assigned exactly once inside a constructor (a "blank final"), if not initialized at declaration.

---

# C6. `instanceof` Operator

> `instanceof` is a binary operator that tests whether an object is an instance of a specific class (or a class that implements a specific interface), returning a `boolean`. It's commonly used before downcasting, to make the cast safe.

```java
class Animal {}
class Dog extends Animal {}

Animal a = new Dog();
System.out.println(a instanceof Dog);      // true
System.out.println(a instanceof Animal);   // true — a Dog IS-AN Animal too
System.out.println(a instanceof String);   // compile error — unrelated types

if (a instanceof Dog) {
    Dog d = (Dog) a;    // safe downcast, protected by the instanceof check
}
```
Without the `instanceof` check first, an invalid cast (e.g., casting an `Animal` that's really a `Cat` into a `Dog`) throws a `ClassCastException` at run time.

---

# C7. Single Class, Nested Classes, Inner Classes, Static Nested Classes, Anonymous Classes

## Single (top-level) class
The ordinary kind of class you've been writing all along — declared directly inside a file, not inside another class.

## Nested Classes (general term)
> A **nested class** is any class defined **within** another class. Nested classes are divided into two categories: **static nested classes** and **non-static (inner) classes**.

### Static Nested Class
Declared `static` inside an outer class. It does **not** have access to the instance members of the outer class (only static members) — behaves almost like a regular top-level class, just namespaced inside the outer class.
```java
class Outer {
    static int outerStaticVar = 10;

    static class StaticNested {          // Java Static Class
        void display() {
            System.out.println("Outer static var: " + outerStaticVar);
        }
    }
}
// usage — no Outer instance needed:
Outer.StaticNested obj = new Outer.StaticNested();
obj.display();
```

### Inner Class (non-static nested class)
An inner class is tied to a **specific instance** of the outer class — it can freely access all of the outer class's instance fields and methods, even `private` ones.
```java
class Outer {
    int outerVar = 100;

    class Inner {                        // non-static inner class
        void show() {
            System.out.println("Outer var: " + outerVar);   // direct access to outer instance field
        }
    }
}
// usage — requires an Outer instance:
Outer outerObj = new Outer();
Outer.Inner innerObj = outerObj.new Inner();
innerObj.show();
```

## Anonymous Class
> An **anonymous class** is a class with **no name**, declared and instantiated in a single expression — typically used to override a method or implement an interface "on the fly" for one-time use.

```java
abstract class Greeting {
    abstract void greet();
}

class AnonymousDemo {
    public static void main(String[] args) {
        Greeting g = new Greeting() {         // anonymous subclass of Greeting, defined inline
            @Override
            void greet() {
                System.out.println("Hello from an anonymous class!");
            }
        };
        g.greet();
    }
}
```
Common real-world use (pre-lambda Java): implementing interfaces like `Runnable` or event listeners inline without creating a separate named class file.
```java
Runnable r = new Runnable() {
    @Override
    public void run() {
        System.out.println("Running in a thread via anonymous class");
    }
};
new Thread(r).start();
```

## Java Singleton (design pattern, not a language keyword)
> The **Singleton pattern** ensures a class has **only one instance** throughout the application, and provides a single global point of access to it. Achieved by: (1) making the constructor `private` (so no other class can call `new`), (2) keeping a `private static` reference to the one instance, and (3) exposing a `public static` method to get that instance.

```java
class Singleton {
    private static Singleton instance;     // holds the one and only instance
    private int counter = 0;

    private Singleton() {}                  // private constructor — blocks external 'new Singleton()'

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();     // create it only once, on first request
        }
        return instance;
    }

    public void increment() { counter++; }
    public int getCounter() { return counter; }
}

class SingletonDemo {
    public static void main(String[] args) {
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();
        s1.increment();
        System.out.println(s1 == s2);            // true — both refer to the exact same object
        System.out.println(s2.getCounter());       // 1 — s2 sees s1's change, because it's the same object
    }
}
```
Typical use cases: configuration managers, logging classes, connection pools — anywhere you need exactly one shared instance.

---

# C8. `enum` — Enumerations in Java

> An **enum** is a special Java type used to define a collection of **named constants**. It is declared using the `enum` keyword and is internally implemented as a class (each enum type implicitly extends `java.lang.Enum`).

## Basic enum
```java
enum Day { MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY }

class EnumDemo {
    public static void main(String[] args) {
        Day today = Day.WEDNESDAY;

        switch (today) {
            case MONDAY:
                System.out.println("Start of the work week");
                break;
            case WEDNESDAY:
                System.out.println("Midweek");
                break;
            default:
                System.out.println("Some other day");
        }
    }
}
```

## `values()` and `valueOf()` — auto-generated by the compiler for every enum
```java
for (Day d : Day.values()) {           // values() returns an array of all constants, in order
    System.out.println(d + " has ordinal " + d.ordinal());
}
Day d = Day.valueOf("FRIDAY");         // converts a String -> the matching enum constant
```

## Java Enumerations Are Class Types / Inherit `Enum`
Because an enum is a real class type, it can have its own **constructors, fields, and methods** — this is a step beyond simple C-style enums.

### enum Constructor + enum with fields (Module 2 explicit topics)
```java
enum Planet {
    MERCURY(3.303e+23, 2.4397e6),
    VENUS(4.869e+24, 6.0518e6),
    EARTH(5.976e+24, 6.37814e6);

    private final double mass;    // in kilograms
    private final double radius;  // in meters

    Planet(double mass, double radius) {    // enum constructor — always implicitly private
        this.mass = mass;
        this.radius = radius;
    }

    double surfaceGravity() {
        final double G = 6.67300E-11;
        return G * mass / (radius * radius);
    }
}

class PlanetDemo {
    public static void main(String[] args) {
        for (Planet p : Planet.values()) {
            System.out.printf("Gravity on %s is %.2f%n", p, p.surfaceGravity());
        }
    }
}
```
**Rule:** enum constructors are **always implicitly `private`** (or package-private) — you can never call `new Planet(...)` from outside; the constants listed at the top of the enum are the *only* instances that will ever exist.

### enum toString / "enum String"
Every enum constant has a default `toString()` that returns its name (e.g., `"MONDAY"`), but like any method, it **can be overridden** per-constant or for the whole enum:
```java
enum Size {
    SMALL("S"), MEDIUM("M"), LARGE("L");

    private final String code;
    Size(String code) { this.code = code; }

    @Override
    public String toString() { return code; }   // overriding enum's String representation
}
System.out.println(Size.MEDIUM);   // prints "M" instead of "MEDIUM"
```

---

# C9. Interfaces

## Definition
> An **interface** is a completely abstract type — a reference type in Java, declared with the `interface` keyword, that specifies a set of method signatures (a "contract") that any implementing class **must** provide the actual implementation for. Interfaces can also contain constant (`public static final`) fields.

Interfaces solve the problem that Java classes can't have multiple inheritance — **a class can implement multiple interfaces**, even though it can extend only one class.

## Defining and implementing an interface
```java
interface Shape {
    double PI = 3.14159;              // implicitly public static final (a constant)

    double area();                     // implicitly public abstract — no body
    double perimeter();                // implicitly public abstract
}

class Circle implements Shape {
    double radius;
    Circle(double r) { radius = r; }

    @Override
    public double area() { return PI * radius * radius; }
    @Override
    public double perimeter() { return 2 * PI * radius; }
}

class Square implements Shape {
    double side;
    Square(double s) { side = s; }

    @Override
    public double area() { return side * side; }
    @Override
    public double perimeter() { return 4 * side; }
}
```

## Applying Interfaces — polymorphism through interfaces
```java
class InterfaceDemo {
    public static void main(String[] args) {
        Shape[] shapes = { new Circle(5), new Square(4) };
        for (Shape s : shapes) {
            System.out.println("Area: " + s.area());     // dynamic dispatch works via interfaces too
        }
    }
}
```

## Rules to remember
- All methods in a traditional interface are implicitly `public abstract` (unless marked `default` or `static`, a later Java feature beyond this textbook).
- All fields in an interface are implicitly `public static final` — i.e., constants.
- A class uses `implements` (not `extends`) to use an interface, and **must implement every method**, or the class itself must be declared `abstract`.
- **A class can implement multiple interfaces**, separated by commas: `class MyClass implements InterfaceA, InterfaceB { ... }` — this is how Java achieves the *effect* of multiple inheritance safely.
- **Interfaces can extend other interfaces** (using `extends`, and even multiple interfaces at once), inheriting all their abstract methods.

## Interface vs. Abstract Class (a favorite comparison question)

| | Abstract Class | Interface |
|---|---|---|
| Keyword | `abstract class` | `interface` |
| Methods | Can have both abstract AND fully implemented (concrete) methods | Traditionally, all methods abstract (no body) |
| Fields | Can have any kind of field (instance variables, any modifier) | Only `public static final` constants |
| Inheritance | A class can extend only **one** abstract class | A class can implement **many** interfaces |
| Constructors | Can have constructors | Cannot have constructors |
| Use case | "IS-A" relationship with shared partial implementation | A "CAN-DO" capability/contract, possibly across unrelated classes |

---

# C10. Polymorphism — Full Picture (Overloading + Overriding, tied together)

You've already seen both halves in detail (C1 and Topic 8.7–8.8); here they are side by side as the exam usually wants them:

> **Polymorphism** means "many forms" — the ability of a single interface (method name) to represent different underlying implementations. Java supports two kinds:

1. **Compile-time Polymorphism (Static Binding) — Method Overloading**
   - Same method name, different parameter lists, within the same class.
   - The compiler decides which version to call based on the argument types, **at compile time**.
2. **Run-time Polymorphism (Dynamic Binding) — Method Overriding**
   - Subclass redefines a superclass method with an identical signature.
   - The JVM decides which version to call based on the **actual object type**, **at run time** (dynamic method dispatch, Topic 8.8).

```java
class Calculator {
    // Compile-time polymorphism (overloading)
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}

class Shape {
    // Run-time polymorphism (overriding) -- see Topic 8.8's FindAreas example for the full pattern
    void draw() { System.out.println("Drawing a generic shape"); }
}
class Circle extends Shape {
    @Override
    void draw() { System.out.println("Drawing a circle"); }
}
```

---

# C11. Reflection (`java.lang.reflect`)

> **Reflection** is the ability of a Java program to **examine or introspect upon itself at run time** — inspecting classes, interfaces, fields, and methods dynamically, without knowing their names at compile time. It's the mechanism behind many frameworks (e.g., for reading annotations, building ORMs, or dependency injection).

Every object has a `getClass()` method (inherited from `Object`, Topic 8.11) that returns a `Class` object — the entry point into reflection.

```java
import java.lang.reflect.*;

class Sample {
    private int x = 10;
    public void greet() { System.out.println("Hello from Sample"); }
}

class ReflectionDemo {
    public static void main(String[] args) throws Exception {
        Sample obj = new Sample();
        Class<?> cls = obj.getClass();                 // step 1: get the Class object

        System.out.println("Class name: " + cls.getName());

        Method[] methods = cls.getDeclaredMethods();     // list all methods
        for (Method m : methods) {
            System.out.println("Method: " + m.getName());
        }

        Field[] fields = cls.getDeclaredFields();         // list all fields, even private ones
        for (Field f : fields) {
            System.out.println("Field: " + f.getName());
        }

        // Invoking a method dynamically by name:
        Method greetMethod = cls.getMethod("greet");
        greetMethod.invoke(obj);          // calls obj.greet() dynamically, without writing obj.greet() directly
    }
}
```
**Key classes in `java.lang.reflect`:** `Class`, `Method`, `Field`, `Constructor`. **Exam-safe definition to memorize:** *"Reflection allows a running Java program to inspect and manipulate the fields, methods, and constructors of classes at run time, even ones it did not know about at compile time."* Trade-off worth mentioning: reflection is powerful but slower than direct code and can break encapsulation (it can even access `private` members using `setAccessible(true)`), so it should be used sparingly.

---

# Quick Revision Cheat-Sheet

| Concept | One-line definition |
|---|---|
| Bytecode | CPU-independent intermediate code produced by `javac`, run by the JVM |
| JVM / JRE / JDK | Runs bytecode / JVM + libraries to run programs / JRE + tools to develop programs |
| Encapsulation | Binding data + code together, hiding data via `private` + accessors |
| Inheritance | Subclass acquires superclass members via `extends` |
| Polymorphism | One interface, many implementations — overloading (compile-time) & overriding (run-time) |
| Abstraction | Exposing essential features, hiding implementation detail |
| Constructor | Special method, same name as class, no return type, runs on object creation |
| `this` | Refers to the current object |
| `super` | Refers to the immediate superclass — calls its constructor or accesses its hidden members |
| Method Overloading | Same name, different parameters, same class, compile-time resolved |
| Method Overriding | Same signature, subclass redefines superclass method, run-time resolved |
| Abstract class | Cannot be instantiated; may mix abstract + concrete methods |
| Interface | Pure contract; class can implement many; achieves multiple-inheritance-like behavior |
| `final` | Constant variable / non-overridable method / non-extendable class |
| Garbage Collection | Automatic reclaiming of memory for unreferenced objects |
| `instanceof` | Tests whether an object belongs to a given class/type |
| Enum | Type-safe set of named constants; can have fields, constructors, methods |
| Singleton | Design pattern ensuring only one instance of a class ever exists |
| Reflection | Inspecting/manipulating classes, methods, fields at run time |

---

**Good luck on your exam.** If you want, next steps could be: a set of practice MCQs/short-answer questions per topic, or flashcards for the definitions above — just ask.
