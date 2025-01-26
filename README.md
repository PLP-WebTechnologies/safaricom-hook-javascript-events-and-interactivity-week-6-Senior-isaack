

## Objective:
Build a functional webpage that incorporates event handling, interactive elements, and form validation using JavaScript.

## Requirements:

Interactive Button with onclick:

Add a button that toggles the background color of the webpage between two colors.
Slider with Real-Time Feedback (oninput):

Add a slider that adjusts the size of a paragraph text dynamically.
Modal with Event Listeners:

Create a modal that displays when a button is clicked and hides when the user clicks a close button.

## Form with Validation:

Include a form with the following fields:
Name (required, minimum 3 characters).
Email (valid email format).
Password (minimum 8 characters, at least one uppercase letter and one number).
Display error messages if validation fails.
Prevent form submission if there are errors.
Bonus (Optional):

Add a dropdown menu that displays a custom message when the selected option changes (onchange).






<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interactive Webpage</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      transition: background-color 0.5s;
    }

    #text-paragraph {
      font-size: 20px;
      margin-top: 20px;
    }

    #modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      justify-content: center;
      align-items: center;
    }

    #modal-content {
      background-color: white;
      padding: 20px;
      border-radius: 5px;
      width: 300px;
      text-align: center;
    }

    #error-message {
      color: red;
      font-size: 12px;
      margin-top: 10px;
    }

    select {
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <!-- Interactive Button to Toggle Background Color -->
  <button onclick="toggleBackgroundColor()">Toggle Background Color</button>

  <!-- Slider to Adjust Paragraph Text Size -->
  <input type="range" id="text-size-slider" min="10" max="50" value="20" oninput="adjustTextSize()" />
  <p id="text-paragraph">This is a paragraph with adjustable text size. Move the slider!</p>

  <!-- Modal Trigger and Modal -->
  <button onclick="openModal()">Open Modal</button>
  <div id="modal">
    <div id="modal-content">
      <h2>Modal Title</h2>
      <p>This is a simple modal.</p>
      <button onclick="closeModal()">Close</button>
    </div>
  </div>

  <!-- Form with Validation -->
  <form id="user-form" onsubmit="return validateForm(event)">
    <div>
      <label for="name">Name:</label>
      <input type="text" id="name" name="name" required minlength="3">
    </div>
    <div>
      <label for="email">Email:</label>
      <input type="email" id="email" name="email" required>
    </div>
    <div>
      <label for="password">Password:</label>
      <input type="password" id="password" name="password" required>
    </div>
    <button type="submit">Submit</button>
    <div id="error-message"></div>
  </form>

  <!-- Dropdown for Custom Message -->
  <select onchange="displayDropdownMessage()">
    <option value="">Select an option</option>
    <option value="Option 1">Option 1</option>
    <option value="Option 2">Option 2</option>
    <option value="Option 3">Option 3</option>
  </select>
  <p id="dropdown-message"></p>

  <script>
    // Toggle background color between two colors
    let isBackgroundColorBlue = true;
    function toggleBackgroundColor() {
      document.body.style.backgroundColor = isBackgroundColorBlue ? 'lightcoral' : 'lightblue';
      isBackgroundColorBlue = !isBackgroundColorBlue;
    }

    // Adjust text size of paragraph with slider
    function adjustTextSize() {
      const textSize = document.getElementById("text-size-slider").value;
      document.getElementById("text-paragraph").style.fontSize = textSize + "px";
    }

    // Open modal
    function openModal() {
      document.getElementById("modal").style.display = "flex";
    }

    // Close modal
    function closeModal() {
      document.getElementById("modal").style.display = "none";
    }

    // Form Validation
    function validateForm(event) {
      event.preventDefault();
      const name = document.getElementById('name').value;
      const email = document.getElementById('email').value;
      const password = document.getElementById('password').value;
      let errorMessage = '';

      // Name validation
      if (name.length < 3) {
        errorMessage += 'Name must be at least 3 characters long.<br>';
      }

      // Email validation
      const emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$/;
      if (!emailPattern.test(email)) {
        errorMessage += 'Please enter a valid email address.<br>';
      }

      // Password validation
      const passwordPattern = /^(?=.*[A-Z])(?=.*[0-9]).{8,}$/;
      if (!passwordPattern.test(password)) {
        errorMessage += 'Password must be at least 8 characters long, with at least one uppercase letter and one number.<br>';
      }

      // Display error messages if any
      if (errorMessage) {
        document.getElementById('error-message').innerHTML = errorMessage;
      } else {
        alert('Form submitted successfully!');
        document.getElementById('user-form').reset();
        document.getElementById('error-message').innerHTML = '';
      }
    }

    // Display message based on dropdown selection
    function displayDropdownMessage() {
      const dropdown = document.querySelector('select');
      const message = dropdown.value ? `You selected ${dropdown.value}.` : '';
      document.getElementById('dropdown-message').innerText = message;
    }
  </script>
</body>
</html>

