<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gamblaizer</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    font-family:Arial, sans-serif;
    background:#111;
    color:white;
}

header{
    background:#000;
    padding:20px;
    text-align:center;
    box-shadow:0 2px 10px rgba(0,0,0,0.5);
}

header h1{
    color:#00ff88;
    font-size:2.5rem;
}

.container{
    max-width:1000px;
    margin:auto;
    padding:30px;
}

.card{
    background:#1b1b1b;
    padding:25px;
    border-radius:15px;
    margin-bottom:20px;
}

input, button{
    width:100%;
    padding:12px;
    margin-top:10px;
    border:none;
    border-radius:8px;
}

input{
    background:#2b2b2b;
    color:white;
}

button{
    background:#00ff88;
    color:black;
    font-weight:bold;
    cursor:pointer;
}

button:hover{
    opacity:0.9;
}

.result{
    margin-top:20px;
    font-size:18px;
}

footer{
    text-align:center;
    padding:20px;
    background:#000;
    margin-top:30px;
}
</style>
</head>

<body>

<header>
    <h1>Gamblaizer</h1>
    <p>Bet Calculator & Odds Analyzer</p>
</header>

<div class="container">

    <div class="card">
        <h2>Bet Calculator</h2>

        <label>Stake Amount</label>
        <input type="number" id="stake" placeholder="Enter stake">

        <label>Decimal Odds</label>
        <input type="number" id="odds" step="0.01" placeholder="Enter odds">

        <button onclick="calculateBet()">Calculate</button>

        <div class="result" id="betResult"></div>
    </div>

    <div class="card">
        <h2>Bet Analyzer</h2>

        <label>Probability (%)</label>
        <input type="number" id="probability" placeholder="Estimated probability">

        <button onclick="analyzeBet()">Analyze Bet</button>

        <div class="result" id="analysisResult"></div>
    </div>

</div>

<footer>
    © 2026 Gamblaizer
</footer>

<script>

function calculateBet(){

    let stake = parseFloat(document.getElementById("stake").value);
    let odds = parseFloat(document.getElementById("odds").value);

    if(isNaN(stake) || isNaN(odds)){
        document.getElementById("betResult").innerHTML =
        "Please enter valid values.";
        return;
    }

    let payout = stake * odds;
    let profit = payout - stake;

    document.getElementById("betResult").innerHTML =
    `
    Potential Payout: <b>R${payout.toFixed(2)}</b><br>
    Potential Profit: <b>R${profit.toFixed(2)}</b>
    `;
}

function analyzeBet(){

    let odds = parseFloat(document.getElementById("odds").value);
    let probability = parseFloat(document.getElementById("probability").value);

    if(isNaN(odds) || isNaN(probability)){
        document.getElementById("analysisResult").innerHTML =
        "Please enter valid values.";
        return;
    }

    let impliedProbability = (1 / odds) * 100;
    let edge = probability - impliedProbability;

    let risk = "High Risk";

    if(edge > 10){
        risk = "Lower Risk";
    }
    else if(edge > 0){
        risk = "Medium Risk";
    }

    document.getElementById("analysisResult").innerHTML =
    `
    Implied Probability: <b>${impliedProbability.toFixed(2)}%</b><br>
    Estimated Edge: <b>${edge.toFixed(2)}%</b><br>
    Risk Rating: <b>${risk}</b>
    `;
}

</script>

</body>
</html>
