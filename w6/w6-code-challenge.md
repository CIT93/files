# Week 6 Checkpoint: The Order History Table

**Objective:**
Upgrade the UI from a simple summary to a full **Order History Table**. You will implement a module to render rows dynamically and use **Event Delegation** to handle deleting items.

**Scenario:**
The manager is happy that the data is saved, but they have a request: *"I can only see the last order! I need to see a list of ALL orders placed today."*

**Your Mission:**
1.  Update your HTML to include a Table structure.
2.  Create a module (`order-list.js`) that loops through your array and creates a table row for every order.
3.  Update `app.js` to render this table every time the app starts or a new order is placed.

---
### Step 1: Setup and Update HTML (The Table Skeleton)
Create a new folder in your public repo named `w6` copy the ending code from `w6a`. Update the title to be `Order History Table` 


Open `index.html`. 
1.  Remove the old `order-summary` div.
2.  Add a new Table structure. Give the `<tbody>` a specific ID so we can target it with JavaScript.

```
html
<div id="order-history-section">
    <h2>Order History</h2>
    <table id="order-table">
        <thead>
            <tr>
                <th>Date</th>
                <th>Qty</th>
                <th>Size</th>
                <th>Total</th>
                <th>Actions</th>
            </tr>
        </thead>
        <tbody id="order-table-body">
            </tbody>
    </table>
</div>
```
**Commit message:** `Step 1 Complete`

### Step 2: Create `order-list.js` (The Render Module)
Create a new file named `order-list.js`. This matches the `renderTable` concept from the lecture.

**Requirements:**
1.  **Select the Tbody:** Get a reference to `document.getElementById('order-table-body')`.
2.  **Export `renderOrders`:** Create and export a function that accepts the `orders` array as a parameter.
3.  **The Logic:**
    * **Clear:** Set the `tbody.innerHTML` to an empty string `''` (this prevents duplicates when re-rendering).
    * **Loop:** Use a loop (like `forEach` or `for...of`) to go through the `orders` array.
    * **Create Row:** Inside the loop, create a new `<tr>` element.
    * **Populate:** Set the `innerHTML` of the row to create `<td>` cells for:
        * Date (Optional: format it nicely)
        * Qty
        * Size
        * Total Price
    * **Append:** Add the new row to the `tbody`.
**Commit message:** `Step 2 Complete`
---

### Step 3: Update `app.js` (Render the List)
Open `app.js`. We need to switch from showing just one result to showing the whole list.

1.  **Import:** Import your new module at the top of the file:
    `import * as orderList from './order-list.js';`
    *(You can remove the old `resultsDisplay` import if you want).*

2.  **Update `init` (Load on Startup):**
    * Inside the `init` function, after you load data from storage, call your new function:
    ```javascript
    if (loadedOrders.length > 0) {
        orders.push(...loadedOrders);
        // Render the full list instead of just the last one
        orderList.renderOrders(orders);
    }
    ```

3.  **Update `handleOrderSubmit` (Update on New Order):**
    * Inside your submit handler, immediately after you save the new order, call `orderList.renderOrders(orders)` to refresh the table.
**Commit message:** `Step 3 Complete`
---

### Step 4: Verify It Works
1.  **Add Orders:** Fill out the form and submit 3 different orders.
2.  **Check Table:** You should see 3 rows in your table.
3.  **Persistence:** Refresh the page.
4.  **Success:** The table should still be there with all 3 rows!


### Optional Challenge: The "Clear Data" Button
If you want an extra challenge, try implementing a button to wipe the history.

**Scenario:**
The manager wants a way to reset the list at the beginning of a new day.

**Requirements:**
1.  **HTML:** Add a `<button id="clear-btn">` below your table.
2.  **JavaScript (`app.js`):**
    * Select the button.
    * Add a `click` event listener.
    * **Inside the listener:**
        1.  Clear the `orders` array (e.g., `orders.length = 0`).
        2.  Clear Local Storage (e.g., `localStorage.removeItem(...)` or save the empty array).
        3.  Update the UI: Call `orderList.renderOrders(orders)` to show the empty table.

**Commit message:** `Step 5 Complete`