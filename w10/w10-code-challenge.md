# Week 10 Challenge: The Logic (CRUD)

**Objective:**
Make the buttons actually work. We will implement this in **Three Phases**. Test each phase before moving to the next!

---

### Setup
Create a new folder in your public repo named `w10`. Copy your files from `w8` into it. Update the title in `index.html` to `CRUD Complete`.

* **Commit with message:** `w10 setup done`

---

### Phase 1: The Delete Feature
Open `app.js`. Find your `handleDelete` function.

**Task:**
1.  Use `orders.findIndex` and `.splice` to remove the item from the array.
2.  Save the updated array to storage.
3.  Re-render the table (Make sure to pass your callbacks again: `{ onDelete: handleDelete, onEdit: handleEdit }`).

**🛑 CHECKPOINT:**
1.  Refresh your page.
2.  Click "Delete" on a row.
3.  **Does the row immediately disappear?**
4.  Refresh the page. **Is the row still gone?**
    * *If yes, Phase 1 is complete!*

* **Commit with message:** `delete feature complete`

---

### Phase 2: The "Populate Form" Feature
Now we handle the "Edit" button. This phase *only* moves data from the array into the form. It does not save changes yet.

**Task:**
1.  **The HTML:** Add `<input type="hidden" id="order-id">` inside your HTML form.
2.  **The JS:** In `app.js`, update `handleEdit(id)` to do the following:
    * **Find the order:** Use `.find()` to grab the specific order object.
    * **Populate visible inputs:** Set the value of your standard text/number inputs.
    * **Handle the Radio Buttons (Size):** You cannot just set a `.value` on a radio group. You must find the specific radio button that matches the order's size and set its `.checked` property to `true`.
      *(Hint: You can use `document.querySelector` with an attribute selector like this: `document.querySelector('input[name="size"][value="' + order.size + '"]').checked = true;`)*
    * **Handle the Checkbox (Gift Wrap):** Similar to radios, checkboxes use `.checked`. Set it equal to your order's boolean value.
    * **Populate hidden input:** Set the value of your **hidden** input (`order-id`) to the order's ID.

**🛑 CHECKPOINT:**
1.  Refresh.
2.  Click "Edit" on a specific order.
3.  Scroll up to the form.
4.  **Did the Size radio button, standard inputs, and Gift Wrap checkbox automatically update to match the order?**
    * *Warning: Do NOT click Submit yet. If you do, it will create a duplicate. We fix that next.*

* **Commit with message:** `edit feature populates form`

---

### Phase 3: The "Update" Logic
Now we fix the Submit button. Currently, it always creates a brand new order. We need to split the logic: Update vs. Create.

**Task:**
Refactor `handleOrderSubmit` in `app.js`.
1.  Get your new `orderData` and calculate the `total` like you normally do.
2.  **Get the hidden ID** from the form (`order-id`).
3.  **The Logic Switch:**
    * **IF the ID exists:** Find the order's index in the array. Update that specific object by merging your new `orderData` and `total` into it (the spread operator `...` is great for this, as it keeps the original ID and timestamp intact!).
    * **ELSE:** Create a completely new order object (with a new ID and timestamp) and push it to the array.
4.  Save to storage, update your displays, and re-render the table.
5.  **CRITICAL CLEANUP:** Clear the hidden ID (`document.getElementById('order-id').value = '';`) and `.reset()` the form at the very end!

**🛑 FINAL CHECKPOINT:**
1.  Refresh.
2.  Click "Edit" on an order. Change the Qty.
3.  Click "Submit".
4.  **Did the row update?** (Success!)
5.  **Did a new row appear?** (Fail - check your `if/else` logic and make sure you are clearing the hidden ID!).
6.  Now, create a *new* order. **Does it work normally?**

* **Commit with message:** `w10 complete`