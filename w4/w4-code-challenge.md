# Week 4 Challenge: The Order History

**Objective:**
Upgrade your "Custom T-Shirt" app! You will practice using **Arrays** to store data, the **Spread Operator** to merge objects, and creating a dedicated **Calculation Module**.

**Scenario:**
The store manager is happy with the form, but they have two new requests:
1.  **No Math:** They are tired of calculating the cost manually. (T-Shirts are $15, Gift Wrap is $2). 
2.  **No Memory:** Currently, the app forgets the previous order as soon as a new one is placed. We need to store a history of **all** orders placed in the current session.

---
### Step 1: Setup
Create a new folder in your public repo named `w4` copy the ending code from `w3`. Update the title to be `The Custom Order Form` 
**Commit message:** `Step 1 Complete`

### Step 2: Create `price-calculator.js`
Create a new file named `price-calculator.js`. This module's job is to handle the math so your main app doesn't have to.

**Requirements:**
1.  **Constants:** Define a price for a shirt (e.g., `15`) and a price for gift wrap (e.g., `2`).
    * Make sure to use **camelCase** our standard naming convention for variables,
2.  **Export a Function:** Create and export a function named `calculateTotal`.
    * **Input:** It should accept the `orderData` object (the one from your handler) as a parameter.
    * **Logic:** Calculate the total: `(Qty * Shirt Price) + (Gift Wrap Price if selected)`.
        * Keyword in this requirement `if`.
    * **Output:** Return an object containing the key `totalPrice` (e.g., `{ totalPrice: 47 }`).
**Commit message:** `Step 2 Complete`

---

### Step 3: Refactor `app.js` (The Array & Spread)
Open your `app.js`. We need to change how we handle the "Submit" event.

---
**Requirements:**
1.  **Import:** Import everything from your new calculator module. 
    * *Hint: Use the same style as Week 3:* `import * as priceCalculator from './price-calculator.js';`
2.  **The Array:** At the top of your file (before the functions), create a `const` array named `orders`. Initialize it as empty `[]`.
    * *Note: We use `const` because the array reference doesn't change, even though we push items into it.*
3.  **Update `handleOrderSubmit`:**
    * **Calculate:** Call your new calculator function (`priceCalculator.calculateTotal(...)`), passing in the form data. Save the result to a variable.
    * **Merge (The Spread Operator):** Create a new object named `newOrder`. Use the spread operator (`...`) to combine:
        * The original `orderData`.
        * The new `calculatedPrice` data.
        * A `timestamp` (use `new Date().toISOString()`).
    * **Store:** `push` this new object into your `orders` array.
    * **Verify:** `console.log` the `orders` array.


### Step 3: Verify Your Work
1.  Open your browser **Console**.
2.  Fill out the form (e.g., 2 Shirts, Gift Wrapped) and click "Place Order".
3.  Fill out the form **again** with different values and click "Place Order".
4.  **Success:** You should see an Array in the console that grows.
    * Click 1: `Array(1)` -> `[{ qty: 2, size: "Medium", totalPrice: 32, ... }]`
    * Click 2: `Array(2)` -> Contains both the first and second order.

**Commit message:** `Step 3 Complete`

---

### Step 4: Implement the Display Module (`results-display.js`) Optional (or earn a late pass)
We need to separate our DOM updates from our main logic, just like we did in the Carbon Footprint app.

**1. Update your HTML (The Output Area)**
Replace your old `<div id="order-summary">...</div>` at the bottom of `index.html` with this new version. Notice that it starts hidden (`display: none`) and has specific `<span>` tags with IDs so we can inject our data directly into them.

```html
<div id="order-summary" style="display: none;">
    <h2>Order Success!</h2>
    <p><strong>Total Cost:</strong> $<span id="display-total"></span></p>
    <p><strong>Details:</strong> <span id="display-qty"></span> <span id="display-size"></span> T-Shirt(s)</p>
    <p><strong>Gift Wrap:</strong> <span id="display-gift"></span></p>
</div>
```
