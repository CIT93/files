# Decision Making App - Step 3
## Managing Data: Deleting Entries & Module Callbacks

In Step 3, we are going to add the ability to delete entries from your history. To do this properly, we will use **Event Delegation** and a **Callback Architecture** so your table module can communicate with your main application logic.

## Setup
* **Create Folder**: Inside your `my-apps` folder, create a new folder named `step3`.
* **Copy Files**: Copy **all** files from your `step2` folder and paste them into your new `step3` folder.
* **Work Here**: Close any open files from step 2 and open the files in `step3` to begin working.

---

## 1. The Callback Architecture Setup
Right now, your table renders the HTML buttons, but `app.js` holds the data. We need to pass a "callback function" from `app.js` into your table module so the table knows what to do when a button is clicked.

* **Open `table-render.js`**:
    * At the top of your file (outside any function), declare a variable to store your callbacks:
      `let _currentCallbacks = {};`
    * Update your `renderTable` function signature to accept a second parameter:
      `export const renderTable = function(data, callbacks) { ... }`
    * Inside `renderTable`, immediately save those callbacks:
      `_currentCallbacks = callbacks;`
* **Open `app.js`**:
    * Create an empty placeholder function for deleting:
      ```javascript
      const handleDeleteEntry = function(id) {
          console.log(`Delete clicked for ID: ${id}`);
      }
      ```
    * Find everywhere you call `renderTable(...)` (in `init` and `handleFormSubmit`) and update it to pass an object containing your function:
      `renderTable(myData, { onDelete: handleDeleteEntry });`
* **Commit with message**: `callback architecture setup`

---

## 2. Event Delegation (`table-render.js`)
Since our Delete buttons are created dynamically, we cannot attach event listeners directly to them. We must listen to their parent container (the table body).

* **Open `table-render.js`**:
    * Create a new function named `handleTableClick(event)`.
    * Inside this function:
        1. Get the target element: `const target = event.target;`
        2. Check if the clicked element is a delete button:
           ```javascript
           if (target.classList.contains('delete') && typeof _currentCallbacks.onDelete === 'function') {
               // Extract the ID from the data-id attribute
               const id = target.dataset.id;
               // Call the function we passed from app.js
               _currentCallbacks.onDelete(id);
           }
           ```
    * At the bottom of your file, attach this function to your `<tbody>` element:
      `document.querySelector('#history-list').addEventListener('click', handleTableClick);`
* **Test**:
    1. Ensure you have data in your table.
    2. Click a "Delete" button.
    3. **Success**: You should see "Delete clicked for ID: [your-id]" in your console.
* **Commit with message**: `event delegation for table clicks added`

---

## 3. The Delete Logic (`app.js`)
Now that the click is successfully communicating the `id` back to `app.js`, we need to actually remove that item from our array and LocalStorage.

* **Open `app.js`**:
    * Update your `handleDeleteEntry(id)` function:
        1. **Find the Index**: Use `.findIndex()` to locate the object in your `myData` array where the `entry.id` matches the `id` passed in. *(Note: Watch your data types! `dataset.id` is a string, but your `Date.now()` ID is a number. Use `parseInt()` or `==` if needed).*
        2. **Remove the Item**: If the index is found (`!== -1`), remove it using `.splice(index, 1)`.
        3. **Save and Render**: Call your storage function to save the updated array, and call `renderTable` to visually update the screen.
           ```javascript
           saveToLS(myData);
           renderTable(myData, { onDelete: handleDeleteEntry });
           ```
* **Test**:
    1. Add a few entries to your app.
    2. Click the "Delete" button on one of them.
    3. **Success**: The row should disappear immediately.
    4. Refresh the page. **Success**: The row should still be gone.
* **Commit with message**: `delete logic complete`