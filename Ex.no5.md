Ex06 BMI Calculator
Date: 10-11-2025
AIM
To create a BMI calculator using React Router

ALGORITHM
STEP 1 State Initialization
Manage the current page (Home or Calculator) using React Router.

STEP 2 User Input
Accept weight and height inputs from the user.

STEP 3 BMI Calculation
Calculate the BMI based on user input.

STEP 4 Categorization
Classify the BMI result into categories (Underweight, Normal weight, Overweight, Obesity).

STEP 5 Navigation
Navigate between pages using React Router.

PROGRAM
App.jsx
import "./App.css";
import { Routes, Route, Link } from "react-router-dom";
import Home from "./pages/Home";
import Calculator from "./pages/Calculator";

function App() {
	return (
		<div className="app-root">
			<header className="app-header">
				<h1>BMI Calculator</h1>
				<nav>
					<Link to="/">Home</Link>
					<Link to="/calculator">Calculator</Link>
				</nav>
			</header>

			<main className="app-main">
				<Routes>
					<Route path="/" element={<Home />} />
					<Route path="/calculator" element={<Calculator />} />
				</Routes>
			</main>
		</div>
	);
}

export default App;
Home.jsx
import { Link } from "react-router-dom";
import "./Home.css";

export default function Home() {
	return (
		<div className="home-page">
			<h2>Welcome</h2>
			<p>
				This simple app calculates Body Mass Index (BMI). Click below to
				go to the calculator.
			</p>
			<Link to="/calculator" className="btn">
				Go to Calculator
			</Link>
		</div>
	);
}
Calculator.jsx
import { useState } from "react";
import "./Calculator.css";

function categorize(bmi) {
	if (bmi <= 0 || Number.isNaN(bmi)) return "";
	if (bmi < 18.5) return "Underweight";
	if (bmi < 25) return "Normal weight";
	if (bmi < 30) return "Overweight";
	return "Obesity";
}

export default function Calculator() {
	const [weight, setWeight] = useState(""); // kg
	const [height, setHeight] = useState(""); // cm
	const [result, setResult] = useState(null);

	function calculate(e) {
		e.preventDefault();
		const w = parseFloat(weight);
		const hCm = parseFloat(height);
		if (!w || !hCm || w <= 0 || hCm <= 0) {
			setResult({
				error: "Please enter positive numbers for weight and height.",
			});
			return;
		}
		const h = hCm / 100;
		const bmi = w / (h * h);
		const rounded = Math.round(bmi * 100) / 100;
		setResult({ bmi: rounded, category: categorize(rounded) });
	}

	function reset() {
		setWeight("");
		setHeight("");
		setResult(null);
	}

	return (
		<div className="calculator-page">
			<h2>BMI Calculator</h2>
			<form onSubmit={calculate} className="bmi-form">
				<label>
					Weight (kg)
					<input
						type="number"
						step="any"
						min="0"
						value={weight}
						onChange={(e) => setWeight(e.target.value)}
						placeholder="e.g. 70"
					/>
				</label>

				<label>
					Height (cm)
					<input
						type="number"
						step="any"
						min="0"
						value={height}
						onChange={(e) => setHeight(e.target.value)}
						placeholder="e.g. 175"
					/>
				</label>

				<div className="form-actions">
					<button type="submit" className="btn primary">
						Calculate
					</button>
					<button type="button" className="btn" onClick={reset}>
						Reset
					</button>
				</div>
			</form>

			{result && (
				<section className="result">
					{result.error ? (
						<p className="error">{result.error}</p>
					) : (
						<>
							<p>
								Your BMI is <strong>{result.bmi}</strong>
							</p>
							<p>
								Category: <strong>{result.category}</strong>
							</p>
						</>
					)}
				</section>
			)}
		</div>
	);
}
OUTPUT
alt text

RESULT
The program for creating BMI Calculator using React Router is executed successfully.
