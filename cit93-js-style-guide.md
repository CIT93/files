# CIT93 JavaScript: Code Style Guide

Welcome to the JavaScript code style guide. Consistent coding styles make projects easier to read, debug, and maintain—especially when navigating your assignments in VS Code or GitHub Codespaces. 

Based on our Week 6 codebase, please adhere to the following conventions for all future JavaScript modules.

## 1. Variable Declarations

* **Use `const` by Default:** Always declare your variables using `const` unless you are absolutely certain the variable's reference will need to be reassigned later (Rio's Rule).
* **Arrays and Objects:** Use `const` even for arrays and objects whose contents will change over time. `const` prevents the variable identifier from being reassigned, but it still allows you to push new items to an array or update object properties.
  ```javascript
  // Good: The array reference remains constant, even as items are pushed.
  const carbonFootprintEntries = [];
  carbonFootprintEntries.push(newEntry);
  ```
* **State Variables (`let`):** Use `let` exclusively for variables that require reassignment, such as tracking UI states, timeouts, or toggles.
  ```javascript
  let isConfirmingClearAll = false; 
  let clearAllTimeoutId = null; 
  ```
* **Global Constants:** Use `SCREAMING_SNAKE_CASE` for global, unchangeable constants (like storage keys) to distinguish them from standard variables.
  ```javascript
  const LOCAL_STORAGE_KEY = 'carbonFootprintEntries';
  ```

## 2. Function Syntax

* **Function Expressions:** Define functions as expressions and assign them to `const` variables rather than using standard function declarations. This prevents hoisting issues and keeps your code execution predictable.
  ```javascript
  // Good
  const handleFormSubmit = function(event) {
      event.preventDefault();
      // ...
  };
  ```

## 3. Control Structures

* **Single-Statement `if/else` Blocks:** For brief, single-statement `if`, `else if`, or `else` conditions, you may omit the curly brace block delimiters to keep the code concise. Keep these on a single line.
  ```javascript
  // Good
  if (householdMembers === 1) return 14;
  else if (householdMembers === 2) return 12;
  ```
* **Switch Statements:** Use `switch` statements when evaluating a single variable against multiple specific string or number values (e.g., categorizing diet types or food packaging).
  ```javascript
  switch (dietType) {
      case 'meatHeavy': return 10;
      case 'average': return 8;
      default: return 0;
  }
  ```

## 4. Modern JavaScript Features (ES6+)

* **Modules:** Break your code into focused files (modules). Use `export const` to expose functions and `import * as moduleName from './module.js'` to bring them into your main application file.
* **Spread Operator:** Use the spread operator (`...`) to efficiently copy and merge object properties.
  ```javascript
  const newEntry = {
      ...formData,
      ...calculatedResults,
      timestamp: new Date().toISOString()
  };
  ```
* **Template Literals:** Use backticks (`` ` ``) and the `${}` syntax for string interpolation instead of concatenation.
  ```javascript
  console.log(`${radio.value} has the attribute of ${radio.checked}`);
  ```
* **Clearing `const` Arrays:** To clear an array defined with `const`, do not attempt to reassign it to an empty array `[]`. Instead, set its `.length` property to `0`.
  ```javascript
  carbonFootprintEntries.length = 0; 
  ```
* **Shallow Copies:** When sorting an array that you do not want to permanently reorder, use the spread operator (`...`) to create a shallow copy first.
  ```javascript
  const sortedEntries = [...entries].sort(function(a, b) { ... });
  ```

## 5. DOM Manipulation

* **Variable Caching:** Store references to DOM elements at the top of your modules using `const` so you only query the DOM once.
  ```javascript
  const carbonFootprintForm = document.getElementById('carbonFootprintForm');
  const householdMembersInput = carbonFootprintForm.querySelector('#householdMembers');
  ```
* **Dynamic Elements:** Use `document.createElement()` to generate new HTML elements using JavaScript, and `appendChild()` to add them as children of another element in the DOM. Use `innerHTML` combined with template literals to quickly build the internal structure of newly created elements. 
* **Data Attributes:** Use the `.dataset` property to attach and read custom `data-*` attributes directly on HTML elements.
  ```javascript
  row.dataset.id = entry.id;
  ```
* **Separation of Concerns:** Keep DOM updates and event listeners separate from your core calculation logic. 

## 6. Persistent Storage & Error Handling

* **`localStorage` and JSON:** `localStorage` can only store strings. When saving objects or arrays, you must convert them into a JSON string using `JSON.stringify()`. When retrieving them, convert them back into a JavaScript array or object using `JSON.parse()`.
* **`try...catch` Blocks:** Always wrap your `localStorage` read and write operations inside a `try...catch` block. This allows the application to catch an error and keep running if the stored data is corrupted or fails to parse.
  ```javascript
  try {
      localStorage.setItem(LOCAL_STORAGE_KEY, JSON.stringify(entries));
  } catch (error) {
      console.error(`Error saving data: ${error}`);
  }
  ```

## 7. Commenting and Documentation

* **Inline Comments:** Use `//` for brief explanations of complex logic, step-by-step descriptions, or clarifications on specific method choices.

## 8. Debugging and DevTools

* **Test Your Execution:** Always make sure your code actually runs! Submit your forms, interact with your UI, and verify that the expected behaviors occur before submitting your work.
* **Check the Console:** Keep your browser's Developer Tools open while you work. Watch the Console tab closely for any red error messages when your page loads or when a form is submitted.
* **Step Through Your Code:** Using DevTools to set breakpoints and step through your code line-by-line is a critical skill for understanding execution flow and finding bugs.
* **Technical Code Reviews:** Demonstrating how to use DevTools to step through your code will be a required part of your technical code reviews. Make sure you are practicing this regularly!