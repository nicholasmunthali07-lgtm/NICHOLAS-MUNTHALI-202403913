
html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quadratic Solver & Grading System</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        .container {
            max-width: 600px;
            margin: auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
        }
        input[type="number"] {
            width: 100%;
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #3e8e41;
        }
        #quadraticResult, #gradingResult {
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            background-color: #f9f9f9;
        }
        .error-message {
            color: red;
            font-size: 0.8em;
            margin-top: 5px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Quadratic Equation Solver</h2>
        <p>Enter the coefficients a, b, and c for the quadratic equation ax² + bx + c = 0</p>

        <div class="form-group">
            <label for="a">a:</label>
            <input type="number" id="a" name="a">
            <div id="aError" class="error-message"></div>
        </div>

        <div class="form-group">
            <label for="b">b:</label>
            <input type="number" id="b" name="b">
            <div id="bError" class="error-message"></div>
        </div>

        <div class="form-group">
            <label for="c">c:</label>
            <input type="number" id="c" name="c">
            <div id="cError" class="error-message"></div>
        </div>

        <button onclick="solveQuadratic()">Compute</button>
        <button onclick="clearQuadratic()">Reset</button>

        <div id="quadraticResult"></div>

        <h2>Grading System</h2>
        <p>Enter your score (0-100) to get your grade.</p>

        <div class="form-group">
            <label for="score">Score:</label>
            <input type="number" id="score" name="score">
            <div id="scoreError" class="error-message"></div>
        </div>

        <button onclick="calculateGrade()">Compute</button>
        <button onclick="clearGrade()">Reset</button>

        <div id="gradingResult"></div>
    </div>

    <script>
        function solveQuadratic() {
            const a = parseFloat(document.getElementById('a').value);
            const b = parseFloat(document.getElementById('b').value);
            const c = parseFloat(document.getElementById('c').value);

            document.getElementById('aError').innerText = "";
            document.getElementById('bError').innerText = "";
            document.getElementById('cError').innerText = "";

            if (isNaN(a) || isNaN(b) || isNaN(c)) {
                if (isNaN(a)) document.getElementById('aError').innerText = "Please enter a valid number for a.";
                if (isNaN(b)) document.getElementById('bError').innerText = "Please enter a valid number for b.";
                if (isNaN(c)) document.getElementById('cError').innerText = "Please enter a valid number for c.";
                return;
            }

            if (a === 0) {
                document.getElementById('aError').innerText = "a cannot be zero.";
                return;
            }

            const discriminant = b * b - 4 * a * c;
            let roots = "";
            let root1 = null;
            let root2 = null;

            if (discriminant > 0) {
                root1 = (-b + Math.sqrt(discriminant)) / (2 * a);
                root2 = (-b - Math.sqrt(discriminant)) / (2 * a);
                roots = `Two distinct real roots: ${root1.toFixed(2)} and ${root2.toFixed(2)}`;
            } else if (discriminant === 0) {
                root1 = -b / (2 * a);
                roots = `One real repeated root: ${root1.toFixed(2)}`;
            } else {
                const realPart = (-b / (2 * a)).toFixed(2);
                const imaginaryPart = (Math.sqrt(-discriminant) / (2 * a)).toFixed(2);
                roots = `Two complex conjugate roots: ${realPart} + ${imaginaryPart}i and ${realPart} - ${imaginaryPart}i`;
            }

            document.getElementById('quadraticResult').innerHTML = `
                Discriminant: ${discriminant.toFixed(2)}<br>
                Nature of roots: ${roots}
            `;
        }

        function clearQuadratic() {
            document.getElementById('a').value = "";
            document.getElementById('b').value = "";
            document.getElementById('c').value = "";
            document.getElementById('quadraticResult').innerText = "";
            document.getElementById('aError').innerText = "";
            document.getElementById('bError').innerText = "";
            document.getElementById('cError').innerText = "";
        }

        function calculateGrade() {
            const score = parseInt(document.getElementById('score').value);
            document.getElementById('scoreError').innerText = "";

            if (isNaN(score)) {
                document.getElementById('scoreError').innerText = "Please enter a valid score.";
                return;
            }

            if (score < 0 || score > 100) {
                document.getElementById('scoreError').innerText = "Score must be between 0 and 100.";
                return;
            }

            let grade = "";
            if (score > 85) {
                grade = "A+";
            } else if (score >= 75) {
                grade = "A";
            } else if (score >= 65) {
                grade = "B+";
            } else if (score >= 60) {
                grade = "B";
            } else if (score >= 55) {
                grade = "C+";
            } else if (score >= 50) {
                grade = "C";
            } else if (score == 49) {
                grade = "D";
            }
             else if (score > 0) {
                grade = "D";
            }
             else {
                grade = "D";
            }

            document.getElementById('gradingResult').innerText = `Score ${score} → Grade ${grade}`;
        }

        function clearGrade() {
            document.getElementById('score').value = "";
            document.getElementById('gradingResult').innerText = "";
            document.getElementById('scoreError').innerText = "";
        }
    </script>
</body>
</html>
README.md

markdown
# ICS-Quadratic-Grader

## Project Title and Brief Description

This project consists of an HTML page with two main functionalities: a quadratic equation solver and a grading system. The quadratic solver takes coefficients a, b, and c as input and calculates the discriminant and roots of the equation. The grading system takes a score as input and outputs the corresponding letter grade.

## How to Run

1.  Save the `index.html` file to your local machine.
2.  Double-click the `index.html` file to open it in your web browser. The page should run offline.

## Test Cases

### Quadratic Solver

*   **Case 1:** a = 1, b = -3, c = 2 (Two distinct real roots: 2.00 and 1.00)
*   **Case 2:** a = 1, b = -2, c = 1 (One real repeated root: 1.00)
*   **Case 3:** a = 1, b = 0, c = 1 (Two complex conjugate roots: 0.00 + 1.00i and 0.00 - 1.00i)
*   **Case 4:** a = 0, b = 2, c = 3 (Error: a cannot be zero)
*   **Case 5:** a = abc, b = 2, c = 3 (Error: invalid input)

### Grading System

*   **Case 1:** Score = 82 (Grade A)
*   **Case 2:** Score = 85 (Grade A+)
*   **Case 3:** Score = 75 (Grade A)
*   **Case 4:** Score = 65 (Grade B+)
*   **Case 5:** Score = 60 (Grade B)
*   **Case 6:** Score = 55 (Grade C+)
*   **Case 7:** Score = 50 (Grade C)
*   **Case 8:** Score = 49 (Grade D)
*   **Case 9:** Score = 100 (Grade A+)
*   **Case 10:** Score = 0 (Grade D)
*   **Case 11:** Score = -1 (Error: out of range)
*   **Case 12:** Score = 101 (Error: out of range)
*   **Case 13:** Score = text (Error: invalid input)
