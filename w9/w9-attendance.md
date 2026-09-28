# CIT93 Week 9: The "Delete & State" Investigation Tasks

### Level 1: The "Navigator" (Foundational Knowledge)
1. Find the `handleDeleteEntry` function. Which line number starts the actual removal of data from the array?
2. In the `init` function, we load data from `localStorage`. If `loadedEntries` has data, what syntax do we use to push those items into our main array?
3. Where in the code do we tell the browser to "stop and wait" for the user to submit the form (preventing a page reload)?
4. In `handleDeleteEntry`, we check `if(indexToDelete !== -1)`. What does a value of `-1` represent in JavaScript when using `findIndex`?
5. Look at `performClearAllData`. We call `resultsDisplay.hideResults()`. Why do we do this if we are already clearing the table?
6. In the "Clear All" logic, which specific line of code physically changes the text the user sees on the button?

### Level 2: The "Detective" (Intermediate Logic)
7. We use `const carbonFootprintEntries`. Why doesn't the browser throw an error when we `splice` or change the `.length` of a `const` array?
8. In `handleDeleteEntry`, we call `renderTable`. What would happen to the screen if we deleted the data from memory but skipped this line?
9. Why do we pass `handleDeleteEntry` as an argument inside an object to `renderTable`? Why not just call it directly from the table module?
10. If you have items in your table and click "Clear All" once (activating the "Are you sure?" state), then click the page background, why does the button reset?
11. In `handleFormSubmit`, how does the code distinguish between "Creating a new entry" and "Updating an existing one" (Edit mode)?
12. Look at the `setTimeout` in the `init` function. What is the numerical value `3000` representing, and what happens when that time is up?

### Level 3: The "Architect" (Advanced Concepts)
13. **Trace the ID:** The ID starts in the HTML table. How does it travel through the `onDelete` callback in the renderer to reach `handleDeleteEntry` in `app.js`?
14. In the "Clear All" listener, we use `event.stopPropagation()`. What "parent" element are we preventing this click event from reaching?
15. Why do we use `carbonFootprintEntries.length = 0` to clear the array instead of simply saying `carbonFootprintEntries = []`?
16. If you delete a record and then **immediately** close the browser tab, why is the record still gone when you come back? (Which function is responsible?)
17. In `handleEditEntry`, we use `window.scrollTo`. What property of the `window` object are we manipulating, and why is `behavior: 'smooth'` a good UX choice?
18. **The Safety Net:** In the "Clear All" logic, we store `clearAllTimeoutId`. Why is it critical to call `clearTimeout` at the start of the `resetClearAllButton` function?