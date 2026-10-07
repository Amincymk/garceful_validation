# garceful_validation
PROJECT TITLE: Graceful Date Input Validator

DESCRIPTION:
This project is a small web page that accepts a date from the user and validates it using JavaScript. The program handles valid input and several types of invalid input without crashing.

The application does not use any live service or API.

FILES:

1. index.html
2. script.js
3. README.md

---

## FILE 1: index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Date Validator</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f4f4;
            padding: 40px;
        }

        .container {
            max-width: 500px;
            margin: auto;
            background: white;
            padding: 25px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        input {
            width: 100%;
            padding: 12px;
            margin: 10px 0;
            box-sizing: border-box;
        }

        button {
            width: 100%;
            padding: 12px;
            background: #2563eb;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
        }

        button:hover {
            background: #1d4ed8;
        }

        #message {
            margin-top: 20px;
            padding: 12px;
            border-radius: 5px;
        }

        .success {
            background: #dcfce7;
            color: #166534;
        }

        .error {
            background: #fee2e2;
            color: #991b1b;
        }
    </style>
</head>

<body>

    <div class="container">
        <h1>Date Validator</h1>

        <p>Enter a date in YYYY-MM-DD format.</p>

        <input
            type="text"
            id="dateInput"
            placeholder="Example: 2026-10-07"
        >

        <button onclick="handleDateInput()">
            Validate Date
        </button>

        <div id="message"></div>
    </div>

    <script src="script.js"></script>

</body>
</html>
```

---

## FILE 2: script.js

```javascript
function parseDate(input) {
    if (typeof input !== "string") {
        throw new Error("Invalid input type");
    }

    if (input.trim() === "") {
        throw new Error("Empty input");
    }

    if (input.length > 50) {
        throw new Error("Input is too long");
    }

    const datePattern = /^\d{4}-\d{2}-\d{2}$/;

    if (!datePattern.test(input)) {
        throw new Error("Invalid date format");
    }

    const parts = input.split("-");

    const year = Number(parts[0]);
    const month = Number(parts[1]);
    const day = Number(parts[2]);

    const date = new Date(year, month - 1, day);

    if (
        date.getFullYear() !== year ||
        date.getMonth() !== month - 1 ||
        date.getDate() !== day
    ) {
        throw new Error("Invalid calendar date");
    }

    return date;
}


function handleDateInput() {
    const inputElement = document.getElementById("dateInput");
    const messageElement = document.getElementById("message");

    try {
        const input = inputElement.value;

        const date = parseDate(input);

        messageElement.textContent =
            "Valid date: " + date.toDateString();

        messageElement.className = "success";

    } catch (error) {

        console.error("Date validation failed:", error.message);

        messageElement.textContent =
            "Please enter a valid date in YYYY-MM-DD format.";

        messageElement.className = "error";
    }
}
```

---

## FILE 3: README.md

# Graceful Date Input Validator

## Project Description

This project is a small JavaScript web application that accepts a date from a user and validates it.

The application demonstrates graceful error handling. Instead of allowing the program to crash or showing technical error messages to the user, it gives a simple message explaining how the input should be corrected.

No live API, database, or external service is used.

## Technologies

* HTML
* CSS
* JavaScript
* Browser Console

## How It Works

The user enters a date in this format:

YYYY-MM-DD

Example:

2026-10-07

The `parseDate()` function checks the input before attempting to create a JavaScript Date object.

If something goes wrong, the function throws an error.

The `handleDateInput()` function catches the error using `try...catch`.

The user receives a safe and understandable message while the technical error is written to the browser console for debugging.

## Failure Cases

### 1. Empty Input

Input:

""

What the user sees:

"Please enter a valid date in YYYY-MM-DD format."

What is logged:

"Empty input"

How the user can fix it:

Enter a date such as:

2026-10-07

---

### 2. Whitespace Input

Input:

"   "

What the user sees:

"Please enter a valid date in YYYY-MM-DD format."

What is logged:

"Empty input"

How the user can fix it:

Remove the spaces and enter a valid date.

---

### 3. Very Long Input

Example:

"2026-10-07-abcdefghijklmnopqrstuvwxyz-1234567890"

What the user sees:

"Please enter a valid date in YYYY-MM-DD format."

What is logged:

"Input is too long"

How the user can fix it:

Enter only the date using the YYYY-MM-DD format.

---

### 4. Unexpected Input Type

Example:

A number, object, array, or other non-string value passed directly to `parseDate()`.

What the user sees:

"Please enter a valid date in YYYY-MM-DD format."

What is logged:

"Invalid input type"

How the user can fix it:

Enter the date as text.

---

### 5. Incorrect Date Format

Example:

"07/10/2026"

What the user sees:

"Please enter a valid date in YYYY-MM-DD format."

What is logged:

"Invalid date format"

How the user can fix it:

Use:

2026-10-07

---

### 6. Invalid Calendar Date

Example:

"2026-02-31"

What the user sees:

"Please enter a valid date in YYYY-MM-DD format."

What is logged:

"Invalid calendar date"

How the user can fix it:

Enter a real calendar date, such as:

2026-02-28

---

### 7. Random Text

Example:

"hello"

What the user sees:

"Please enter a valid date in YYYY-MM-DD format."

What is logged:

"Invalid date format"

How the user can fix it:

Enter a date using YYYY-MM-DD.

## Security and Privacy

The application does not send user input to an external server.

Technical error details are not displayed to the user.

Only a general error message is shown on the page.

Detailed error information is logged to the browser console for debugging.

This prevents internal implementation details from being exposed to normal users.

## Testing

The following tests should be performed:

| Test            | Input                   | Expected Result |
| --------------- | ----------------------- | --------------- |
| Valid date      | 2026-10-07              | Accepted        |
| Empty input     | ""                      | Error message   |
| Spaces          | "   "                   | Error message   |
| Very long input | More than 50 characters | Error message   |
| Wrong type      | Number/object           | Error handled   |
| Wrong format    | 07/10/2026              | Error message   |
| Invalid date    | 2026-02-31              | Error message   |
| Random text     | hello                   | Error message   |

## Manual Testing

1. Open `index.html` in a browser.
2. Enter `2026-10-07`.
3. Click "Validate Date".
4. Confirm that the date is accepted.
5. Delete the input and click the button.
6. Confirm that an error message appears.
7. Try `07/10/2026`.
8. Try `2026-02-31`.
9. Try a very long string.
10. Open Developer Tools and select the Console tab.
11. Confirm that technical error information is logged there.

## Expected Behaviour

The application should never crash because of invalid user input.

For valid input, it displays the validated date.

For invalid input, it displays:

"Please enter a valid date in YYYY-MM-DD format."

Technical details are kept in the console rather than being shown to the user.

## Conclusion

This project demonstrates graceful error handling by validating user input before processing it and using `try...catch` to handle failures. The user receives a clear message explaining what kind of input is expected, while technical error information is kept out of the interface.
