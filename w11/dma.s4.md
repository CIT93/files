# Decision Making App - Step 4
## UI Polish & In-Place Editing

In Step 4, we are taking your app from a functional prototype to a polished application. You will clean up the user interface (UI) to handle "empty states," ensure your "Clear Form" button works completely, and implement the final CRUD operation: **Updating (Editing)** existing entries.

> **Note:** As you've been building, you might have already tackled some of the UI cleanup (like hiding the table when it's empty). If you have, simply read through **Phase 1** to verify your logic meets the requirements before moving to Phase 2.

You have built a fantastic foundation over the past few weeks! To help you transition from following tutorials to independent problem-solving, this step provides the goals rather than the exact code. Whenever you aren't sure how to build a requirement, look back at your recent assignments—they hold all the technical answers you need to succeed here.

## Setup
* **Create Folder**: Inside your `my-apps` folder, create a new folder named `step4`.
* **Copy Files**: Copy **all** files from your `step3` folder and paste them into your new `step4` folder.
* **Work Here**: Close any open files from step 3 and open the files in `step4` to begin working.
* **Commit with message**: `step 4 setup complete`

---

## Phase 1: UI & Data Polish
Before we add new features, we need to clean up our user interface (UI) to handle "empty states" and refactor our data management so our modules are handling the right tasks. 

Use your **Carbon Footprint (CFP)** app as your technical reference for how to meet these requirements.

**Your Requirements:**
1. **HTML & CSS:** Ensure your immediate decision result container and your `<table>` are hidden by default using inline styles (`style="display: none;"`). Add a "No entries saved yet" message below the table.
2. **Results UI (`ui.js`):** Implement functions to show and hide the results container. Call the hide function when the app initializes so the page starts clean.
3. **Table UI (`table-renderer.js`):** Update your render logic. If your data array is empty, hide the table and show the "No entries" message. If there is data, show the table and hide the message.
4. **Clear Form:** Wire up your "Clear Form" button. When clicked, it must clear all form inputs **and** hide the results container. *Hint: Make sure clearing the form also happens automatically after a successful submission!*
5. **The Storage Module:** Open your storage module (e.g., `data-store.js`). Create and export a new function that generates and returns a unique ID **String**. You must use the exact standard we established in the CFP app. 
    
6. **App Integration:** Open `app.js`. Find where you are creating brand new entries and replace your hardcoded `Date.now()` with a call to your new `generateUniqueId()` function.

> **⚠️ Crucial Debugging Hint: The Data Type Trap** > In previous steps, you used `Date.now()` directly, which saved your old IDs as **Numbers**. However, your new storage function saves them as **Strings**. Furthermore, when you click a button on your table, the browser's `event.target.dataset.id` always extracts a **String**. 
> 
> If you click delete on an older entry, it might fail. Why? Because you should be using strict equality (`===`) in your `.findIndex()` or `.find()` methods just like we did in the Carbon Footprint app, and `1710000000000 === "1710000000000"` evaluates to `false`! 
> 
> *Your fix:* Do not change your code to use loose equality (`==`)! Stick to the strict equality (`===`) standard. Instead, simply clear your Local Storage (using your browser's DevTools under Application > Local Storage) to wipe out the old Number-based entries. From now on, all new entries will be Strings, and your `===` check will work perfectly.

*Test: Load the page (clean). Submit (results/table appear). Click Clear Form (form empties, results vanish). Delete all table rows (table vanishes, "No entries" appears).*
* **Commit with message**: `ui and data polish implemented`


---

## Phase 2: The Edit Setup (Wiring the Form)
To edit an entry, we need to extract its data, put it back into the form, and track its unique ID invisibly.

**Your Requirements:**
1. **The Hidden ID:** Add a hidden `<input>` to your HTML form to hold the entry's ID. Update your "get form data" logic to capture this value (or return `null` if it's empty).
2. **Populate Form (`form-handler.js`):** Create a function (e.g., `populateFormForEdit`) that takes an entry object and plugs its values back into your HTML inputs. It must also set the hidden ID value and change the Submit button text to something like "Update Entry".
3. **The Edit Callback (`app.js` & `table-render.js`):** Create a `handleEditEntry(id)` function in `app.js` that finds the correct object in your array and passes it to your populate function. Pass this callback down to your table renderer and wire it up to your "Edit" buttons using Event Delegation, just like you did for Delete.

*Test: Click the "Edit" button on a table row. The form inputs should instantly fill with that row's data, and the submit button text should change.*
* **Commit with message**: `edit callback and form population implemented`

---
## To take the break:
- Submit the **Commit History URL** to Canvas. (Note: Missing this step results in a -10 point **deduction**).
- Push to GitHub. Make sure your previous commit is visible.
- Add a Submission Comment: "Taking the break, will finish by Thursday Morning!"
---

## Phase 3: The Edit Execution (Update vs. Create)
Your form submission logic can no longer just blindly create new entries. It must check if you are updating an existing one.

**Your Requirements:**
1. **Refactoring Submit (`app.js`):** Inside your `handleFormSubmit` function, write logic to check if an ID exists in the submitted form data.
    * **If it's an Update:** Find the existing object in your array and replace it with the new calculated data. **Crucial:** You must preserve the *original* timestamp and ID of the entry. Do not generate new ones.
    * **If it's a New Entry:** Generate a new ID and timestamp, and push the object to your array as usual.
2. **Form Cleanup:** Update your clear form logic so that it also wipes out the hidden ID value and resets the Submit button text back to its original state.

*Test: Edit an entry, change a value, and hit "Update". The existing row in the table should update (it should not create a duplicate). Submit a brand new entry; it should create a new row.*
* **Commit with message**: `edit execution update vs create implemented`

---

## Phase 4: Planning for Step 5 (`README.md`)
In the final step of this project (Step 5), you will be required to add **one completely new input** to your form and incorporate it into your decision-making logic. 

**Do not code this yet.** We are only planning.

* Open your `README.md` file.
* Add a new section titled `## Step 5 Planning`.
* Answer the following two questions in that section:
    1. **What new input will you add?** (Describe the input, e.g., "A checkbox asking if I have a deadline," or "A number input for my current budget.")
    2. **How will this change your logic?** (Explain how your `decision.js` file will use this new piece of data to alter the final result.)

* **Commit with message**: `step 4 complete and step 5 planned`