# Week 5 Attendance 
## Decision Making App - Doc and UI

Your goal for this project is to build a web application that helps you make personal decisions. You'll create an app where you can input details about a decision important to your own life, see your current submission, and eventually manage a history of past decisions. This project will reinforce key web development patterns like modular JavaScript and storing data right in your browser. Since it's about your life, your app will be truly unique!

## Step 1: Files and Doc
* Create a new folder inside your **private** repo named `my-app`. This should be located at the root of your repo.
* Inside `my-app`, create another folder called `step1`. All files for this work will go directly into this `my-app/step1` folder.
* Inside `step1`, create a new `README.md` file. 
* Use the following H1 for the first line: `# My Decision Making App`
* Then, include the following sections using H2 `##`:
    - **Project Title**: Name your project.
    - **Description**: Briefly explain what your specific decision app is designed to do (e.g., "This app helps me track and analyze my decisions about [e.g., choosing a university major, deciding on a new tech gadget, planning my personal finances]"). It takes my current energy level, the day of the week, and the outside temperature as inputs to generate a personalized workout suggestion.")
    - **Input Types Used**: List the specific types of inputs you included in your form (e.g., "text for 'Language Name', number for 'Learning Curve (1-5)', checkbox for 'Open Source?'"). Briefly explain why these inputs are relevant to your decision.
    - **Color Palette**: Describe your chosen color palette (e.g., "A calming green and blue palette with a contrasting orange for buttons") and list the main hex codes you used (e.g., #RRGGBB).
        * Choose 3-5 colors that go well together. Think about a main background color, a text color, and perhaps an accent color for buttons or highlights. Choose colors that reflect the theme of your decision app.
            * **Required Format**:
                * `#HexCode` - Usage (e.g., Main Background)
                * `#HexCode` - Usage (e.g., Primary Text)
                * `#HexCode` - Usage (e.g., Submit Button)
            * Helpful Color Palette Resources:
                - [Coolors.co](https://coolors.co/)
                - [Paletton.com](http://paletton.com/)
                - [Adobe Color](https://color.adobe.com/)
    - **Commit with message**: `files and doc started`

## Step 2: HTML
* **Setup**: Copy the `index.html` file from your ending code for the Carbon Footprint (4.2) exercise and paste it into your `my-app/step1` folder.
* **Customization**: All Carbon Footprint-specific content, text, and elements must be completely customized for your decision-making topic.
    - Update page headings, paragraph content, and the submit button text.
    - Update HTML attributes to match your new data: `id`, `name`, `value`, `for`, and `placeholder` text.
* **Decision Input Form**:
    - Update the form to include at least 3-4 distinct input fields relevant to your decision. You must show variety by including:
        * **Type A**: At least one Text input (e.g., "Decision Topic", "Option Name") OR Number input (e.g., "Priority Score 1-10", "Cost").
        * **Type B**: At least one Checkbox (e.g., "Urgent?", "Requires Research?") OR Radio Button set (e.g., "Impact: Low / Medium / High").
        * **Optional**: Feel free to add `<textarea>` (for Pros/Cons) or `<select>` dropdowns (for Categories).
    - **Important**: Rename all `id` and `name` attributes to be specific to your new data (e.g., change `id="firstname"` to `id="decision-name"`).
* **Decision Display Section**:
    - Update the existing output/display section (table or div) with headers that match your new decision data.
- **Commit with message**: `html updated`


## Step 3: CSS
* **Setup**: Copy the `style.css` file from your ending code for the Carbon Footprint (4.2) exercise and paste it into your `my-app/step1` folder.
* Ensure your `index.html` is correctly linked to this new sheet: `<link rel="stylesheet" href="style.css" />`.
* Apply your chosen colors strategically throughout your styling. You can copy the CSS from 4.2 as a base, but you must update the colors to match your selected palette.
    - Add basic global styles for the `body` (e.g., font-family, font-size, line-height, text color, and background-color).
    - Style the form elements: background colors, input borders, and button colors (normal and hover states).
- **Commit with message**: `css updated`

