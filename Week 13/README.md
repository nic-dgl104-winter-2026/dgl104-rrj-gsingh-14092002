# DGL 104 – Research and Reflection Journal
 
**Course:** DGL 104 – Application Development Foundations  
**Student:** Gagandeep singh  
**Semester:** Winter 2026  
  
---

## Week 13 – Mar. 30 – Final Reflection
 
### Overview
 
This is the final week of DGL 104 and the last entry in this Research and Reflection Journal. Looking back at everything covered from Week 8 through Week 12, this week gave me the opportunity to step back and appreciate something important — almost every concept I studied in the classroom, I ended up using in real life through the **Task Management System (TMS)** project. That connection between theory and practice is what made this second half of the semester feel genuinely meaningful to me.
 
---
 
### From Theory to Practice — What I Learned and What I Built
 
When I started Week 8, I was learning about user stories, functional requirements, and exploring GitHub repositories for the first time. At that point, the project felt distant and abstract. I did not fully understand why we were studying design patterns, architectural patterns, OOP, and functional programming — they each felt like separate topics. But as the semester progressed and the project took shape, I realized that every single concept from the course lectures ended up directly inside the code I wrote.
 
Here is what that journey looked like for me.
 
---
 
#### Week 8 – User Stories and GitHub → Project Planning
 
In Week 8 I learned how to write user stories and functional requirements. At the time it felt like a writing exercise. But when it came to planning the Task Management System, I found myself thinking in exactly those terms. Features like *"As a Manager, I can assign a task to a Developer so that work is distributed correctly"* or *"As an Admin, I can delete any task so that outdated work is removed"* — these were the exact kinds of user stories that shaped what the application needed to do. Without that Week 8 foundation, I would have started coding without a clear picture of what I was building or for whom.
 
Exploring GitHub in Week 8 also paid off directly. By the time I was setting up the project repository, I already understood how to structure a `README.md`, why a `CONTRIBUTING.md` matters, and how to use branches and pull requests properly — all habits I built from exploring open source projects early in the semester.
 
---
 
#### Week 9 – Design Patterns → Four Patterns in the Project
 
Week 9 was the week that connected most directly to the project. I studied four design patterns — **Factory Method**, **Adapter**, **Observer**, and **Singleton** — and I remember thinking they were interesting but wondering when I would actually use them. The answer turned out to be: immediately.
 
The Task Management System implements four design patterns:
 
- **Singleton Pattern** (`backend/db/database.js`) — I used this to ensure only one database connection is ever created and shared across the entire application. Before learning about this pattern, I might have created a new database connection in every file that needed it. Understanding the Singleton showed me why that is a problem and gave me a clean, professional solution.
 
- **Factory Pattern** (`backend/patterns/factory.js`) — I used this to create user objects with different permissions based on their role. Instead of scattering `if/else` role checks throughout the codebase, the Factory centralizes that logic in one place. This came directly from the Week 9 lecture on how Factory Method removes hardcoded object creation from the main program logic.
 
- **Observer Pattern** (`backend/patterns/observer.js`) — I used this to build the real-time notification system. Whenever a task is created, updated, or deleted, all subscribers are automatically notified. This is exactly the subscription mechanism described in Week 9 — the task management code does not need to know who is listening, it just emits an event and the Observer handles the rest.
 
- **Strategy Pattern** (`backend/patterns/strategy.js`) — I used this to allow tasks to be sorted by priority, due date, or status without changing the core code. The sorting algorithm can be swapped at any time by passing a different strategy function. This was inspired by the Week 9 lesson on keeping algorithms isolated, testable, and easy to extend.
 
Seeing all four patterns working inside a real application made them feel permanent in my understanding. Before the project, I knew the theory. After the project, I know when and why to use each one.
 
---
 
#### Week 10 – MV\* Patterns and Open Source → Architecture and Contribution Mindset
 
Week 10 introduced MVC, MVVM, and MVP architectural patterns, and also pushed me to seriously engage with open source communities. Both of these shaped the project in different ways.
 
The Task Management System follows a **MVC-inspired architecture**. The frontend HTML and JavaScript files act as the **View**, the Express.js route handlers act as the **Controller**, and the SQLite database layer acts as the **Model**. When I was structuring the project folders, I made deliberate decisions about what logic belonged where — business logic in the routes, data management in the database layer, and display logic in the frontend. That clean separation came directly from understanding MVC.
 
The open source work in Week 10 also shaped how I approached the project. I followed the same contribution practices I had studied — meaningful commit messages, working on separate branches, and treating the `README.md` as important documentation rather than an afterthought. Even though this was a solo project, I practiced it as if it were an open source repository, because I learned from Week 10 that good habits matter regardless of the audience.
 
---
 
#### Week 11 – OOP → Classes, Roles, and Data Hiding
 
Week 11 covered Object-Oriented Programming in depth — encapsulation, abstraction, inheritance, and polymorphism. The Task Management System uses OOP throughout the backend.
 
The **role-based access system** is a direct application of OOP principles. Each user has a role — Admin, Manager, Developer, or Tester — and the Factory pattern creates user objects with the appropriate permissions. The `balance` field in the Week 11 `BankAccount` encapsulation example directly inspired how I thought about protecting user permission data — it should not be freely accessible or modifiable from anywhere in the code.
 
**Encapsulation** is present in how the database connection is handled through the Singleton class — outside code gets access to the connection through a controlled method, not directly. **Abstraction** is present in how the route handlers interact with the database — they call methods without needing to know the details of the SQL queries underneath.
 
Understanding OOP formally also helped me write cleaner JavaScript classes throughout the project, because I was no longer just writing syntax — I understood the principles behind what I was doing.
 
---
 
#### Week 12 – Functional Programming → Cleaner JavaScript Throughout
 
Week 12 introduced functional programming, and while the Task Management System is not a purely functional application, FP principles influenced the way I wrote JavaScript throughout the frontend and backend.
 
Instead of writing `for` loops to process task data, I used `filter`, `map`, and `reduce` pipelines. For example, when preparing the data for the **live pie chart on the dashboard**, I used a `reduce` call to count tasks by status — a clean, single-expression computation instead of a loop with a counter variable. When filtering tasks on the Kanban board by column, I used `filter` rather than a loop with `if` statements inside.
 
The **Strategy pattern's sort functions** are themselves pure functions — they take two values and return a comparison result without touching any external state. This is functional programming applied inside an OOP design pattern, which is exactly what Week 12 taught: you do not have to choose between paradigms. You use the right tool for the right situation.
 
The **Redux reducer model** discussed in the Week 12 lecture also influenced how I structured state updates in the frontend. Rather than mutating task arrays directly, I used the spread operator to create new arrays — keeping the state predictable and making the UI easier to reason about.
 
---
 
### What i learned while i was working on my project
 
The lectures gave me the vocabulary, the frameworks, and the mental models. The project gave me the experience of applying all of them under real constraints — a real deadline, a real database, a real deployed URL that anyone can visit.
 
There were moments in the project where things did not work the way I expected. Setting up JWT authentication took longer than planned. The Singleton pattern felt theoretical until I saw what happened without it — two modules importing the database separately and creating conflicting connections. The Observer pattern clicked the moment I saw a task update trigger a notification log automatically, without the task route knowing anything about notifications.
 
These are the kinds of lessons that do not come from reading or writing about concepts — they come from building something real and running into real problems. Every bug I fixed and every design decision I made was shaped by something I had studied in the course.
 
---
 
### Final Thoughts
 
Looking at this journal from Week 8 to Week 13, I can see a clear progression. I started by learning how to think about users, then how to structure solutions with design patterns, then how to organize entire applications with architectural patterns, then how to model real-world entities with OOP, and finally how to write cleaner, more expressive code with functional programming. Each week built on the last.
 
The Task Management System is the place where all of those threads came together. It has user stories built into its features, design patterns in its architecture, MVC in its structure, OOP in its classes, and functional programming in its data processing. It is not a perfect application — there are things I would do differently now — but it is a genuine demonstration of what I learned in DGL 104.
 
I am walking away from this course with a vocabulary, a set of tools, and most importantly a way of thinking about software that I did not have before. That feels like the real outcome of this semester.
 
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
- Reselman, B. (2024). *Understanding the 7 principles of functional programming*. TheServerSide. https://www.theserverside.com/tip/Understanding-the-7-principles-of-functional-programming
- Sarkar, D. P. (2026). *Week 11 – Object oriented programming* [Lecture notes]. DGL 104, North Island College.
- Sarkar, D. P. (2026). *Week 12 – Functional programming* [Lecture slides]. DGL 104, North Island College.
- Shiffman, D. (2025). *The Coding Train*. https://www.youtube.com/c/TheCodingTrain
 
