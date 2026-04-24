# Decision Making App - Step 6
## Custom Form Validation

In Step 6, we are taking complete control of the user experience. By default, the browser tries to validate forms for us using HTML attributes like `required` or `min`. While helpful, the browser's default error popups are often ugly, hard to style, and inconsistent across different devices. 

Your goal is to disable the browser's default behavior and implement the custom JavaScript validation plan you designed in your Step 5 `README.md`.

## Setup
* **Create Folder**: Inside your `my-apps` folder, create a new folder named `step6`.
* **Copy Files**: Copy **all** files from your `step5` folder into your new `step6` folder.
* **Work Here**: Ensure you are only editing the files in the `step6` directory.
* **Commit with message**: `step 6 setup complete`

---

## Phase 1: HTML Preparation (Taking Control)
Before we can write our custom validation, we need to tell the browser to back off and let our JavaScript do the heavy lifting.

**Your Requirements:**
1. **Disable Browser Validation:** Open your `index.html` and add the `novalidate` attribute to your main `<form>` tag.
2. **Strip HTML Constraints:** Go through every `<input>`, `<select>`, or `<textarea>` in your form. Remove any HTML validation attributes (e.g., remove `required`, `min`, `max`, `minlength`). 
3. **Error Containers:** Add a placeholder element (like an empty `<span>` or `<div>` with a specific class/id) below or next to each input field. This is where your custom error messages will eventually appear.

*Test: Try to submit an empty form. Because you removed `required` and added `novalidate`, the form should attempt to process the blank data without the browser stopping you (which might break your app or save blank entries—that is exactly what we will fix in Phase 2!).*
* **Commit with message**: `novalidate added and html constraints removed`

---

## Phase 2: Implementing the Validation Logic
Refer back to the plan you wrote in your `README.md` during Step 5. It is time to enforce those boundary rules using JavaScript.

**Your Requirements:**
1. **The Validation Check**: Inside your form submission logic—*before* you try to create or update an entry—you must check the incoming data against your rules.
2. **Apply Your Rules:** Write logic to check for the boundaries you planned. Needs to be at least 3 inputs
    * *Examples:* Is the text string empty? Is the number less than 0? Was a radio button left unselected?
3. **Display Errors:** If a piece of data fails your check, you must prevent the form from submitting (do not create/update the array) and inject your planned Error Message into the DOM using the error containers you built in Phase 1.
4. **Clear Errors:** If the user fixes their mistake and resubmits, your code must clear the old error messages from the screen.

*Test: Leave your form entirely blank and hit submit. Your custom error messages should appear. Fill out the form perfectly and hit submit. The errors should disappear and the data should save properly.*
* **Commit with message**: `custom javascript form validation implemented`

---

## Phase 3: UI Polish (The Error State)
A good application clearly communicates state to the user.

**Your Requirements:**
1. **Visual Cues:** Add CSS to ensure your error messages stand out (e.g., red text, bold font). 
2. **The "Clear Form" Reset:** Update your "Clear Form" button logic. If a user clicks "Clear Form," it must also wipe out any visible error messages currently on the screen.

*Test: Trigger an error intentionally. Click your "Clear Form" button. The form should empty out, the results should hide, and the error messages should vanish.*
* **Commit with message**: `error state styling and clear form logic updated`