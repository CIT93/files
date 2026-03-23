# Decision Making App - Step 5
## Logic Expansion & Modern Syntax

In Step 5, you transition from following a set blueprint to implementing your own custom logic. You will also modernize your entire codebase by refactoring your functions into **Arrow Functions**, a standard in professional JavaScript development.

## Setup
* **Create Folder**: Inside your `my-app` folder, create a new folder named `step5`.
* **Copy Files**: Copy **all** files from your `step4` folder into your new `step5` folder.
* **Work Here**: Ensure you are only editing the files in the `step5` directory.
* **Commit with message**: `step 5 setup complete`

---

## Phase 1: The Modern Refactor (Arrow Functions)
Before adding your new features, you must modernize your code. Arrow functions provide a more concise syntax and are the industry standard for modern JavaScript development.

**Your Requirements:**
1. **Refactor Every Module:** Review `app.js`, `ui.js`, `table-renderer.js`, `form-handler.js`, and `data-store.js`.
2. **Convert to Arrows:** Change every function declaration or function expression into an **Arrow Function**.
   * *Reference:* Look at how we used arrow functions in the later stages of the Carbon Footprint project (`const myFunction = () => {}`).
3. **Check for Hoisting:** Remember that arrow functions are not "hoisted" to the top of the file like traditional function declarations. You may need to adjust the *order* of your functions in your files so they are defined *before* they are called.

*Test: Run your app. It should function exactly as it did in Step 4. If the console shows "ReferenceError: Cannot access... before initialization," you have a hoisting issue to fix!*
* **Commit with message**: `all functions refactored to arrow functions`

---

## Phase 2: Implement Your Custom Logic
It is time to execute the plan you wrote in your Step 4 README. You are adding a new dimension to your decision-making engine.

**Your Requirements:**
1. **HTML Update:** Add the new input field you planned. It must have a proper `<label>`, a unique `id`, and fit the layout of your existing form.
2. **Data Capture:** Update your form handler to capture this new value. Ensure it is being saved into your data object alongside your other inputs.
3. **Update the Engine (`decision.js`):** Modify your logic to factor in this new data. 
   * *Requirement:* This input cannot be "just for show." It **must** influence the final recommendation or score returned by your app.
4. **Update the UI:** Ensure this new value is rendered in your immediate results and appears as a new column in your history table. Remember to test the edit and delete functionality as well.  

*Test: Submit several entries. Verify that the new input is changing the results as expected and appearing correctly in the table.*
* **Commit with message**: `custom input and decision logic implemented`

---

## Phase 3: Planning for Step 6 (Form Validation)
In Step 6, we will focus on **Form Validation**—ensuring the user cannot submit "bad" data (like empty strings, negative numbers, or missing selections).

**Do not code the validation yet.** * Open your `README.md` file.
* Add a new section titled `## Step 6 Planning: Validation`.
* For **each** input in your form (including at least 3 inputs), answer the following three questions:
    1. **What is the "Required" state?** (e.g., Is it mandatory? Must a checkbox be checked?)
    2. **What are the "Boundary" rules?** (e.g., If it's a number, what is the min/max? If it's text, is there a minimum length?)
    3. **The Error Message:** Write out the exact, user-friendly sentence you want the user to see if they fail that specific validation.

* **Commit with message**: `step 5 complete and step 6 validation planned`