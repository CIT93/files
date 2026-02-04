# Week 6 Attendance Challenge: Persistent Orders

**Objective:**
Your T-Shirt Shop is doing great, but the manager noticed a critical bug: **If they refresh the browser page, all the order history disappears!** Your job is to implement **Local Storage** so the orders stay saved even after a page reload.

**Scenario:**
You need to create a new module named `order-storage.js` to handle saving and loading data. Then, connect it to your main app so it saves every time a new order is placed and loads previous orders when the app starts.

---

### Step 1: Setup
Create a new folder in your public repo named `w6a` copy the ending code from `w4`. Update the title to be `Persistent Orders` 

**Commit message:** `Step 1 Complete`

### Step 2: Display Results
If you didn't get this done in Week 4 You Code then you will need to do it now. 

Create a new file named `results-display.js`. Its job is to control the results HTML display. This is from Week 4 You Code:

**1. Update your HTML (The Output Area)**
Replace your old `<div id="order-summary">...</div>` at the bottom of `index.html` with this new version. Notice that it starts hidden (`display: none`) and has specific `<span>` tags with IDs so we can inject our data directly into them.

```
html
<div id="order-summary" style="display: none;">
    <h2>Order Success!</h2>
    <p><strong>Total Cost:</strong> $<span id="display-total"></span></p>
    <p><strong>Details:</strong> <span id="display-qty"></span> <span id="display-size"></span> T-Shirt(s)</p>
    <p><strong>Gift Wrap:</strong> <span id="display-gift"></span></p>
</div>
```
**2. Create results-display.js Create a new file named results-display.js. Its job is to control that HTML.**
* References: Get references to the `order-summary` container and the 4 span IDs inside it.
* Export `displayOrder`: Create a function that accepts an order object.
    * Update the `textContent` of the spans using data from the object (`order.totalPrice`, `order.qty`, etc.).
    * Logic: For gift wrap, if/else to display "Yes" if true, or "No" if false.
    * Visibility: Set the container's style to `display: 'block'`.
    * Inside `handleOrderSubmit`, remove any old console.log or text updates.
    * Call `resultsDisplay.displayOrder(newOrder)`

**3. Connect it to app.js**
* Import the module: `import * as resultsDisplay from './results-display.js'`;
* Test it: Fill out the form and submit. You should see your new display appear!

**Commit message:** `Step 2 Complete`

### Step 3: Create the Storage Module (`order-storage.js`)
Create a new file named `order-storage.js`. Use the code from the lecture as a template, but adapt it for our order system.

**Requirements:**
1.  **Key:** Define a constant `LOCAL_STORAGE_KEY` (e.g., `'tshirt_orders_data'`).
2.  **Save Function:** Export a function named `saveOrders`.
    * It should accept the `orders` array as a parameter.
    * Use `JSON.stringify` to convert the array to a string.
    * Use `localStorage.setItem` to save it.
    * *Bonus:* Wrap it in a `try...catch` block to handle errors.
3.  **Load Function:** Export a function named `loadOrders`.
    * Use `localStorage.getItem` to retrieve the string.
    * If data exists, use `JSON.parse` to turn it back into an array and return it.
    * If no data exists (it's null), return an empty array `[]`.

**Commit message:** `Step  3 Complete`

---

### Step 4: Load Data on Startup (`app.js`)
Open `app.js`. We need to check for saved orders as soon as the app launches.

**Requirements:**
1.  **Import:** Import everything from your new module.
    * `import * as orderStorage from './order-storage.js';`
2.  **Update `init` Function:**
    * Inside your `init` function (before setting event listeners), call `orderStorage.loadOrders()`.
    * **Check:** If the returned array has items (length > 0), add them to your main `orders` array.
    * **The Trick:** Since `orders` is a `const` array, you can't reassign it (`orders = loaded`). Instead, use the **Spread Operator** to push the items
    * *Optional:* Log "Orders loaded" to the console.

---
**Commit message:** `Step 4 Complete`

### Step 5: Save Data on Submit (`app.js`)
We need to update storage every time the list changes.

**Requirements:**
1.  Find your `handleOrderSubmit` function.
2.  Look for the line where you `.push(newOrder)` into the array.
3.  Immediately after that line, call your new save function

---

### Step 6: Verify It Works
1.  Open your browser **Console** and the **Application** tab (look for "Local Storage" on the left).
2.  Place an order (e.g., 5 Small Shirts).
3.  **Check:** You should see a key named `tshirt_orders_data` appear in the Application tab.
4.  **Refresh:** Refresh the page.
5.  **Check:** Look at the Console. The `orders` array should **not** be empty—it should still contain the order you just placed!

---




