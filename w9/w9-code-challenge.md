# Week 9 Challenge: The Logic (CRUD)

**Objective:**
Make the buttons actually work. We will implement this in **Three Phases**. Test each phase before moving to the next!

---

### Phase 1: The Delete Feature
Open `app.js`. Find your `handleDelete` function.

**Task:**
1.  Use `orders.findIndex` and `.splice` to remove the item from the array.
2.  Save to storage.
3.  Re-render the table.

**🛑 CHECKPOINT:**
1.  Refresh your page.
2.  Click "Delete" on a row.
3.  **Does the row immediately disappear?**
4.  Refresh the page. **Is the row still gone?**
    * *If yes, Phase 1 is complete!*

---

### Phase 2: The "Populate Form" Feature
Now we handle the "Edit" button. This phase *only* moves data into the form. It does not save changes yet.

**Task:**
1.  Add `<input type="hidden" id="order-id">` to your HTML form.
2.  In `app.js`, update `handleEdit(id)`:
    * Find the order object.
    * Set the value of your visible inputs (Qty, Size).
    * Set the value of your **hidden** input (`order-id`).

**🛑 CHECKPOINT:**
1.  Refresh.
2.  Click "Edit" on a specific order (e.g., the one with "Large" size).
3.  Scroll up to the form.
4.  **Did the "Size" dropdown automatically change to "Large"?**
    * *Warning: Do NOT click Submit yet. If you do, it will create a duplicate. We fix that next.*

---

### Phase 3: The "Update" Logic
Now we fix the Submit button.

**Task:**
Refactor `handleOrderSubmit` in `app.js`.
1.  Get the ID from the hidden input.
2.  **IF** the ID exists -> Update the existing object in the array.
3.  **ELSE** -> Create a new object and push it.
4.  **Important:** Clear the hidden ID at the end of the function!

**🛑 FINAL CHECKPOINT:**
1.  Refresh.
2.  Click "Edit" on an order. Change the Qty to "100".
3.  Click "Submit".
4.  **Did the row update to 100?** (Success!)
5.  **Did a new row appear?** (Fail - check your `if/else` logic).
6.  Now, create a *new* order. **Does it work normally?**