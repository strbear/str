<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>STR Bear Ratio Calculator - Whiteout Survival</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #1c1c1c;
      padding: 20px;
      color: #fff;
    }
    h1 {
      color: #ffffff;
      background-color: #333;
      padding: 10px;
      border-radius: 10px;
    }
    p.description {
      margin-top: 10px;
      background-color: #2e2e2e;
      padding: 10px;
      border-radius: 5px;
      color: #ccc;
    }
    label, input, textarea {
      display: block;
      margin: 10px 0;
    }
    input[type="number"], textarea {
      width: 100%;
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    button {
      margin-top: 20px;
      padding: 10px 20px;
      background-color: #3498db;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #2980b9;
    }
    .output {
      margin-top: 20px;
      padding: 15px;
      background-color: #2e2e2e;
      border-radius: 5px;
      color: #fff;
    }
    label {
      background-color: #2e2e2e;
      padding: 5px;
      border-radius: 5px;
    }
  </style>
</head>
<body>
  <h1>STR Bear Ratio Calculator</h1>
  <p class="description">Welcome STR warriors! You’ve fought bears, survived blizzards, and probably sent the wrong troops at least once. This tool is here to help you look smart, stay deadly, and make your squad leaders proud. Now enter your numbers like the tactical genius you are!</p>

  <label for="infantry">Total Infantry:</label>
  <input type="number" id="infantry" placeholder="Enter total Infantry count">

  <label for="lancer">Total Lancer:</label>
  <input type="number" id="lancer" placeholder="Enter total Lancer count">

  <label for="marksman">Total Marksman:</label>
  <input type="number" id="marksman" placeholder="Enter total Marksman count">

  <label for="squadCapacities">Enter squad capacities (comma-separated, e.g. 138710,138710,98300):</label>
  <textarea id="squadCapacities" placeholder="Example: 138710,138710,98300,98300,138710,98300,138710"></textarea>

  <button onclick="calculateDistribution()">Calculate Distribution</button>

  <div class="output" id="output"></div>

  <script>
    function calculateDistribution() {
      const infantry = parseInt(document.getElementById('infantry').value) || 0;
      const lancer = parseInt(document.getElementById('lancer').value) || 0;
      const marksman = parseInt(document.getElementById('marksman').value) || 0;
      const squadInput = document.getElementById('squadCapacities').value.trim();

      const squads = squadInput.split(',').map(val => parseInt(val.trim())).filter(val => !isNaN(val));
      const totalCapacity = squads.reduce((sum, cap) => sum + cap, 0);

      if (totalCapacity === 0 || marksman === 0) {
        document.getElementById('output').innerHTML = "Please enter valid troop counts and squad capacities.";
        return;
      }

      const marksmanPercent = marksman / totalCapacity;
      const remainingPercent = 1 - marksmanPercent;
      const infantryPercent = remainingPercent / 2;
      const lancerPercent = remainingPercent / 2;

      let outputHTML = `<strong>Total Capacity:</strong> ${totalCapacity}<br>`;
      outputHTML += `<strong>Marksman %:</strong> ${Math.round(marksmanPercent * 100)}%<br>`;
      outputHTML += `<strong>Infantry %:</strong> ${Math.round(infantryPercent * 100)}%<br>`;
      outputHTML += `<strong>Lancer %:</strong> ${Math.round(lancerPercent * 100)}%<br><br>`;

      outputHTML += `<strong>Squad Breakdown:</strong><br>`;

      squads.forEach((cap, index) => {
        const m = Math.floor(cap * marksmanPercent);
        const i = Math.floor(cap * infantryPercent);
        const l = cap - m - i;
        outputHTML += `Squad ${index + 1}: Marksman: ${m}, Infantry: ${i}, Lancer: ${l} (Total: ${cap})<br>`;
      });

      document.getElementById('output').innerHTML = outputHTML;
    }
  </script>
</body>
</html>
