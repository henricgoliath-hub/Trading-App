
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Trading Signals</title>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #0b1120;
      color: white;
    }

    header {
      background: #111827;
      padding: 28px 20px;
      text-align: center;
      border-bottom: 1px solid #374151;
    }

    header h1 {
      margin: 0;
      font-size: 30px;
    }

    header p {
      color: #9ca3af;
    }

    .container {
      width: 92%;
      max-width: 650px;
      margin: 25px auto;
    }

    .rate {
      background: #1f2937;
      border: 1px solid #374151;
      border-radius: 16px;
      padding: 20px;
      margin-bottom: 18px;
    }

    .pair {
      font-size: 22px;
      font-weight: bold;
    }

    .price {
      font-size: 28px;
      margin: 15px 0;
      color: #60a5fa;
    }

    .updated {
      color: #9ca3af;
      font-size: 13px;
    }

    button {
      width: 100%;
      padding: 15px;
      border: none;
      border-radius: 10px;
      background: #2563eb;
      color: white;
      font-size: 16px;
      font-weight: bold;
    }

    .notice {
      text-align: center;
      color: #9ca3af;
      font-size: 12px;
      line-height: 1.5;
      margin-top: 22px;
    }

    #status {
      text-align: center;
      margin-bottom: 20px;
      color: #22c55e;
    }
  </style>
</head>

<body>

<header>
  <h1>📈 My Trading Signals</h1>
  <p>Market Reference Dashboard</p>
</header>

<div class="container">

  <div id="status">Loading reference rates...</div>

  <div class="rate">
    <div class="pair">EUR/USD</div>
    <div class="price" id="eurusd">Loading...</div>
    <div class="updated" id="eurDate"></div>
  </div>

  <div class="rate">
    <div class="pair">GBP/USD</div>
    <div class="price" id="gbpusd">Loading...</div>
    <div class="updated" id="gbpDate"></div>
  </div>

  <button onclick="loadRates()">🔄 Refresh Rates</button>

  <div class="notice">
    These are reference exchange rates, not live trading prices or trading advice.
  </div>

</div>

<script>

async function getRate(base, quote) {

  const response = await fetch(
    `https://api.frankfurter.dev/v2/rate/${base}/${quote}`
  );

  if (!response.ok) {
    throw new Error("Could not load rate");
  }

  return await response.json();
}

async function loadRates() {

  const status = document.getElementById("status");

  status.textContent = "Loading reference rates...";

  try {

    const eur = await getRate("EUR", "USD");
    const gbp = await getRate("GBP", "USD");

    document.getElementById("eurusd").textContent =
      eur.rate.toFixed(5);

    document.getElementById("gbpusd").textContent =
      gbp.rate.toFixed(5);

    document.getElementById("eurDate").textContent =
      "Reference date: " + eur.date;

    document.getElementById("gbpDate").textContent =
      "Reference date: " + gbp.date;

    status.textContent = "🟢 Rates loaded";

  } catch (error) {

    status.textContent =
      "⚠️ Could not load rates. Try again.";

    console.error(error);

  }
}

loadRates();

</script>

</body>
</html>