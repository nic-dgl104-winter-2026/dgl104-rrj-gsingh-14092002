# DGL 104 – Research and Reflection Journal
 
**Course:** DGL 104 – Application Development Foundations  
**Student:** Gagandeep singh  
**Semester:** Winter 2026  
 
---
  
## Week 9 – Mar. 4
 
### Overview
 
Week 9 introduced one of the most important concepts in software development — **design patterns**. According to the course notes, design patterns are reusable fragments of code that provide a solution to a specific and typically well-understood coding problem (DGL 104 Course Notes, Week 9, 2025). This week also focused on understanding open source contributions and finding real projects to potentially contribute to. The three main activities this week were: researching four key design patterns, reading the open source contribution guide, and identifying potential projects to contribute to.
 
---
 
### Activity 1: Research on Design Patterns
 
Design patterns are typical solutions to commonly occurring problems in software design. They are like pre-made blueprints that can be customized to solve a recurring design problem in code (Refactoring Guru, 2025). They are divided into three main categories: **Creational**, **Structural**, and **Behavioural**. This week I studied four key patterns in detail.
 
---
 
#### 1. Factory Method Pattern *(Creational)*
 
The **Factory Method** pattern provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created (Refactoring Guru, 2025).
 
**Purpose:**  
It is used when a program needs to create objects without specifying the exact class of the object that will be created. This keeps the code flexible and easy to extend.
 
**Real-World Application:**  
A notification system is a great example. The system may need to send different types of notifications — such as `EmailNotification` or `SMSNotification` — depending on user preferences. Instead of hardcoding which type to create, the Factory Method lets the subclass decide which object to instantiate.
 
**Example:**
 
```javascript
class Notification {
  send() {
    throw new Error("send() must be implemented");
  }
}
 
class EmailNotification extends Notification {
  send() {
    console.log("Sending Email Notification");
  }
}
 
class SMSNotification extends Notification {
  send() {
    console.log("Sending SMS Notification");
  }
}
 
class NotificationFactory {
  static create(type) {
    if (type === "email") return new EmailNotification();
    if (type === "sms") return new SMSNotification();
    throw new Error("Unknown notification type");
  }
}
 
const notification = NotificationFactory.create("email");
notification.send(); // Output: Sending Email Notification
```
 
**Reflection:**  
The Factory Method pattern made me think about how often I have written `if/else` blocks just to decide which object to create. This pattern gives that logic a proper structure, making it much easier to add new types in the future without changing existing code.
 
---
 
#### 2. Adapter Pattern *(Structural)*
 
The **Adapter** pattern allows objects with incompatible interfaces to collaborate (Refactoring Guru, 2025).
 
**Purpose:**  
It acts as a bridge between two incompatible systems, converting the interface of one class into another that a client expects. This is especially useful when integrating third-party libraries or external APIs.
 
**Real-World Application:**  
When an application connects to an external API that uses a different data format, an adapter converts the data so both systems can communicate properly. For example, an app that expects data in JSON format but receives XML from an API would use an adapter to convert the XML into JSON before processing it.
 
**Example:**
 
```javascript
// Old system speaks XML
class XmlDataProvider {
  getXmlData() {
    return "<user><name>Alice</name></user>";
  }
}
 
// New system expects JSON
class XmlToJsonAdapter {
  constructor(xmlProvider) {
    this.xmlProvider = xmlProvider;
  }
 
  getData() {
    const xml = this.xmlProvider.getXmlData();
    // Simplified conversion for demonstration
    return { user: { name: "Alice" } };
  }
}
 
const adapter = new XmlToJsonAdapter(new XmlDataProvider());
console.log(adapter.getData()); // Output: { user: { name: 'Alice' } }
```
 
**Reflection:**  
The Adapter pattern solved a problem I have encountered in practice — trying to connect two systems that were never designed to work together. Before knowing about this pattern, I would have rewritten one of the systems entirely. Now I understand that an adapter is a cleaner, less disruptive solution.
 
---
 
#### 3. Observer Pattern *(Behavioural)*
 
The **Observer** pattern lets you define a subscription mechanism to notify multiple objects about any events that happen to the object they are observing (Refactoring Guru, 2025).
 
**Purpose:**  
It is used when a change in one object needs to automatically trigger updates in one or more other objects. This is very common in event-driven systems.
 
**Real-World Application:**  
Social media platforms use the Observer pattern constantly. When a user posts something or interacts with content, all their followers receive a notification automatically. The post is the **subject** and the followers are the **observers**.
 
**Example:**
 
```javascript
class EventEmitter {
  constructor() {
    this.listeners = [];
  }
 
  subscribe(listener) {
    this.listeners.push(listener);
  }
 
  notify(data) {
    this.listeners.forEach(listener => listener(data));
  }
}
 
const feed = new EventEmitter();
 
feed.subscribe((post) => console.log(`User 1 notified: ${post}`));
feed.subscribe((post) => console.log(`User 2 notified: ${post}`));
 
feed.notify("Alice posted a new photo!");
// Output:
// User 1 notified: Alice posted a new photo!
// User 2 notified: Alice posted a new photo!
```
 
**Reflection:**  
The Observer pattern is one I had unknowingly used before when working with event listeners in JavaScript — `addEventListener` is essentially an implementation of this pattern. Naming and understanding the pattern formally helps me recognize it in code written by others, which makes reading and maintaining codebases much easier.
 
---
 
#### 4. Singleton Pattern *(Creational)*
 
The **Singleton** pattern ensures that a class has only one instance while providing a global access point to that instance (Refactoring Guru, 2025).
 
**Purpose:**  
It is used for shared resources that should only exist once throughout the lifetime of an application — such as a configuration manager, logging system, or database connection.
 
**Real-World Application:**  
A logging system is a perfect example. If every part of an application created its own logger, logs would be scattered and inconsistent. The Singleton ensures that every part of the application writes to the same single logger instance.
 
**Example:**
 
```javascript
class Logger {
  constructor() {
    if (Logger.instance) {
      return Logger.instance;
    }
    this.logs = [];
    Logger.instance = this;
  }
 
  log(message) {
    this.logs.push(message);
    console.log(`[LOG]: ${message}`);
  }
}
 
const logger1 = new Logger();
const logger2 = new Logger();
 
logger1.log("App started");
logger2.log("User logged in");
 
console.log(logger1 === logger2); // Output: true (same instance)
```
 
**Reflection:**  
The Singleton pattern is powerful but should be used carefully. While it solves the problem of shared resources elegantly, overusing it can make code harder to test because global state is difficult to reset between tests. This taught me that design patterns are not automatically the right solution — context and trade-offs always matter.
 
---
 
### Activity 2: Read "How to Contribute to Open Source"
 
This week I read GitHub's *"How to Contribute to Open Source"* guide in full. The guide covered everything from understanding what open source is, to finding projects, to making your first contribution (GitHub Open Source Guides, 2025).
 
**Key Takeaways:**
 
**What counts as a contribution?**  
I learned that contribution does not only mean writing code. It also includes fixing documentation, reporting bugs, translating content, helping other users in forums, reviewing pull requests, and designing UI elements. This was reassuring because it means there are many ways to add value to a project regardless of skill level.
 
**Section 2 – What it means to contribute:**  
This section emphasized that contributions are about community as much as code. Every open source project has its own culture and norms, and reading the `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, and existing issues before contributing is essential. Jumping in without reading these can lead to wasted effort or rejected pull requests.
 
**Section 4 – Finding a project to contribute to:**  
This section recommended starting small — looking for issues labelled `good-first-issue` or `help wanted`. It also recommended contributing to projects you already use, because you understand them as a user and are more motivated to improve them.
 
**Reflection:**  
Reading this guide shifted my perspective on open source. I previously thought contributing meant submitting large, complex pull requests to huge projects like Linux or React. In reality, even fixing a typo in documentation is a valued contribution. The guide also made me think carefully about project health — a project with no recent activity, no responses to issues, and no `CONTRIBUTING.md` is not a good place to start. I will use these criteria when selecting projects to contribute to.
 
---
 
### Activity 3: Find Potential Projects to Contribute To
 
Using **Good First Issue**, **Up for Grabs**, and **CodeTriage**, I identified three potential open source projects that align with what I have been learning in DGL 104.
 
---
 
#### Project 1: p5.js
 
**URL:** [https://github.com/processing/p5.js](https://github.com/processing/p5.js)
 
**Summary:**  
p5.js is a JavaScript library that brings the creative coding and visual art philosophy of Processing to the web. Since I researched Processing in Week 8, this project felt like a natural connection. The repository is very active, has a welcoming `CONTRIBUTING.md`, and has many issues labelled `good-first-issue` related to documentation, examples, and bug fixes.
 
**Checklist Highlights:**
-  Has a clear `README.md`
-  Has a `CONTRIBUTING.md` with clear instructions
-  Has a `CODE_OF_CONDUCT.md`
-  Issues are actively responded to by maintainers
-  Has `good-first-issue` labels
-  Last commit within the past week
 
**Interesting Discovery:**  
The p5.js community is deeply connected to the Processing Foundation, which actively promotes diversity and inclusion in creative coding. The project explicitly welcomes contributions from beginners and artists, not just experienced developers.
 
---
 
#### Project 2: freeCodeCamp
 
**URL:** [https://github.com/freeCodeCamp/freeCodeCamp](https://github.com/freeCodeCamp/freeCodeCamp)
 
**Summary:**  
freeCodeCamp is one of the largest open source educational platforms for learning web development. It is written in JavaScript and has thousands of open issues, many of which are documentation and curriculum improvements that do not require deep technical knowledge.
 
**Checklist Highlights:**
-  Has a detailed `README.md`
-  Has a thorough `CONTRIBUTING.md`
-  Issues are clearly categorized and labelled
-  Very active community and fast maintainer responses
-  Has `first-timers-only` and `help wanted` labels
-  Last commit within the past 24 hours
 
**Interesting Discovery:**  
freeCodeCamp has a dedicated contributor community on Discord with thousands of members, which makes it easy to ask questions and get guidance before submitting a pull request.
 
---
 
#### Project 3: Docusaurus
 
**URL:** [https://github.com/facebook/docusaurus](https://github.com/facebook/docusaurus)
 
**Summary:**  
Docusaurus is an open source documentation website builder maintained by Meta. It is built with JavaScript and React and is used by many well-known projects. It has clear contribution guidelines and regularly posts issues suitable for new contributors.
 
**Checklist Highlights:**
-  Has a clear `README.md`
-  Has a `CONTRIBUTING.md`
-  Issues are well-labelled and organized
-  Maintainers respond to issues within a few days
-  Has `good first issue` labels
-  Last commit within the past week
 
**Interesting Discovery:**  
Docusaurus is used to build the documentation sites for projects like React, Redux, and Jest. Contributing to Docusaurus means indirectly improving documentation for some of the most widely used tools in web development.
 
---
 
### Community Connections
 
After exploring the three projects above, I spent time researching their community connections.
 
- **p5.js** has an active forum at [https://discourse.processing.org](https://discourse.processing.org) and a Discord server. The Processing Foundation also runs an annual fundraiser and community events.
- **freeCodeCamp** has a very large Discord server with dedicated channels for contributors, including channels for first-timers. They also have a forum at [https://forum.freecodecamp.org](https://forum.freecodecamp.org).
- **Docusaurus** is connected to the broader Meta Open Source community and has a Discord server linked directly from the repository.
 
**Reflection:**  
Exploring community connections showed me that the best open source projects are more than just code repositories — they are living communities of people who share knowledge, help each other, and build together. Finding the community home of a project before contributing is important because it gives you access to informal guidance that is not always in the documentation. I plan to join the p5.js Discord before making my first contribution, as it seems the most aligned with what I have been studying this semester.
 
---
 
### Weekly Reflection
 
Week 9 was one of the most content-rich weeks so far. Learning about design patterns gave me a vocabulary and structure for problems I had encountered before but could not name. The Factory Method, Adapter, Observer, and Singleton patterns each solve a specific, real problem — and knowing them makes me a more confident developer. Reading the open source contribution guide removed a lot of the fear I had around contributing to public projects. And exploring GitHub for real projects showed me that there are communities out there that are genuinely welcoming to beginners. I spent approximately **3 hours** this week and feel ready to make my first contribution in the coming weeks.
 
> **Code Reference:** See [`contributions.md`](./contributions.md) – Week 9 design pattern code snippets in JavaScript demonstrating all four patterns studied this week.
 
---
 
## Bibliography
 
- DGL 104 Course Notes. (2025). *Week 8: Functional user requirements and user stories*. North Island College.
- DGL 104 Course Notes. (2025). *Week 9: Design patterns*. North Island College.
- GitHub Open Source Guides. (2025). *How to contribute to open source*. https://opensource.guide/how-to-contribute/
- Processing Foundation. (2025). *Processing*. https://processing.org
- Refactoring Guru. (2025). *Design patterns*. https://refactoring.guru/design-patterns
- Shiffman, D. (2025). *The Coding Train*. https://www.youtube.com/c/TheCodingTrain
 