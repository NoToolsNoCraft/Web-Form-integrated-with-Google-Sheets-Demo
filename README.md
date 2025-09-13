Live web app link: https://notoolsnocraft.github.io/Web-Form-integrated-with-Google-Sheets-Demo/

The Web app (pure front end HTML, CSS and JS) is basically a form component where the visitors are asked to fill their data such as their name, email and a message. You may find the whole front end code in the index.html document.

The submit button then sends the data to the integrated Google Sheet document.

The integration with Google Sheets works in a way that a Google Apps Script is set up. You may find the script I've used in the repository under the same name. The script is using the Google Sheet ID in order to connect with it.

# Web Form Integrated with Google Sheets

**Live Demo:** [Click here to try the app](https://notoolsnocraft.github.io/Web-Form-integrated-with-Google-Sheets-Demo/)

This project demonstrates how to connect a **pure front-end HTML/CSS/JS form** with a **Google Sheet** using **Google Apps Script**.  
When a visitor submits the form, their data (name, email, message) is sent directly into a spreadsheet, creating a lightweight backend-less data collection tool.

---

## 📂 Project Structure

- **`index.html`**  
  The complete front end of the application.  
  Key sections:
  - **Form** (`<form id="dataForm">`)  
    Collects the visitor’s **name, email, and message**.
  - **JavaScript Fetch** (`fetch(...)`)  
    Sends form data as JSON to the deployed Google Apps Script web app URL.  
    - Uses `method: "POST"`  
    - Sends JSON body  
    - Handles success/error responses and updates the `.status` div accordingly.
  - **Status messages**  
    Displays submission progress (`Submitting data...`, ✅ success, ❌ error).

- **`Google Apps Script (Code.gs)`**  
  Handles requests from the front end:
  - **`doPost(e)`** → Parses JSON payload, appends a row (`Timestamp, Name, Email, Message`) to the sheet.  
  - **`doGet(e)`** → Returns a simple message to confirm the web app is deployed.  

---

## ⚙️ How It Works (Flow)

1. User fills out the form in `index.html`.  
2. JavaScript serializes the data into JSON.  
3. A `fetch` request sends the data to the Google Apps Script web app.  
4. The Apps Script `doPost()` function writes the data into the Google Sheet.  
5. The server responds with a success/error JSON message.  
6. The UI updates the status message accordingly.  

---

## 🚀 Setup Guide

Follow these steps to recreate the integration:

### 1. Prepare Google Sheet
1. Go to [Google Sheets](https://sheets.google.com).  
2. Create a new sheet.  
3. Rename the first tab to **Sheet1**.  
4. Optionally, add column headers: `Timestamp | Name | Email | Message`.  
5. Copy the **Spreadsheet ID** from the URL.  
   - Example URL:  
     ```
     https://docs.google.com/spreadsheets/d/1H2peYFnGowbHrxpghL9dfJeewDuC3uFiwKeaVpq3t6E/edit
     ```  
     The ID is the long string between `/d/` and `/edit`.

---

### 2. Create Google Apps Script
1. Go to [Google Apps Script](https://script.google.com).  
2. Create a **new project**.  
3. Replace the default code with the provided Google Apps Script in the repository

Replace "YOUR_SHEET_ID" with your actual Google Sheet ID.

3. Deploy as Web App

In Apps Script, go to Deploy → New deployment.

Select Web app.

Under Execute as, choose Me.

Under Who has access, choose Anyone (or Anyone with the link).

Click Deploy and copy the Web App URL.

4. Update Front End

In index.html, find the fetch(...) call:

fetch("YOUR_WEB_APP_URL", {
  method: "POST",
  body: JSON.stringify(data),
  headers: {
    'Content-Type': 'text/plain'
  }
})


Replace "YOUR_WEB_APP_URL" with the URL from step 3.

5. Host the Front End

Option A: Open index.html locally in your browser.

Option B: Host it with GitHub Pages
, Netlify, or any static hosting service.

In this repository, GitHub Pages is already enabled:
👉 Live Demo

✅ Example Use Cases

Contact forms without a backend server

Feedback collection

Event registration

Simple surveys

🔒 Notes on Security

This setup is best suited for small projects or prototypes.

Since the script is open to "anyone with the link", consider:

Adding basic spam filtering (e.g., reCAPTCHA).

Restricting access to authenticated Google accounts if needed.

Regularly monitoring your sheet for unwanted submissions.


