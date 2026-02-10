# Step 2 - Part A: Logic Refactor
## Upgrading the "Brain" of Your App

Before we build the table or storage, we need to upgrade your `decision.js` module. We want to make your code more professional by using **named helper functions** and returning a detailed, **flat object**.

### 1. The Helper Function Requirement
Refactor your code to use at least one **helper function**.
* **Concept**: A helper function is a small function that does *one specific job* (like checking a threshold or formatting a string). It is **not** exported; it is used internally by your main function.
* **Why?**: This makes your main logic cleaner and easier to read.
* **Task**: Identify a part of your logic (e.g., checking a specific condition) and move it into its own function.

### 2. The Logic Requirement: Use All Inputs
Your decision logic cannot just ignore data. If your form asks for it, your code must use it.
* **Rule**: Ensure that **every single input variable** from your form is used somewhere in your `if/else` statements or your helper functions to determine the final result.

### 3. The Return Object: Decision + Factors (Flat Structure)
Update your main exported function to return a single, flat object. It should not just tell us the *answer* (the decision); it should include the *key data points* (factors) that led to that decision.

**Required Return Structure:**
Do not nest your factors inside a separate object. Return them as top-level properties.
1.  `decision`: The main result (string).
2.  `...factors`: The specific scores, categories, or inputs that influenced the result.

**Example Code:**
> **Note:** The example below follows **Pattern B: The Advisor** (Logic-based). It evaluates specific conditions to determine a category.
> * If you chose **Pattern A (The Scorer)**, your helper function might calculate a number (e.g., `calculateRiskScore`).
> * If you chose **Pattern C (The Summarizer)**, your helper might build a text string (e.g., `formatWarningMessage`).

```javascript
// Helper Function (Not Exported - Used internally)
// Task: Determines urgency based on days remaining (Input 1)
const calculateUrgency = function(daysLeft) {
  if (daysLeft <= 2) {
    return "High";
  } else {
    return "Low";
  }
}

// Main Function (Exported)
export function determineProjectAction(inputs) {
  // 1. Use the Helper to process Input 1 (daysUntilDue)
  const urgencyLevel = calculateUrgency(inputs.daysUntilDue);

  // 2. Logic to determine the decision using ALL inputs
  let action = "Hold";
  
  // Logic uses: Urgency (Input 1), Importance (Input 2), AND Team Size (Input 3)
  if (urgencyLevel === "High" && inputs.importance > 8) {
    // Nested check uses the third input
    if (inputs.teamSize > 3) {
       action = "Delegate to Team"; // High urgency, High importance, Big team
    } else {
       action = "Do It Yourself";   // High urgency, High importance, Small team
    }
  } else if (inputs.importance < 5) {
    action = "Backlog";             // Low importance
  }

  // 3. Return the Decision AND the Factors (Flat Object)
  return {
    decision: action,                   // The Main Result
    urgency: urgencyLevel,              // Factor 1 (Calculated)
    daysRemaining: inputs.daysUntilDue, // Factor 2 (Raw Input)
    importanceScore: inputs.importance, // Factor 3 (Raw Input)
    teamAvailable: inputs.teamSize      // Factor 4 (Raw Input)
  };
}
```
### 4. Testing Your Refactor
* Open app.js and locate your handleFormSubmit.
* console.log the result of your decision function.
* Test: Submit your form.
