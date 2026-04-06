# Contributions – Code Snippets
 
---
 
## Week 11 – Object-Oriented Programming in JavaScript
 
**Language:** JavaScript  
**Topic:** The four OOP principles — Encapsulation, Abstraction, Inheritance, and Polymorphism  
 
---
 
### Snippet 1 – Encapsulation
 
```javascript
// Encapsulation – hiding data inside a class using private fields
 
class BankAccount {
  #balance; // Private field – cannot be accessed outside the class
 
  constructor(owner, initialBalance) {
    this.owner = owner;
    this.#balance = initialBalance;
  }
 
  deposit(amount) {
    if (amount > 0) {
      this.#balance += amount;
      console.log(`Deposited $${amount}. New balance: $${this.#balance}`);
    }
  }
 
  withdraw(amount) {
    if (amount > 0 && amount <= this.#balance) {
      this.#balance -= amount;
      console.log(`Withdrawn $${amount}. New balance: $${this.#balance}`);
    } else {
      console.log("Insufficient funds!");
    }
  }
 
  getBalance() {
    return this.#balance;
  }
}
 
const account = new BankAccount("Alice", 5000);
account.deposit(1000);
account.withdraw(2000);
console.log("Current Balance: $" + account.getBalance()); // $4000
 
// account.#balance = 999999; // ❌ This would throw an error – data is protected
```
 
**What This Code Does:**
- The `#balance` field uses JavaScript's private field syntax, meaning it cannot be read or modified from outside the class — this is encapsulation protecting the integrity of sensitive data.
- The `deposit()` and `withdraw()` methods are the only controlled access points to modify the balance, and they include validation logic to prevent invalid operations like negative deposits or overdrafts.
- This pattern directly mirrors the `BankAccount` example from the Week 11 OOP lecture, translated into modern JavaScript syntax using ES2022 private class fields instead of Java's `private` keyword.
 
---
 
### Snippet 2 – Abstraction
 
```javascript
// Abstraction – defining a common interface without exposing implementation
 
class Shape {
  // Simulated abstract method – subclasses must override this
  draw() {
    throw new Error("draw() must be implemented by subclass");
  }
 
  describe() {
    console.log("I am a shape.");
  }
}
 
class Circle extends Shape {
  draw() {
    console.log("Drawing a Circle ⬤");
  }
}
 
class Rectangle extends Shape {
  draw() {
    console.log("Drawing a Rectangle ▬");
  }
}
 
class Triangle extends Shape {
  draw() {
    console.log("Drawing a Triangle ▲");
  }
}
 
// The caller only needs to know that shapes can be drawn
const shapes = [new Circle(), new Rectangle(), new Triangle()];
shapes.forEach(shape => shape.draw());
 
// Output:
// Drawing a Circle ⬤
// Drawing a Rectangle ▬
// Drawing a Triangle ▲
```
 
**What This Code Does:**
- The `Shape` base class defines a `draw()` method that throws an error if not overridden, simulating an abstract method — JavaScript does not have a built-in `abstract` keyword like Java, so this is a common pattern to enforce the contract.
- Each subclass provides its own implementation of `draw()`, hiding the details of *how* each shape is drawn from the code that uses them — the `forEach` loop does not need to know what type of shape it is dealing with.
- This snippet is directly inspired by the `Animal` and `Shape` abstraction examples in the Week 11 lecture, and also connects to the p5.js work this semester — in Processing-style creative coding, abstracting drawing logic into shape classes is a very common and practical pattern.
 
---
 
### Snippet 3 – Inheritance
 
```javascript
// Inheritance – child class reuses and extends parent class behaviour
 
class Vehicle {
  constructor(brand) {
    this.brand = brand;
  }
 
  honk() {
    console.log(`${this.brand} goes: Beep! Beep!`);
  }
 
  describe() {
    console.log(`This is a ${this.brand} vehicle.`);
  }
}
 
class Car extends Vehicle {
  constructor(brand, model) {
    super(brand); // Calls the parent constructor
    this.model = model;
  }
 
  showDetails() {
    console.log(`Car: ${this.brand} ${this.model}`);
  }
}
 
class ElectricCar extends Car {
  constructor(brand, model, range) {
    super(brand, model); // Calls Car constructor
    this.range = range;
  }
 
  showDetails() {
    console.log(`Electric Car: ${this.brand} ${this.model} | Range: ${this.range}km`);
  }
}
 
const myCar = new Car("Toyota", "Camry");
myCar.honk();        // Inherited from Vehicle
myCar.showDetails(); // Defined in Car
 
const myEV = new ElectricCar("Tesla", "Model 3", 500);
myEV.honk();         // Inherited from Vehicle via Car
myEV.showDetails();  // Overridden in ElectricCar
```
 
**What This Code Does:**
- The `Car` class inherits from `Vehicle` using the `extends` keyword and calls `super(brand)` to initialize the parent class — this demonstrates the **extension** strategy of inheritance where new features are added without modifying the original class.
- `ElectricCar` extends `Car` which in turn extends `Vehicle`, creating a three-level inheritance chain that mirrors the Bird → FlyingBird → Robin hierarchy shown in Fig. 11.6 of the Week 11 lecture.
- This example shows how inheritance eliminates redundant code — `honk()` is written once in `Vehicle` but is available to both `Car` and `ElectricCar` automatically, which is exactly the code reusability benefit described in the lecture.
 
---
 
### Snippet 4 – Polymorphism and Dynamic Binding
 
```javascript
// Polymorphism – same method name, different behaviour per object type
 
class Animal {
  makeSound() {
    console.log("Some generic animal sound...");
  }
}
 
class Dog extends Animal {
  makeSound() {
    console.log("Woof! Woof!");
  }
}
 
class Cat extends Animal {
  makeSound() {
    console.log("Meow! Meow!");
  }
}
 
class Duck extends Animal {
  makeSound() {
    console.log("Quack! Quack!");
  }
}
 
// Polymorphism in action – the correct makeSound() is called at runtime
const animals = [new Dog(), new Cat(), new Duck(), new Animal()];
 
animals.forEach(animal => animal.makeSound());
 
// Output:
// Woof! Woof!
// Meow! Meow!
// Quack! Quack!
// Some generic animal sound...
```
 
**What This Code Does:**
- Each subclass overrides the `makeSound()` method with its own specific implementation — this is **method overriding**, the foundation of polymorphism in OOP languages.
- The `forEach` loop calls `makeSound()` on every animal without knowing or caring what specific type each one is — JavaScript's **dynamic binding** resolves which version of `makeSound()` to call at runtime based on the actual object type, not the variable type.
- This snippet directly demonstrates the polymorphism diagram from Fig. 11.7 of the Week 11 lecture (Shape → Circle/Box/Triangle with their own `draw()` methods), applied to the Animal example from the course notes — showing that the same principle works across any type hierarchy.
 