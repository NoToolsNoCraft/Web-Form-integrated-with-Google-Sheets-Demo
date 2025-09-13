# Web Form Integrated with Google Sheets

**Live Demo:** [Click here to try the app](https://notoolsnocraft.github.io/Web-Form-integrated-with-Google-Sheets-Demo/)

This project demonstrates how to connect a **pure front-end HTML/CSS/JS form** with a **Google Sheet** using **Google Apps Script**. When a visitor submits the form, their data (name, email, message) is sent directly into a spreadsheet, creating a lightweight, backend-less data collection tool.

---

## 📂 Project Structure

This project is made up of two key parts that work together to collect and store data.

* **`index.html`**
    The front-end of the application, which includes:
    * **The Form**: An `<form id="dataForm">` to collect the visitor's **name, email, and message**.
    * **JavaScript `fetch`**: This handles the submission, sending the form data as a JSON payload to the deployed Google Apps Script web app URL using the `POST` method. It also manages success and error responses.
    * **Status Messages**: A `.status` div that displays real-time messages like `Submitting data...`, ✅ **Success**, or ❌ **Error**.

* **`Google Apps Script (Code.gs)`**
    This script acts as the backend, handling requests from the front-end.
    * `doPost(e)`: This function is the core of the script. It receives the JSON data, parses it, and appends a new row to the Google Sheet with a `Timestamp`, `Name`, `Email`, and `Message`.
    * `doGet(e)`: A simple function that returns a message to confirm the web app is deployed and working.

---

## ⚙️ How It Works (Flow)

The process is a simple, six-step journey from the user's browser to your Google Sheet.

1.  A user fills out and submits the form in `index.html`.
2.  The JavaScript code serializes the data into a JSON object.
3.  A `fetch` request sends this data to your deployed Google Apps Script web app.
4.  The Apps Script's `doPost()` function receives the request and writes the data into the designated Google Sheet.
5.  The script responds with a success or error JSON message.
6.  The browser's JavaScript receives this response and updates the UI's status message accordingly.

---

## 🚀 Setup Guide

To get this project running yourself, follow these steps.

### 1. Prepare Your Google Sheet

1.  Go to [Google Sheets](https://sheets.google.com) and create a new sheet.
2.  Rename the first tab to **Sheet1**.
3.  **Optional:** Add column headers like `Timestamp | Name | Email | Message` for clarity.
4.  **Copy the Spreadsheet ID** from the URL. This is the long string of letters and numbers located between `/d/` and `/edit` in your sheet's URL. For example:
    `https://docs.google.com/spreadsheets/d/1H2peYFnGowbHrxpghL9dfJeewDuC3uFiwKeaVpq3t6E/edit`

### 2. Create and Deploy the Google Apps Script

1.  Go to [Google Apps Script](https://script.google.com) and create a **new project**.
2.  Replace the default code with the provided `Google Apps Script (Code.gs)` from this repository.
3.  **Important:** In the script, replace `"YOUR_SHEET_ID"` with the Spreadsheet ID you copied in the previous step.
4.  Deploy the script as a web app:
    * Click **Deploy** → **New deployment**.
    * Select **Web app**.
    * Under "Execute as," choose **Me**.
    * Under "Who has access," choose **Anyone** (or **Anyone with the link**).
    * Click **Deploy** and **copy the Web App URL**. This is the link your form will send data to.

### 3. Update the Front-End

1.  Open the `index.html` file in your preferred code editor.
2.  Find the `fetch(...)` call and replace `"YOUR_WEB_APP_URL"` with the Web App URL you copied in the previous step.

### 4. Host the Front-End

* **Option A:** Simply open `index.html` locally in your web browser.
* **Option B:** Host the file using a service like **GitHub Pages**, **Netlify**, or any other static hosting service. This repository already has GitHub Pages enabled.

---

## ✅ Example Use Cases

This simple yet powerful setup is perfect for:

* Contact forms without a backend server
* Feedback collection
* Event registration
* Simple surveys

---

## 🔒 Notes on Security

This setup is ideal for small projects or prototypes, but keep these security considerations in mind:

* Because the script is open to "anyone," consider adding basic spam filtering like **reCAPTCHA** to your form.
* If needed, you can restrict access to authenticated Google accounts to prevent unwanted submissions.
* Regularly monitor your Google Sheet for any unwanted submissions.
