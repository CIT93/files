# Week 8 Challenge: Wiring the Dashboard

**Objective:**
Upgrade your module to render interactive buttons and use Event Delegation to detect clicks.

---

### Step 1: Setup
Create a new folder in your public repo named `w8`. Copy your files from `w6` into it. Update the title in `index.html` to `Wiring the Dashboard`.

* **Commit with message:** `w8 setup done`

---

### Step 2: Upgrade Data (Add Unique ID)
Currently, our order objects only have `qty`, `size`, and `price`. To delete or edit a specific order later, we need a unique ID.

1.  **Clear Old Data:** Since your old orders don't have IDs, they will break the new features.
    * Open your browser's DevTools (F12) -> Application Tab -> Local Storage.
    * Right-click your data key (e.g., `orders`) and select **Delete**.
    * Refresh the page (Table should be empty).
2.  **Update `app.js`:**
    * Find your `handleOrderSubmit` function.
    * Inside the new order object, add an `id` property using `Date.now()`.

```javascript
// app.js - inside handleOrderSubmit
const newOrder = {
    id: Date.now().toString(), // <--- ADD THIS LINE (Unique ID based on time)
    qty: qty,
    size: size,
    totalPrice: totalPrice,
    // ... any other properties
};
```

* **Commit with message:** `unique id added`

---

### Step 3: Update HTML (Table Header)
Since we are adding a new column of buttons to our table, we need to update the header so everything aligns correctly.

1.  Open `index.html`.
2.  Find your `<thead>` section inside the table.
3.  Add a new `<th>` for "Actions" at the end of the row.

---

### Step 4: Add Buttons to the Table
Update `order-list.js`. Add the Edit and Delete buttons to your row HTML.
* **Requirement:** Use classes `edit-btn` and `delete-btn`. Use `data-id="${order.id}"`.

**🛑 CHECKPOINT:**
1.  Save your code.
2.  Add a new order (so you have data with an ID).
3.  **Do you see the two buttons on the row?** If yes, proceed.

* **Commit with message:** `add btn to tbl`

---

### Step 5: Implement Event Delegation (The Listener)

**The Problem:**
We created the "Edit" and "Delete" buttons dynamically using JavaScript. Because they didn't exist when the page first loaded, we can't attach an `addEventListener` directly to them.

**The Solution:**
We use **Event Delegation**. Instead of listening to every single button, we attach *one* listener to the parent element (the `tbody`). When you click a button inside the table, the "click event" bubbles up to the parent, and we catch it there!



**Open `order-list.js` and follow these steps:**

#### 5.1 Create the Listener (and Test It!)
First, let's just make sure we can detect the clicks. We won't connect `app.js` yet.

**Add this code to `order-list.js` (before the export):**

```javascript
const tableBody = document.getElementById('order-table-body');

tableBody.addEventListener('click', function(event) {
    const target = event.target;
    
    // 1. Get the ID from the button that was clicked
    const id = target.dataset.id;

    // 2. Guard Clause: If they clicked a row (white space) but NOT a button, 
    // there will be no ID. So we stop the function immediately.
    if (!id) return;

    // 3. Temporary Test: Log the ID to prove it works!
    console.log("Clicked button with ID:", id); 
});
```

**🛑 CHECKPOINT:**
1.  Refresh your page.
2.  Click the "Delete" button on any row.
3.  **Do you see the ID in the console?**
    * *Yes:* Great! The wiring works. Now let's connect it to the real logic.
    * *No:* Check your `data-id` attribute in the HTML string from Step 4.

* **Commit with message:** `table event listener wired`

---

### Step 6: Connect to `app.js` (The Controller)

Now that we know the table is listening, we need to send that command to `app.js` where the data lives.

#### 6.1 Create the Functions in `app.js`
Open `app.js`. Create two functions to handle the actions. For now, they will just log a message.

```javascript
// app.js

const handleDelete = function(id) {
    console.log("App.js: Requesting delete for order", id);
};

const handleEdit = function(id) {
    console.log("App.js: Requesting edit for order", id);
};
```

#### 6.2 Pass Functions to the Module
Update your `orderList.renderOrders` calls (in `init` and `handleOrderSubmit`) to pass these new functions.

```javascript
// app.js
orderList.renderOrders(orders, {
    onDelete: handleDelete,
    onEdit: handleEdit
});
```

---

### Step 7: Complete the Wiring (Final Update)

Now `app.js` is sending the functions, but `order-list.js` isn't catching them yet.

**Open `order-list.js` one last time.**

#### 7.1 Setup the Module Scope
Add this variable at the very top of the file to store the functions.

```javascript
// order-list.js top of file
let moduleCallbacks = {};
```

#### 7.2 Receive the Functions
Update your `renderOrders` function to accept the callbacks and save them.

```javascript
export const renderOrders = function(orders, callbacks) {
    // Save the callbacks for later
    moduleCallbacks = callbacks;
    
    // ... rest of your code ...
};
```

#### 7.3 Update the Listener Logic
Go back to the event listener you wrote in Step 5. **Remove** the temporary `console.log("Clicked button...")`.

Now, you must write the logic to handle the specific buttons. You need to check the class name of the target to decide which function to call.

**Write the code to satisfy these requirements:**

1.  **Check for Delete:** Write an `if` statement to check if the `target` has the class `delete-btn`.
    * *Action:* If true, call `moduleCallbacks.onDelete` and pass the `id`.
2.  **Check for Edit:** Write an `if` statement to check if the `target` has the class `edit-btn`.
    * *Action:* If true, call `moduleCallbacks.onEdit` and pass the `id`.

> **Hint:** Remember to check if the function exists before calling it (e.g., `if (moduleCallbacks.onDelete) ...`).

**🛑 FINAL CHECKPOINT:**
1.  Refresh.
2.  Click "Delete".
3.  **Does the console say "App.js: Requesting delete..."?**
    * If yes, you have successfully wired your modules!

* **Commit with message:** `w8 complete`