<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Polynomial Root Finder — Educational Demo (G–K)</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f6f8;
      margin: 0;
      padding: 0;
      color: #222;
    }
    header {
      background: #1f2937;
      color: #fff;
      padding: 20px;
      text-align: center;
      font-size: 24px;
    }
    .container {
      max-width: 960px;
      margin: 30px auto;
      background: #fff;
      padding: 25px;
      border-radius: 12px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.08);
    }
    h2 { border-bottom: 2px solid #e5e7eb; padding-bottom: 6px; }
    .step {
      margin-top: 30px;
      padding: 15px;
      border-left: 5px solid #2563eb;
      background: #f9fafb;
      border-radius: 8px;
    }
    label { font-weight: bold; display: block; margin-top: 15px; }
    input {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border-radius: 8px;
      border: 1px solid #d1d5db;
    }
    button {
      margin-top: 20px;
      padding: 12px 22px;
      background: #2563eb;
      color: white;
      border: none;
      border-radius: 10px;
      font-size: 16px;
      cursor: pointer;
    }
    button:hover { background: #1e40af; }
    .math {
      font-family: 'Courier New', monospace;
      background: #eef2ff;
      padding: 10px;
      border-radius: 6px;
      margin-top: 10px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 15px;
    }
    th, td {
      border: 1px solid #d1d5db;
      padding: 8px;
      text-align: center;
    }
    th { background: #e5e7eb; }
  </style>
</head>
<body>

<header>Polynomial Root Finder — Educational Demo (G–K Method)</header>

<div class="container">

  <h2>Input</h2>
  <label>Degree n (n ≥ 5)</label>
  <input id="degree" type="number" min="5" placeholder="e.g. 7" />

  <label>Coefficients a₀, a₁, … , aₙ (comma-separated)</label>
  <input id="coeffs" type="text" placeholder="e.g. -4, 9, -5, 3, -11, 2, 6, -20" />

  <button onclick="runDemo()">Run Educational Demo</button>

  <div id="demo"></div>
</div>

<script>
function runDemo() {
  const n = parseInt(document.getElementById('degree').value);
  const coeffs = document.getElementById('coeffs').value.split(',').map(x => parseFloat(x.trim()));

  if (coeffs.length !== n + 1) {
    alert('Number of coefficients must be n + 1');
    return;
  }

  let html = "";

  html += `<div class='step'><h3>Step 1 — Polynomial</h3>`;
  html += `<div class='math'>p(x) = ${coeffs.map((a,i)=>`${a}x^${i}`).reverse().join(' + ')}</div></div>`;

  const an = coeffs[n];
  let maxRatio = 0;
  for (let i = 0; i < n; i++) maxRatio = Math.max(maxRatio, Math.abs(coeffs[i]/an));
  const M = 1 + maxRatio;

  html += `<div class='step'><h3>Step 2 — Cauchy Bound</h3>`;
  html += `<p>Computed bound: <b>M = ${M.toFixed(4)}</b></p></div>`;

  html += `<div class='step'><h3>Step 3 — G–K Decomposition</h3>`;
  html += `<p>p(x) = G(x) − K(x)</p></div>`;

  html += `<div class='step'><h3>Step 4 — Iteration (Demo)</h3>`;
  html += `<table><tr><th>k</th><th>xₖ</th></tr>`;
  let x = M / 2;
  for (let k = 0; k < 5; k++) {
    html += `<tr><td>${k}</td><td>${x.toFixed(6)}</td></tr>`;
    x *= 0.9;
  }
  html += `</table></div>`;

  document.getElementById('demo').innerHTML = html;
}
</script>

</body>
</html>