#  DMA - Decision Making App Step 1
## JavaScript Implementation
The carbon footprint will be your guide to implement the following, make sure you do the steps in order of the instructions and commits.

### `app.js` Setup
* **Create File**: In your `my-app/step1` folder, create a new file named `app.js`.
* **Link File**: Update your `index.html` to include the `<script>` tag pointing to this file.
    * **Hint**: Do not forget the `defer` attribute so the HTML loads before the JS runs.
* **Code & Test**: Write the following JavaScript, saving and testing in the browser console as you go:
    - **Sanity Check**: Add a `console.log('App Loaded')` at the top of the file to confirm the connection is working.
    - **Global Data**: Create an array literal to hold all submitted decision entries. Name this variable specifically for your app (e.g., `gymSessions`, `budgetEntries`, `gameHighScores`).
    - **DOM References**: Setup references (variables) for your HTML Form and your "Clear/Reset" button.
    - **Event Handlers (Skeleton)**:
        * Create a function named `handleFormSubmit`. For now, just have it `console.log` a message like "Form Submitted".
        * Create a function named `handleClearForm`. For now, just have it `console.log` a message like "Clear Button Clicked".
    - **Init Function**:
        * Create an `init()` function.
        * Inside `init`, attach event listeners to your Form (listen for `submit`) and your Reset Button (listen for `click`), passing in the handler functions you created above.
    - **Start the App**: Attach an event listener to the `document` that waits for `DOMContentLoaded` to call your `init()` function.
* **Commit with message**: `app.js started`

## ☕ The “Thursday Morning Break” Option

Feeling the burn? If you have completed everything above, you may pause here.

### To take the break:
- Submit the **URL to your commit history**
- Make sure the previous commit is visible and pushed to github
- Add a submission comment saying:

> Taking the break, will finish by Thursday Morning!

*(If you are not taking the break, continue below.)*

### `form-handler.js` Setup
* **Convert to Module**: In your `index.html`, locate your script tag for `app.js`.
    * Add `type="module"` to the opening tag.
* **Create File**: In your `my-app/step1` folder, create a new file named `form-handler.js`.
* **Code & Test**: Write the following JavaScript logic. Since this is a module, remember to `export` the functions you need to use in other files.
    - **DOM References**: At the top of the file, create references to your Input fields (so you can read their values) and your Form (so you can reset it).
    - **`getFormInputs` Function**:
        * Create and export a function named `getFormInputs()`.
        * Inside, create a helper function to handle your Radio buttons or Checkboxes (e.g., to loop through and find which one is checked).
        * Return an object literal containing the values from your form. Ensure the property names match your specific decision topic.
    - **`clearForm` Function**:
        * Create and export a function named `clearForm()`.
        * Inside, use the form's `.reset()` method.
        * `console.log` a relevant message (e.g., "Form cleared").

### `app.js` Update
* **Imports**: At the top of `app.js`, import the `getFormInputs` and `clearForm` functions from `./form-handler.js`.
* **Update `handleFormSubmit`**:
    * Inside your existing handler, ensure you are preventing the default form submission behavior (`e.preventDefault()`).
    * Call `getFormInputs()` and store the result in a variable.
    * `console.log` the returned object to ensure your data is being captured correctly.
* **Commit with message**: `form-handler.js started`

## `decision.js`
In the Carbon Footprint app, we had `calculator.js`—a specific file dedicated to doing the math. For your personal app, you need a similar "brain," but instead of calculating carbon, it evaluates your decision.

* **Create File**: In your `my-app/step1` folder, create a new file named `decision.js` (or something specific like `workout-logic.js`).
* **Code & Test**:
    * **The Goal**: Create and export a function that takes your **form data** as input and returns a **result object**.
    * **The "Pure Function" Rule**: This function **must not** touch the DOM. No `document.getElementById`, no updating HTML. It strictly takes data in and sends data out.

### Instructions:
1.  **Define the Function**: Create and export a function (e.g., `calculateDecision`, `evaluateChoice`).
2.  **Define Inputs**: This function should accept one parameter: the object you created in `form-handler.js`.
3.  **Write the Logic**: You must write code that processes the inputs. **You must use at least one conditional statement (`if/else`)** to determine the outcome.
    * *Choose a pattern below, or create your own:*
    * **Pattern A: The Scorer (Math-based)**
        * *Logic:* Calculate a score, then use `if/else` to assign a rating.
        * *Example Return:* `return { score: 85, feedback: "High Priority - Do it now!" }`
    * **Pattern B: The Advisor (Logic-based)**
        * *Logic:* Check specific inputs (e.g., weather, mood) to determine a category.
        * *Example Return:* `return { suggestion: "Read a Book", icon: "📖", style: "relaxing" }`
    * **Pattern C: The Conditional Summarizer (Text-based)**
        * *Logic:* Build a summary string, but use `if/else` to modify it based on conditions (e.g., adding a warning if cost is high).
        * *Example Return:* `return { summary: "Buy the headphones (Warning: Over Budget)", alert: true }`
4.  **Return the Result**: Ensure your function returns an **Object Literal**, not just a string or number.

* **Commit with message**: `decision logic created`
> **Future-Proofing Your Logic (Architectural Note):**
> For Step 1, it is acceptable to write all your logic inside this one main function. However, good developers plan for growth. As you write your code, ask yourself: *"Is this doing too much?"*
>
> If your function gets longer than 15-20 lines, or if you are calculating two completely different things (like 'Cost' vs. 'Risk'), consider how you might break those out into smaller helper functions in future weeks (just like we did with `determineHouseSizePts` in the Carbon Footprint app).

### `app.js` Update
* **Import**: Import your new function at the top of `app.js`.
* **Update `handleFormSubmit`**:
    * Call your new decision function, passing in the data you got from `getFormInputs`.
    * Store the returned object in a variable.
    * `console.log` the returned object to verify your logic works.
* **Commit with message**: `return decision object`


