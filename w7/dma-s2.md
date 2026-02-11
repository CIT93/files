# Decision Making App - Step 2
## Refactoring, Persistence, and Rendering

In Step 2, we will make the app "real" by saving data to LocalStorage and rendering a history of your decisions. We have structured this so you can **test** your progress after every single step.

## Setup
* **Create Folder**: Inside your `my-apps` folder, create a new folder named `step2`.
* **Copy Files**: Copy **all** files from your `step1` folder and paste them into your new `step2` folder.
* **Work Here**: Close any open files from step 1 and open the files in `step2` to begin working.
* **Commit with message**: `setup step2 done`
---

## 1. Logic Cleanup: Data Structure
**Goal**: We need to attach a unique ID and a timestamp to every decision so we can track it later.
* **Open `app.js`**:
    * Locate your `handleFormSubmit` function.
    * **Update Entry Creation**: Combine your inputs and decision into one object, adding an ID and Timestamp:
      ```javascript
      const newEntry = {
          id: Date.now(), 
          timestamp: new Date().toISOString(),
          ...inputs,
          ...decision
      }
      ```
    * **Update Array**: Push this new object into your global array (e.g., `myData.push(newEntry)`).
* **Test**:
    1. Add `console.log(myData)` after the push.
    2. Submit the form in the browser.
    3. **Success**: Expand the array in the console. Your object should now have `id`, `timestamp`, `inputs`, and `decision` properties.
* **Commit with message**: `array update and id added`

---


## 2. UI Module: `ui.js` (Immediate Feedback)
**Goal**: Standardize how we show the *current* decision result (the text above the form).
* **Create/Rename**:
    * If you have `results-display.js`, rename it to `ui.js`.
    * If not, create a new file `ui.js`.
* **Code (`ui.js`)**:
    * Export a function named `renderDecision(decisionObj)`.
    * Inside, select the DOM element for your result display (e.g., `#decision-output`) and update its text/HTML with your decision.
* **Connect (`app.js`)**:
    * Import `renderDecision` from `./ui.js`.
    * Call `renderDecision(decisionObj)` inside `handleFormSubmit`.
* **Test**:
    1. Submit the form.
    2. **Success**: The text on the screen updates immediately with your new result.
* **Commit with message**: `ui module standardized`

---

## 3. HTML Update: The Table
**Goal**: Create the skeleton for our history list.
* **Open `index.html`**:
    * Below your "Decision Result" section, add a `<table>`.
    * Add a `<thead>` with `<tr>` and `<th>` elements matching your data (e.g., `<th>Date</th>`, `<th>Score</th>`).
    * **Crucial**: Add a final header `<th>Actions</th>`.
    * Add an empty `<tbody>` with an `id` (e.g., `id="history-list"`).
* **Test**:
    1. View your page.
    2. **Success**: You should see the table headers (but no data rows yet).
* **Commit with message**: `table html added`

---
### To take the break:
- Submit the **Commit History URL** to Canvas. (Note: Missing this step results in a -10 point **deduction**).
- Push to GitHub. Make sure your previous commit is visible.
- Add a Submission Comment: "Taking the break, will finish by Thursday Morning!"
---

## 4. Data Store Module: `data-store.js`
**Goal**: Save data to the browser so it survives a refresh.
* **Create File**: Create `data-store.js` in your `step2` folder.
* **Code (`data-store.js`)**:
    * Define a unique Key: `const MY_DATA = "decision-app-data";` (Use a name specific to your app).
    * Export `saveToLS(array)`: Stringify and save to LocalStorage.
    * Export `getFromLS()`: Parse and return data (or return `[]` if null).
* **Connect (`app.js`)**:
    * Import `saveToLS` and `getFromLS`.
    * **Global Variable**: Initialize your global array using `getFromLS()` (instead of `[]`).
    * **Handle Submit**: Immediately after pushing to your array, call `saveToLS(myData)`.
* **Test**:
    1. Submit your form.
    2. Refresh the page.
    3. Open DevTools $\rightarrow$ Application Tab $\rightarrow$ LocalStorage.
    4. **Success**: You should see your data saved there, even after a refresh.
* **Commit with message**: `data persistence implemented`

---

## 5. Table Render Module: `table-render.js`
**Goal**: specific module to render the table rows and buttons.
* **Create File**: Create `table-render.js`.
* **Code (`table-render.js`)**:
    * Export a function `renderTable(data)`.
    * Select your `<tbody>` and clear `innerHTML`.
    * Loop through `data`. For each item, build a `<tr>` with `<td>`s for your specific data.
    * **Actions Column**: In the last `<td>`, use this exact HTML:
      ```html
      <td class="action-cell">
          <button class="action-button edit" data-id="${entry.id}">Edit</button>
          <button class="action-button delete" data-id="${entry.id}">Delete</button>
      </td>
      ```
    * Append the rows to the `<tbody>`.
* **Connect (`app.js`)**:
    * Import `renderTable`.
    * **Update `init`**: Call `renderTable(myData)` on startup.
    * **Update `handleFormSubmit`**:
        1. Call `renderTable(myData)` after saving.
        2. **Reset Form**: Call `clearForm()` (from `form-handler.js`) to clear inputs.
* **Test**:
    1. Reload the page. **Success**: Previous data should appear in the table.
    2. Submit new data. **Success**: It appears instantly, and the form clears.
* **Commit with message**: `render the table implemented`