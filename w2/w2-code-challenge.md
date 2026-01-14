# Challenge: Refactoring – The Shopping Cart

## Objective
You will take the **Click Counter** code from Section 2.2 and refactor (modify) it to create a **Shopping Cart** calculator.

---

## Scenario
The client loves the button interaction you built, but they don't need a click counter—they need a checkout system!  
They have provided new HTML with different ID names. Your job is to update your JavaScript to match their new HTML and logic.

---

## Step 1: The New HTML

In your public repo (ex riow-pub) create a new folder named w2, it will be at the same level as w1 from last week. Copy the ending files from the 2.2 code along. No need to copy the app2-1.js file. 

Replace the body of your `index.html` with the following code.

⚠️ **Important:** Notice the ID names have changed to match the new context.

```html
<body>
    <h1>My Shopping Cart</h1>
    
    <p id="total-display">Current Total: $0</p>
    
    <button id="add-item-btn">Add Item ($15)</button>
</body>
```

### ✅ Step 1 Checkpoint
Once done, review your HTML carefully:
- Confirm the IDs match **exactly**
- Refresh the browser to ensure no errors appear

Before moving on to the next step, commit your changes using this message:

**Commit message:** `Step 1 Complete`

---

## Step 2: Refactor Your JavaScript

Open your `app.js`. It is currently looking for the old IDs and using old variable names. You need to fix it.

---

### 2.1 Update DOM Selectors (Crucial Step)

Your code is currently trying to find:

```js
document.getElementById("output-message")
```

That ID no longer exists.

**Update your `const` selectors** to grab the new elements:
- `total-display`
- `add-item-btn`

💡 *Tip:* You should also rename your JavaScript variables to match (for example, `totalDisplayElement`).

#### ✅ Step 2.1 Checkpoint
- No `null` errors in the Console
- Button click successfully triggers your function

Commit before moving on:

**Commit message:** `Step 2.1 Complete`

---

### 2.2 Variable Cleanup

- Delete the `userName` variable.
- Rename `clickCount` to `totalCost`.
- Initialize `totalCost` to `0`.
- Add a new `const` variable named `itemPrice` and set it to `15`.

📏 **Rio's Rule:** Use `const` unless the value needs to change!

#### ✅ Step 2.2 Checkpoint
- No reference errors
- Variables are clearly named and readable

Commit before continuing:

**Commit message:** `Step 2.2 Complete`

---

### 2.3 Update the Function Logic

#### The Math
- Add `itemPrice` to `totalCost` every time the button is clicked
- Use the compound assignment operator (`+=`)

#### The Message
- Display the updated total using a template string:

```
Current Total: $<totalCost>
```

#### The Decision (`if / else`)
- If `totalCost >= 60`:
  - Change text color to `red`
  - Append `(Over Budget!)`
- Else:
  - Change text color to `black` (or green)

#### ✅ Step 2.3 Checkpoint
- Total updates correctly
- Budget logic behaves as expected

Commit your work:

**Commit message:** `Step 2.3 Complete`

---

### 2.4 Update the Event Listener

Ensure your event listener is attached to your **new button variable name**.

#### ✅ Step 2.4 Checkpoint
- Button responds on every click
- No console errors

Final commit for this step:

**Commit message:** `Step 2.4 Complete`

---

## 🆘 Hints Guide (If You Get Stuck)

### ❓ Nothing happens when I click the button!
- Check your **IDs**
- Verify `getElementById()` matches the HTML exactly
- Look for this error in the Console:
  > `Cannot read properties of null`

---

### ❓ The total says `$151515` instead of `$45`
- Check your **data types**
- Strings concatenate; numbers add
- `itemPrice` should be a number, not a string

---

### ❓ ReferenceError: `clickCount` is not defined
- Ensure **every instance** of `clickCount` was renamed to `totalCost`

---

### ❓ The text color isn't changing
- Verify your condition:

```js
if (totalCost >= 60)
```

- Make sure you're not using old variable names
