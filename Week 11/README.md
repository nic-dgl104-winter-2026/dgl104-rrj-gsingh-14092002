# DGL 104 – Research and Reflection Journal
 
**Course:** DGL 104 – Application Development Foundations  
**Student:** Gagandeep singh  
**Semester:** Winter 2026  
 
---

 
## Week 11 – Mar. 17
 
### Overview
 
Week 11 introduced **Object-Oriented Programming (OOP)**, one of the most widely used and important programming paradigms in modern software development. According to the course lecture, OOP is an approach to program organization and development that attempts to eliminate the pitfalls of conventional programming by incorporating the best features of structured programming along with several powerful new concepts (Sarkar, 2026). This week had two main activities: reading and summarizing the OOP documentation, and reflecting on how JavaScript — the language I have been working with throughout this course — supports OOP principles.
 
---
 
### Activity 1: Read the OOP Documentation – Summary and Application
 
#### From Procedural to Object-Oriented Programming
 
Before OOP, the dominant approach was **procedure-oriented programming** — writing lists of instructions organized into functions, where most data was shared globally across the program. The lecture notes explain that this approach emphasized doing things (algorithms) over managing data, and used a top-down design approach (Sarkar, 2026). The major problem with this approach is that global data is vulnerable to accidental changes, and in large programs it becomes very difficult to track which function is accessing which data. Functions also do not naturally model real-world entities, which made complex systems harder to reason about.
 
OOP was developed to address these limitations. Instead of thinking about a program as a sequence of steps, OOP thinks about it as a collection of **objects** — each containing its own data and the functions that operate on that data. This is a bottom-up approach, and it much more naturally reflects the way we think about real-world problems (Sarkar, 2026).
 
---
 
#### The Four Core Principles of OOP
 
The lecture covers four main OOP principles that I studied in detail this week.
 
---
 
##### 1. Encapsulation
 
Encapsulation is the wrapping of data and functions into a single unit called a **class**. The data inside a class is hidden from the outside world and can only be accessed through controlled methods. This is also called **data hiding** (Sarkar, 2026).
 
**Why it matters:**  
In procedural programming, global data could be accidentally changed by any function. Encapsulation prevents this by restricting direct access. Only the methods defined inside the class can modify the data.
 
**Real-World Example:**  
A `BankAccount` class is a perfect example. The `balance` field is private — no outside code can directly change it. The only way to modify it is through the `deposit()` or `withdraw()` methods, which include validation logic. This protects the integrity of the data.
 
**How I would apply this in JavaScript:**  
JavaScript supports encapsulation through classes and, more recently, through private fields using the `#` syntax. For a coding project, I could create a `UserProfile` class where sensitive data like password hashes are private and can only be accessed through specific getter methods.
 
---
 
##### 2. Abstraction
 
Abstraction means representing essential features of an object without exposing the internal implementation details. According to the lecture, classes use abstraction and are defined as a list of abstract attributes and functions — this is why classes are sometimes called **Abstract Data Types (ADT)** (Sarkar, 2026).
 
**Why it matters:**  
Abstraction lets a user interact with an object without needing to understand how it works internally. Just as a driver does not need to understand how a car engine works to drive a car, a developer using a class does not need to know how every method is implemented.
 
**Real-World Example:**  
An abstract `Animal` class defines a `makeSound()` method. The `Dog` and `Cat` subclasses each implement `makeSound()` differently. The user of these classes only needs to know that every Animal can make a sound — not how it does so.
 
**How I would apply this in JavaScript:**  
In a p5.js sketch, I could create an abstract `Shape` class with a `draw()` method. Different shape classes like `Circle`, `Rectangle`, and `Triangle` would each implement `draw()` in their own way, but the code that calls them would just say `shape.draw()` without needing to know which type it is.
 
---
 
##### 3. Inheritance
 
Inheritance is the process by which one class acquires the properties and methods of another class. The class being inherited from is the **parent (base) class**, and the class that inherits is the **child (derived) class**. The lecture describes inheritance as providing the idea of **"reusability"** — we can add new features to an existing class without modifying it (Sarkar, 2026).
 
**Why it matters:**  
Without inheritance, developers would have to copy and paste code between similar classes. With inheritance, shared behaviour lives in one place and is automatically available to all subclasses. This makes code easier to maintain and extend.
 
**Two Strategies of Inheritance:**
- **Extension** — Adds new features to an existing class (e.g., a `Student` class that extends a `Person` class by adding `studentId`)
- **Specialization** — Refines the behaviour of a general class for a specific use case (e.g., a `PremiumUser` that extends `User` with additional permissions)
 
**Real-World Example:**  
A `Vehicle` base class has a `honk()` method and a `brand` property. A `Car` class inherits from `Vehicle` and adds its own `model` property — without rewriting the `honk()` method.
 
**How I would apply this in JavaScript:**  
In the Application Development Coding project, I could use inheritance to build a base `Sketch` class in p5.js that handles setup and draw loop logic, and then extend it with specific sketch types like `InteractiveSketch` or `AnimatedSketch` that add their own unique behaviour.
 
---
 
##### 4. Polymorphism
 
Polymorphism means the ability to take more than one form. A single interface or method name can behave differently depending on the object it is called on. The lecture notes give a useful example: the `+` operator adds two numbers together, but when applied to strings it concatenates them — same interface, different behaviour depending on the data type (Sarkar, 2026).
 
Polymorphism is closely connected to **Dynamic Binding** — the idea that the specific code to be executed is not determined until runtime. This means that calling `shape.draw()` on a list of different shape objects will call the correct version of `draw()` for each one automatically, based on the actual type of the object at that moment.
 
**Why it matters:**  
Polymorphism allows a program to work with objects of different types through a single interface. This makes code much more flexible and reduces the need for large `if/else` chains to check what type of object you are working with.
 
**Real-World Example:**  
A `Shape` class has a `draw()` method. `Circle`, `Box`, and `Triangle` each override this method with their own implementation. When you call `draw()` on any shape object, the correct version is automatically used — this is polymorphism in action.
 
**How I would apply this in JavaScript:**  
In a p5.js coding project, I could define a base `Particle` class and create subclasses like `FireParticle`, `WaterParticle`, and `StarParticle`, each with their own `update()` and `render()` implementations. The main draw loop would call `particle.render()` for every particle without knowing what type it is, and each one would draw itself correctly.
 
---
 
#### OOP in JavaScript – Language Paradigm Assessment
 
The follow-up question for this week asked whether my chosen language supports OOP and to what extent. Since I have been working with JavaScript throughout this course, I researched this question carefully.
 
**Does JavaScript fully support OOP?**  
JavaScript is a **multi-paradigm language** — it supports OOP, but not in the same way as a purely OOP language like Java. JavaScript's OOP is **prototype-based** rather than class-based, meaning objects can inherit directly from other objects without requiring a formal class hierarchy. However, since ES6 (2015), JavaScript introduced the `class` keyword, which provides a cleaner, more familiar syntax for OOP that looks similar to Java or C# (MDN Web Docs, 2025).
 
**OOP Support in JavaScript:**
 
| OOP Principle | JavaScript Support |
|---|---|
| Encapsulation | ✅ Supported — via classes and private fields (`#fieldName`) |
| Abstraction | ✅ Partially supported — no formal `abstract` keyword, but can be simulated |
| Inheritance | ✅ Fully supported — via `extends` and `super` keywords |
| Polymorphism | ✅ Supported — via method overriding in subclasses |
 
**Other Paradigms JavaScript Supports:**  
JavaScript is genuinely multi-paradigmatic. In addition to OOP, it also supports:
- **Functional programming** — Functions are first-class values, and JavaScript has built-in methods like `map()`, `filter()`, and `reduce()` that follow a functional style. This will be explored in Week 12.
- **Procedural programming** — Simple scripts can be written as a sequence of instructions without any classes or objects.
- **Event-driven programming** — Especially in browser environments, JavaScript is built around responding to events.
 
**Reflection:**  
Learning about OOP this week changed how I think about the JavaScript I have already written. Every time I have used `class` in JavaScript, I was using OOP — but I did not always think about *why* those principles exist. Now understanding encapsulation, abstraction, inheritance, and polymorphism from first principles, I can make more deliberate design decisions. The comparison between procedure-oriented and object-oriented programming in the lecture was particularly helpful — it showed clearly that OOP was not invented to be complicated, but to solve real problems that came up as programs grew larger. The idea that data should be protected and tied closely to the functions that operate on it makes complete sense when you see what happens in large procedural programs where global data gets corrupted unexpectedly.
 
---
 
### Activity 2: Connect with External Community – p5.js
 
This week I continued to follow the p5.js community. I spent some time on the [Processing Foundation Discourse forum](https://discourse.processing.org) reading through posts from other contributors and users. I did not post anything myself yet, but I found it helpful to observe how the community communicates. Most questions receive thoughtful responses within a day or two, and the tone is consistently welcoming and supportive. Seeing how maintainers respond to beginner questions made me more confident that when I am ready to engage directly, it will be a positive experience.
 
---
 
### Weekly Reflection
 
Week 11 was one of the most content-rich weeks in terms of theoretical depth. OOP is not a new topic for me — I have used classes and objects in JavaScript before — but studying it this formally, through the lens of the course lecture and the PDF notes, gave me a much stronger foundation. Understanding *why* OOP was invented, and what problems it was designed to solve compared to procedural programming, makes me appreciate it in a new way. The four principles — encapsulation, abstraction, inheritance, and polymorphism — are not just features of a language; they are a philosophy for organizing programs in a way that mirrors how we think about the real world. I also appreciated learning that JavaScript is genuinely multi-paradigmatic, because it means the functional programming concepts coming in Week 12 are not a departure from what I have been doing — they are another layer of the same language. I spent approximately **3 hours** this week on reading, research, and writing.
 
> **Code Reference:** See [`contributions.md`](./contributions.md) – Week 11 JavaScript OOP snippets demonstrating all four principles: encapsulation, abstraction, inheritance, and polymorphism.
 
---
 
## Bibliography
 
- DGL 104 Course Notes. (2025). *Week 8: Functional user requirements and user stories*. North Island College.
- DGL 104 Course Notes. (2025). *Week 9: Design patterns*. North Island College.
- DGL 104 Course Notes. (2025). *Week 10: MV\* patterns*. North Island College.
- GitHub Open Source Guides. (2025). *How to contribute to open source*. https://opensource.guide/how-to-contribute/
- MDN Web Docs. (2025). *Object-oriented programming*. https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object-oriented_programming
- p5.js. (2025). *Contributing to p5.js*. https://github.com/processing/p5.js/blob/main/CONTRIBUTING.md
- Processing Foundation. (2025). *Processing*. https://processing.org
- Refactoring Guru. (2025). *Design patterns*. https://refactoring.guru/design-patterns
- Sarkar, D. P. (2026). *Week 11 – Object oriented programming* [Lecture notes]. DGL 104, North Island College.
- Shiffman, D. (2025). *The Coding Train*. https://www.youtube.com/c/TheCodingTrain
 