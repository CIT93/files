# CIT93 JavaScript: Code Style Guide

Welcome to the JavaScript code style guide. Consistent coding styles make projects easier to read, debug, and maintain—especially when navigating your assignments in VS Code or GitHub Codespaces. 

Based on our Week 4 codebase, please adhere to the following conventions for all future JavaScript modules.

## 1. Variable Declarations

* **Use `const` by Default:** Always declare your variables using `const` unless you are absolutely certain the variable's reference will need to be reassigned later. Rio's Rule
* **Arrays and Objects:** Use `const` even for arrays and objects whose contents will change over time. `const` prevents the variable identifier from being reassigned, but it still allows you to push new items to an array or update object properties.
  ```javascript
  // Good: The array reference remains constant, even as items are pushed.
  const carbonFootprintEntries = [];
  carbonFootprintEntries.push(newEntry);
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

## 5. DOM Manipulation

* **Variable Caching:** Store references to DOM elements at the top of your modules using `const` so you only query the DOM once.
  ```javascript
  const carbonFootprintForm = document.getElementById('carbonFootprintForm');
  const householdMembersInput = carbonFootprintForm.querySelector('#householdMembers');
  ```
* **Separation of Concerns:** Keep DOM updates and event listeners separate from your core calculation logic. 

## 6. Commenting and Documentation

* **Inline Comments:** Use `//` for brief explanations of complex logic, step-by-step descriptions, or clarifications on specific method choices.
