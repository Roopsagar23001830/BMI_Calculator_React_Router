# Ex06 BMI Calculator
## Date: 29-05-2025

## AIM
To develop a responsive and interactive Body Mass Index (BMI) Calculator using React that allows users to input their height and weight, and calculates their BMI to categorize their health status (e.g., Underweight, Normal, Overweight, Obese).

## DESIGN STEPS

### STEP 1: Initialize React Project

<li>Create a new React app using create-react-app.</li>
<li>Install React Router using:</li>
npm install react-router-dom

### STEP 2: Set Up Routing

Create routing structure with react-router-dom:

<li>Home route (/) – Intro or Navigation</li>

<li>BMI Calculator route (/bmi)</li>

<li>Result route (/result)</li>

### STEP 3: Design the BMI Form Page

<li>Create a form to accept Height (in cm or m) and Weight (in kg).</li>

<li>On form submit, navigate to the result page with entered values via URL query params or context/state.</li>

## STEP 4: Handle Input Validation

<li>Check if height and weight are valid numbers.</li>

<li>Optionally, show error messages for invalid inputs.</li>

### STEP 5: Perform BMI Calculation

<li>In the result component:

<li>Extract height and weight from the route (URL or passed state).</li>

<li>Apply the BMI formula:</li>

![image](https://github.com/user-attachments/assets/ec785506-c96b-489e-8783-fb1a5d36101a)
​
 
<li>Convert height from cm to m if needed.</li></li>

### STEP 6: Display Result

<li>Show calculated BMI.</li>

<li>Show category based on BMI range:

<li>Underweight, Normal, Overweight, Obese, etc.</li></li>

### STEP 7: Navigation Options

<li>Provide a button to go back to the BMI form to calculate again.</li>

### STEP 8: Enhancements

<li>Add styling using CSS or Tailwind.</li>

## PROGRAM

app.js
// App.js
// BMI Calculator using React
// © 2025 Roop Sagar S L – Register No: 212223040175. All rights reserved.
// Author: Roop Sagar S L – Project Submission for BMI Calculator

import React from "react";
import { BrowserRouter as Router, Routes, Route, Link, useLocation, useNavigate } from "react-router-dom";
import "./App.css";

function Home() {
  return (
    <div className="container">
      <h1>BMI Calculator</h1>
      <p className="author">By Roop Sagar S L<br />Reg No: 212223040175</p>
      <Link to="/bmi" className="btn">Start Calculation</Link>
    </div>
  );
}

function BMICalculator() {
  const navigate = useNavigate();
  const [height, setHeight] = React.useState("");
  const [weight, setWeight] = React.useState("");
  const [error, setError] = React.useState("");

  const handleSubmit = (e) => {
    e.preventDefault();
    const h = parseFloat(height);
    const w = parseFloat(weight);

    if (!h || !w || h <= 0 || w <= 0) {
      setError("Please enter valid height and weight");
      return;
    }

    setError("");
    navigate(`/result?height=${h}&weight=${w}`);
  };

  return (
    <div className="container">
      <h2>Enter your details</h2>
      <form onSubmit={handleSubmit}>
        <input type="number" placeholder="Height (cm)" value={height} onChange={(e) => setHeight(e.target.value)} />
        <input type="number" placeholder="Weight (kg)" value={weight} onChange={(e) => setWeight(e.target.value)} />
        {error && <p className="error">{error}</p>}
        <button type="submit" className="btn">Calculate BMI</button>
      </form>
      <p className="author">Created by Roop Sagar S L<br />Reg No: 212223040175</p>
    </div>
  );
}

function Result() {
  const location = useLocation();
  const navigate = useNavigate();
  const params = new URLSearchParams(location.search);
  const height = parseFloat(params.get("height"));
  const weight = parseFloat(params.get("weight"));

  const bmi = weight / Math.pow(height / 100, 2);
  let category = "";

  if (bmi < 18.5) category = "Underweight";
  else if (bmi < 24.9) category = "Normal weight";
  else if (bmi < 29.9) category = "Overweight";
  else category = "Obese";

  return (
    <div className="container">
      <h2>Your BMI Result</h2>
      <p><strong>BMI:</strong> {bmi.toFixed(2)}</p>
      <p><strong>Status:</strong> {category}</p>
      <button className="btn" onClick={() => navigate("/bmi")}>Calculate Again</button>
      <p className="author">Developed by Roop Sagar S L<br />Reg No: 212223040175</p>
    </div>
  );
}

export default function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/bmi" element={<BMICalculator />} />
        <Route path="/result" element={<Result />} />
      </Routes>
    </Router>
  );
}

```

app.css
```
/* App.css */
/* BMI Calculator React Project */
/* © 2025 Roop Sagar. All rights reserved. */

body {
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
  background: #f5f5f5;
}

.container {
  max-width: 400px;
  margin: 50px auto;
  padding: 2rem;
  background: #fff;
  border-radius: 10px;
  text-align: center;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

h1, h2 {
  margin-bottom: 1rem;
  color: #333;
}

input {
  width: 90%;
  padding: 10px;
  margin: 0.5rem 0;
  border: 1px solid #ccc;
  border-radius: 6px;
}

.btn {
  display: inline-block;
  padding: 10px 20px;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  margin-top: 1rem;
  text-decoration: none;
}

.btn:hover {
  background: #0056b3;
}

.error {
  color: red;
  margin-top: 0.5rem;
}

.author {
  margin-top: 1.5rem;
  font-size: 0.9rem;
  color: #666;
  font-style: italic;
}

```



## OUTPUT

![Screenshot 2025-05-29 160520](https://github.com/user-attachments/assets/2b05a171-3939-400f-82b7-9121d54314ef)

![Screenshot 2025-05-29 160527](https://github.com/user-attachments/assets/66655b70-8389-4189-a51e-9d5afb33aa78)


## RESULT
The BMI Calculator successfully takes user input for height and weight, performs the BMI calculation in real-time using React state and event handling, and displays the BMI value along with the corresponding health category.
