<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        .container { max-width: 600px; margin: auto; }
        .question { margin-bottom: 10px; display: flex; flex-direction: column; }
        .score { font-weight: bold; }
        .result { display: none; margin-top: 20px; padding: 10px; border: 1px solid #ccc; }
    </style>
</head>
<body>
    <div class="container">
        <h2>Learning Culture Scorecard</h2>
        <p>Rate each statement from 1 (Very Poor) to 5 (Excellent).</p>
        <form id="scorecard">
            <label>Email: </label>
            <input type="email" id="email" name="email" required>
            <br><br>
            <div class="question">
                <label>1. Employees actively seek out learning opportunities.</label>
                <input type="number" min="1" max="5" name="q1" required>
            </div>
            <div class="question">
                <label>2. Learning is seen as a growth opportunity.</label>
                <input type="number" min="1" max="5" name="q2" required>
            </div>
            <div class="question">
                <label>3. Employees feel motivated to apply new skills.</label>
                <input type="number" min="1" max="5" name="q3" required>
            </div>
            <div class="question">
                <label>4. Managers encourage employees to take time for learning.</label>
                <input type="number" min="1" max="5" name="q4" required>
            </div>
            <div class="question">
                <label>5. Learning resources are easily accessible and frequently updated.</label>
                <input type="number" min="1" max="5" name="q5" required>
            </div>
            <button type="submit">Calculate Score</button>
        </form>
        <div class="result" id="result">
            <h3>Your Learning Culture Score:</h3>
            <p class="score" id="score"></p>
            <p id="interpretation"></p>
        </div>
    </div>
    <script>
        document.getElementById('scorecard').addEventListener('submit', function(event) {
            event.preventDefault();
            let total = 0;
            let inputs = document.querySelectorAll('input[type="number"]');
            inputs.forEach(input => total += parseInt(input.value));
            let score = (total / (inputs.length * 5)) * 100;
            document.getElementById('score').innerText = score.toFixed(1) + "%";
            
            let interpretation = "";
            if (score < 30) interpretation = "At Risk: Learning is ignored, employees resist change.";
            else if (score < 50) interpretation = "Weak: Learning exists but lacks impact.";
            else if (score < 70) interpretation = "Developing: Improving but needs stronger leadership support.";
            else if (score < 85) interpretation = "Strong: Learning is valued and aligned with business goals.";
            else interpretation = "High-Performance: Learning drives innovation and competitive advantage.";
            
            document.getElementById('interpretation').innerText = interpretation;
            document.getElementById('result').style.display = 'block';
            
            // Capture Email and Score
            let email = document.getElementById('email').value;
            fetch('https://your-server-endpoint.com/capture-email', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ email: email, score: score.toFixed(1) })
            });
        });
    </script>
</body>
</html>
