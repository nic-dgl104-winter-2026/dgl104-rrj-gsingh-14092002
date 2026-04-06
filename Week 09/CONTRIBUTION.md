# Contributions – Code Snippets
   
---
 
## Week 9 – Design Patterns in JavaScript
 
**Language:** JavaScript  
**Topic:** Factory Method, Adapter, Observer, and Singleton design patterns  
 
---
 
### Snippet 1 – Factory Method Pattern
 
```javascript
// Factory Method Pattern
// Creates different notification objects based on type
 
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
 
**What This Code Does:**
- The `NotificationFactory` class decides which notification object to create based on the `type` argument, so the calling code never needs to know the exact class being instantiated.
- `EmailNotification` and `SMSNotification` both extend the base `Notification` class, meaning new types can be added in the future without changing any existing code — this is the core benefit of the Factory Method pattern.
- This pattern removes hardcoded `if/else` object creation from the main program logic, making the code cleaner, more flexible, and easier to extend over time.
 
---
 
### Snippet 2 – Adapter Pattern
 
```javascript
// Adapter Pattern
// Converts XML data to JSON format so two incompatible systems can work together
 
class XmlDataProvider {
  getXmlData() {
    return "<user><name>Alice</name></user>";
  }
}
 
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
 
**What This Code Does:**
- The `XmlDataProvider` represents an old or external system that returns data in XML format, while the rest of the application expects JSON — the `XmlToJsonAdapter` sits between them and translates the data format.
- The adapter wraps the incompatible class and exposes a `getData()` method that the new system understands, meaning neither the old system nor the new system needs to be rewritten.
- This pattern is especially useful when integrating third-party APIs or legacy systems where you cannot modify the original source code.
 
---
 
### Snippet 3 – Observer Pattern
 
```javascript
// Observer Pattern
// Notifies multiple subscribers when an event occurs
 
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
 
**What This Code Does:**
- The `EventEmitter` class maintains a list of subscriber functions and calls each one automatically whenever `notify()` is triggered, so multiple parts of an application can react to the same event independently.
- New subscribers can be added at any time without changing the `EventEmitter` class itself, making this pattern very easy to extend as an application grows.
- This is the same mechanism behind JavaScript's `addEventListener` — understanding the Observer pattern formally helps in recognizing and reasoning about event-driven code in any language.
 
---
 
### Snippet 4 – Singleton Pattern
 
```javascript
// Singleton Pattern
// Ensures only one Logger instance exists throughout the application
 
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
 
**What This Code Does:**
- The `Logger` constructor checks if an instance already exists before creating a new one — if it does, it returns the existing instance instead, ensuring the class is only ever instantiated once no matter how many times `new Logger()` is called.
- Both `logger1` and `logger2` point to the exact same object in memory, which means all log messages across the entire application go to one consistent place.
- This pattern is ideal for shared resources like loggers, configuration managers, or database connections, but should be used carefully since global state can make unit testing more difficult.
 