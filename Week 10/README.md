# DGL 104 – Research and Reflection Journal
 
**Course:** DGL 104 – Application Development Foundations  
**Student:** Gagandeep singh 
**Semester:** Winter 2026 
 
---

 
## Week 10 – Mar. 11
 
### Overview
 
Week 10 introduced **MV\* architectural patterns**, which are a step above the design patterns studied in Week 9. While design patterns like Singleton or Observer solve specific, well-defined coding problems, MV\* patterns define the overall structure of an entire application (DGL 104 Course Notes, Week 10, 2025). This week also marked a turning point for the Community Code project — it was time to stop researching and start contributing. The three main activities this week were: understanding MV\* patterns from the lecture, assessing the contribution guidelines for the chosen open source project (p5.js), and beginning actual contribution work.
 
---
 
### Activity 1: MV\* Patterns – MVC, MVVM, and MVP
 
MV\* stands for **Model View \*** where the asterisk represents a third component that varies depending on the specific pattern. All MV\* patterns share the same goal: to **separate the data (Model) from the user interface (View)**, making applications easier to develop, test, and maintain. The difference between the patterns lies in how the third component manages the communication between the Model and the View.
 
---
 
#### MVC – Model View Controller
 
**MVC** is one of the oldest and most widely used architectural patterns. It divides an application into three components:
 
| Component | Responsibility |
|---|---|
| **Model** | Manages data, business logic, and rules |
| **View** | Displays data to the user (UI) |
| **Controller** | Handles user input and updates the Model and View |
 
**How it works:**  
The user interacts with the **View**, which sends input to the **Controller**. The Controller processes the input, updates the **Model**, and then refreshes the View with new data. The Controller sits in the middle and manages the flow of information.
 
**Real-World Example:**  
Ruby on Rails is a classic MVC framework used for web development. In a blog application built with Rails, the `Post` model manages database records, the `posts/index.html.erb` view displays them, and the `PostsController` handles requests like creating or deleting a post.
 
**Reflection:**  
MVC makes sense for web applications because the separation between what the user sees and the underlying data is very clear. However, as applications grow larger, Controllers can become very large and difficult to manage — a problem sometimes called "Massive View Controller" in iOS development.
 
---
 
#### MVVM – Model View ViewModel
 
**MVVM** was developed to address some of the limitations of MVC, particularly in modern declarative UI frameworks. It replaces the Controller with a **ViewModel**.
 
| Component | Responsibility |
|---|---|
| **Model** | Manages data and business logic |
| **View** | Displays UI and binds to ViewModel properties |
| **ViewModel** | Exposes data from the Model to the View via data binding |
 
**How it works:**  
In MVVM, the View and ViewModel are connected through **data binding** — when the ViewModel's data changes, the View updates automatically, and vice versa. This removes the need for the View to manually call the Controller to request updates.
 
**Real-World Example:**  
Both **SwiftUI** (iOS) and **Jetpack Compose** (Android) use the MVVM pattern. In a SwiftUI app, a `@StateObject` or `@ObservedObject` is the ViewModel, and the SwiftUI view automatically re-renders whenever the ViewModel's published properties change.
 
**Reflection:**  
MVVM is particularly powerful in reactive frameworks because the two-way data binding reduces the amount of boilerplate code needed to keep the UI in sync with data. This connects back to the **Observer pattern** from Week 9 — data binding is essentially the Observer pattern built into the architecture.
 
---
 
#### MVP – Model View Presenter
 
**MVP** is similar to MVC but replaces the Controller with a **Presenter**, and the View becomes more passive.
 
| Component | Responsibility |
|---|---|
| **Model** | Manages data and business logic |
| **View** | Displays UI, delegates all logic to Presenter |
| **Presenter** | Retrieves data from Model, formats it, and updates the View |
 
**How it works:**  
In MVP, the View does almost nothing on its own — it passes all user interactions to the **Presenter**, which handles the logic and tells the View exactly what to display. The View and Model never communicate directly.
 
**Real-World Example:**  
MVP was commonly used in older Android development before Jetpack Compose. The Activity or Fragment acted as the View, passing all user events to a Presenter class that managed the logic.
 
**Reflection:**  
MVP makes the View completely passive, which makes it much easier to unit test the Presenter without needing an actual UI. This was a key improvement over MVC in mobile development. However, the strict separation can lead to a lot of boilerplate interfaces and classes, which is why MVVM has largely replaced MVP in modern Android development.
 
---
 
#### Summary Comparison
 
| Pattern | Third Component | Communication | Best Used In |
|---|---|---|---|
| MVC | Controller | Controller mediates between Model and View | Web apps (Rails, Django) |
| MVVM | ViewModel | Data binding between View and ViewModel | Mobile apps (SwiftUI, Jetpack Compose) |
| MVP | Presenter | Presenter controls View entirely | Older Android, testable UIs |
 
---
 
### Activity 2: Assess External Community Contribution Guidelines – p5.js
 
Following up from Week 9, I chose **p5.js** ([https://github.com/processing/p5.js](https://github.com/processing/p5.js)) as the external open source project to contribute to. This decision made sense because p5.js is a JavaScript library built on the Processing philosophy — directly connected to the language I researched in Week 8. This week I carefully assessed its contribution documentation.
 
**Documents Reviewed:**
 
| Document | Location | What It Covers |
|---|---|---|
| `README.md` | Root of repository | Overview, installation, quick start |
| `CONTRIBUTING.md` | Root of repository | Full contribution workflow, coding standards, PR process |
| `CODE_OF_CONDUCT.md` | Root of repository | Community behaviour expectations |
| Contributor Docs | [https://p5js.org/contributor-docs](https://p5js.org/contributor-docs) | In-depth guides for contributors |
 
**Key Contribution Requirements I Identified:**
 
- **Fork and branch** — Contributors must fork the repository and create a new branch for each contribution. Working directly on `main` is not allowed.
- **Steward system** — p5.js uses a steward model where specific maintainers are responsible for different areas of the codebase. Pull requests should tag the appropriate steward for review.
- **Unit tests required** — Any code contribution must include unit tests. The project uses a test suite and contributions without tests will not be merged.
- **Issue-first approach** — For any significant change, an issue should be opened and discussed before writing code, to avoid duplicate or unwanted work.
- **Code style** — The project follows specific ESLint rules for code formatting. Running `npm test` before submitting is required.
 
**Reflection:**  
Reading p5.js's contribution documentation was detailed but well worth it. The steward system was something I had not seen before — it is a smart way to manage a large repository where different people have expertise in different areas. The requirement for unit tests with every code contribution raised the bar, but also confirmed that p5.js takes code quality seriously, which means contributing here will genuinely teach me good practices. I also noted that documentation and example contributions do not require unit tests, which gives me a realistic entry point as a first-time contributor. This is consistent with what the "How to Contribute to Open Source" guide recommended last week — starting with documentation before jumping into code.
 
---
 
### Activity 3: Contribute to External Community – p5.js
 
This week I attempted to begin contributing to p5.js. While I did not end up submitting an actual contribution, I made a genuine effort to explore the repository and identify where I could realistically help. This process was more difficult than I expected, and I want to reflect on that honestly here.
 
**What I Tried:**
 
I started by browsing the open issues on the p5.js repository, filtering by `good-first-issue` to find something manageable. I spent time reading through several issues, including ones related to improving inline documentation comments and fixing small inconsistencies in examples. On the surface, some of these looked approachable.
 
However, when I actually opened the repository files and tried to trace where changes would need to be made, I quickly realized how large and complex the codebase is. The source files are organized across many folders, the build system uses tools I was not yet familiar with, and even a small documentation fix required understanding how the JSDoc comments connect to the auto-generated reference website.
 
**Where I Think I Could Contribute:**
 
After spending time exploring, I identified a realistic area — the inline documentation for shape functions like `ellipse()` had some parameters that were not clearly described. For example, the behaviour when the fourth parameter is omitted was not explicitly stated. This felt like a change I could make with more confidence after familiarizing myself further with the project structure.
 
I also noticed that some of the beginner-facing example sketches had minor inconsistencies in commenting style, which could be a good entry point that does not require deep knowledge of the core library.
 
**Why I Did Not Submit Anything Yet:**
 
Honestly, I did not feel confident enough to submit a pull request this week. The contribution guidelines for p5.js are detailed — they require unit tests for code changes, a specific commit message format, and tagging the right area steward for review. I did not want to submit something incomplete or incorrect and leave a bad impression on the maintainers. I felt it was more responsible to take more time to understand the project properly before submitting.
 
**Reflection on the Most Challenging Part of This Week:**  
The hardest part was dealing with the gap between thinking a contribution would be simple and discovering how much context is actually needed before touching someone else's codebase. I overcame the frustration by reminding myself that this is a normal part of the open source experience — even experienced developers take time to understand a new project before contributing. My plan going forward is to keep reading through the codebase, follow a few more merged pull requests to understand the process better, and make my first real contribution in the coming weeks when I feel properly prepared.
 
---
 
### Weekly Reflection
 
Week 10 connected theory and practice in a meaningful way. Learning about MV\* patterns showed me that architectural decisions shape every part of how an application is built — choosing MVC, MVVM, or MVP affects how files are organized, how data flows, and how testable the code is. The connection between MVVM's data binding and the Observer pattern from Week 9 made me realize that design patterns and architectural patterns are not separate ideas — they work together. On the practical side, assessing p5.js's contribution guidelines and beginning my first real open source contribution was both exciting and humbling. The codebase is large, the standards are high, and the process is more structured than I expected. I spent approximately **3 hours** this week and am looking forward to completing and submitting my contribution next week.
 
> **Code Reference:** See [`contributions.md`](./contributions.md) – Week 10 snippets showing MVC and MVVM structural examples in JavaScript.
 
---
 
## Bibliography
 
- DGL 104 Course Notes. (2025). *Week 8: Functional user requirements and user stories*. North Island College.
- DGL 104 Course Notes. (2025). *Week 9: Design patterns*. North Island College.
- DGL 104 Course Notes. (2025). *Week 10: MV\* patterns*. North Island College.
- GitHub Open Source Guides. (2025). *How to contribute to open source*. https://opensource.guide/how-to-contribute/
- p5.js. (2025). *Contributing to p5.js*. https://github.com/processing/p5.js/blob/main/CONTRIBUTING.md
- Processing Foundation. (2025). *Processing*. https://processing.org
- Refactoring Guru. (2025). *Design patterns*. https://refactoring.guru/design-patterns
- Shiffman, D. (2025). *The Coding Train*. https://www.youtube.com/c/TheCodingTrain
 
