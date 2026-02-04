# Week 6 Checkpoint: Order History & Deletion

**Objective:**
Upgrade the UI from a simple summary to a full **Order History Table**. You will implement a module to render rows dynamically and use **Event Delegation** to handle deleting items.

**Scenario:**
The manager loves that the data is saved, but they have a new request: *"I can only see the last order! I need to see a list of ALL orders placed today. Also, sometimes I make a mistake, so I need a delete button."*

**Your Mission:**
1.  Replace your "Single Result Display" with a **Table** that lists every order in the array.
2.  Add a **Delete Button** to each row to remove unwanted orders.

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
Create a new file named `order-list.js`. This will handle building the table rows.

**Requirements:**
1.  **Select the Tbody:** Get a reference to `document.getElementById('order-table-body')`.
2.  **Export `renderOrders`:** Create a function that accepts the `orders` array.
3.  **The Loop:**
    * Clear the `tbody` innerHTML first (so you don't get duplicates).
    * Loop through the `orders` array.
    * For each order, create a `<tr>` (row).
    * **The Content:** Inside the row, create `<td>` cells for Date, Qty, Size, and Total Price.
    * **The Delete Button:** In the last cell, add a button with a class of `delete-btn` and a `data-id` attribute set to the order's timestamp (or unique ID).
    * Append the row to the `tbody`.

**Code Snippet for the Row Content:**
```js
// Inside your template literal for the row:
`<td>${order.qty}</td>
 <td>${order.size}</td>
 <td>$${order.totalPrice}</td>
 <td>
    <button class="delete-btn" data-id="${order.timestamp}">Delete</button>
 </td>`
```
**Commit message:** `Step 2 Complete`

 ### Step 3: Update `app.js` (Render the List)
Open `app.js`. We need to switch from showing just one result to showing the whole list.

1.  **Import:** Import your new module at the top of the file:
    `import * as orderList from './order-list.js';`
2.  **Update `init`:**
    * Inside the `init` function, after you load data from storage, replace the old `resultsDisplay` call with: `orderList.renderOrders(orders);`
3.  **Update `handleOrderSubmit`:**
    * Inside your submit handler, whenever a new order is added, call `orderList.renderOrders(orders)` to refresh the table immediately.

**Commit message:** `Step 3 Complete`

---

### Step 4: Implement Delete (Event Delegation)
Now for the "Delete" logic inside `app.js`.

**1. Create the `deleteOrder` function:**
Create a function named `deleteOrder` that accepts an `id` (timestamp) as a parameter.
* **Find:** Use `.findIndex()` to find the index of the order with that timestamp in your `orders` array.
* **Remove:** If found, remove it using `.splice(index, 1)`.
* **Update:** Immediately call `orderList.renderOrders(orders)` to update the screen and `orderStorage.saveOrders(orders)` to update the database.

**2. Add the Event Listener (Delegation):**
* In your `init` function, select the **Table Body** element (`tbody`).
* Add a `click` event listener to it.
* **The Check:** Inside the listener, check `if (event.target.classList.contains('delete-btn'))`.
* **The Action:** If true, get the id from `event.target.dataset.id` and call your `deleteOrder(id)` function.

**Commit message:** `Step 4 Complete`

---

### Step 5: Verify It Works
1.  **Populate:** Add 3 different orders to your list.
2.  **Persistence:** Refresh the page. You should see a table with 3 rows.
3.  **Delete:** Click the "Delete" button on the **middle** row.
4.  **Check:**
    * The row should vanish immediately.
    * Refresh the page again. The deleted order should *not* come back.
