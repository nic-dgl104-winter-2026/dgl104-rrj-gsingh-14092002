# Contributions – Code Snippets
 
---
 
## Week 10 – MV* Patterns in JavaScript
 
**Language:** JavaScript  
**Topic:** MVC and MVVM architectural pattern structures  
 
---
 
### Snippet 1 – MVC Pattern (Model View Controller)
 
```javascript
// MVC Pattern
// Separates data (Model), UI (View), and logic (Controller)
 
// MODEL – manages data
class PostModel {
  constructor() {
    this.posts = [];
  }
  addPost(post) {
    this.posts.push(post);
  }
  getPosts() {
    return this.posts;
  }
}
 
// VIEW – displays data
class PostView {
  render(posts) {
    console.log("---- Posts ----");
    posts.forEach((post, i) => console.log(`${i + 1}. ${post}`));
  }
}
 
// CONTROLLER – handles input and coordinates Model and View
class PostController {
  constructor(model, view) {
    this.model = model;
    this.view = view;
  }
  addPost(post) {
    this.model.addPost(post);
    this.view.render(this.model.getPosts());
  }
}
 
const model = new PostModel();
const view = new PostView();
const controller = new PostController(model, view);
 
controller.addPost("Hello World");
controller.addPost("MVC is clean!");
// Output:
// ---- Posts ----
// 1. Hello World
// ---- Posts ----
// 1. Hello World
// 2. MVC is clean!
```
 
**What This Code Does:**
- The `PostModel` manages the raw data (the list of posts) with no knowledge of how the data will be displayed, keeping the business logic completely separate from the user interface.
- The `PostView` is only responsible for rendering whatever data it receives — it does not know where the data comes from or how it was changed.
- The `PostController` sits between the two, receiving user actions (like `addPost`), updating the Model, and then instructing the View to re-render — this clear separation is what makes MVC applications easier to maintain and test.
 
---
 
### Snippet 2 – MVVM Pattern (Model View ViewModel)
 
```javascript
// MVVM Pattern
// ViewModel exposes reactive data that the View binds to automatically
 
// MODEL – raw data
class UserModel {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}
 
// VIEWMODEL – prepares and exposes data for the View
class UserViewModel {
  constructor(user) {
    this.user = user;
    this.listeners = [];
  }
 
  // Simulated data binding – notifies View on change
  subscribe(listener) {
    this.listeners.push(listener);
  }
 
  notify() {
    this.listeners.forEach(fn => fn(this.getDisplayData()));
  }
 
  getDisplayData() {
    return {
      displayName: `Name: ${this.user.name}`,
      displayAge: `Age: ${this.user.age}`,
    };
  }
 
  updateName(newName) {
    this.user.name = newName;
    this.notify(); // Automatically updates the View
  }
}
 
// VIEW – subscribes to ViewModel and re-renders on change
const user = new UserModel("Alice", 25);
const viewModel = new UserViewModel(user);
 
// View subscribes (like a UI component binding to state)
viewModel.subscribe((data) => {
  console.log("View updated:", data.displayName, "|", data.displayAge);
});
 
viewModel.updateName("Bob");
// Output: View updated: Name: Bob | Age: 25
```
 
**What This Code Does:**
- The `UserViewModel` exposes prepared, display-ready data to the View through `getDisplayData()`, so the View never needs to format or transform raw Model data itself.
- The subscription mechanism simulates **data binding** — when `updateName()` is called, the ViewModel automatically notifies all subscribed Views to re-render, which is exactly how frameworks like SwiftUI and Jetpack Compose work under the hood.
- This pattern builds directly on the **Observer pattern** from Week 9 — the ViewModel is the subject and the View is the observer, showing how design patterns and architectural patterns work together in real applications.
 
---
 
### Snippet 3 – Git Workflow I Studied for Open Source Contribution (p5.js)
 
> **Note:** This is a workflow I researched and studied this week while exploring how to contribute to p5.js. I have not yet executed these steps on the actual repository — this represents my preparation and understanding of the process before making a real contribution in a future.
 
```bash
# Step 1 – Fork the repository on GitHub, then clone your fork locally
git clone https://github.com/[your-username]/p5.js.git
cd p5.js
 
# Step 2 – Always create a new branch before making any changes
# Never work directly on main
git checkout -b fix/improve-ellipse-docs
 
# Step 3 – After making changes, stage and commit with a descriptive message
git add src/core/shape/2d_primitives.js
git commit -m "fix: clarify optional height parameter in ellipse() JSDoc"
 
# Step 4 – Push your branch to your forked repository
git push origin fix/improve-ellipse-docs
 
# Step 5 – Open a Pull Request on GitHub from your fork to the upstream repo
# Tag the appropriate area steward as required by p5.js contribution guidelines
```
 
**What I Learned From This Workflow:**
- The **fork-and-branch** model means all changes live on a separate branch in your personal fork, never directly on `main` — this keeps the fork clean and makes it easy to sync with the upstream repository as other contributors make changes.
- The commit message format follows **conventional commits** (`fix:`, `feat:`, `docs:`) which p5.js requires so that maintainers and automated tools can clearly understand the purpose and category of each change at a glance.
- Studying this workflow before actually running it helped me understand what the full contribution process looks like end-to-end — from forking all the way to opening a pull request and tagging a steward for review.
 