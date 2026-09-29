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

    .status {
      text-align: center;
      margin-bottom: 20px;
      color: #22c55e;
    }

    .card {
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
      color: #60a5fa;
      margin: 12px 0;
    }

    .signal {
      font-size: 22px;
      font-weight: bold;
      margin: 15px 0;
    }

    .buy {
      color: #22c55e;
    }

    .sell {
      color: #ef4444;
    }

    .wait {
      color: #f59e0b;
    }

    .details {
      background: #111827;
      padding: 14px;
      border-radius: 10px;
      line-height: 1.8;
      color: #d1d5db;
    }

    .updated {
      color: #9ca3af;
      font-size: 13px;
      margin-top: 12px;
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
      margin: 22px 5px;
    }
  </style>
</head>

<body>

<header>
  <h1>📈 My Trading Signals</h1>
  <p>Automated Demo Dashboard</p>
</header>

<div class="container">

  <div id="status" class="status">
    Loading market data...
  </div>

  <div class="card">
    <div class="pair">EUR/USD</div>

    <div id="eurPrice" class="price">
      Loading...
    </div>

    <div id="eurSignal" class="signal wait">
      WAIT
    </div>

    <div class="details">
      Strategy: Demo trend rule<br>
      Status: Educational demo
    </div>

    <div id="eurUpdated" class="updated"></div>
  </div>

  <div class="card">
    <div class="pair">GBP/USD</div>

    <div id="gbpPrice" class="price">
      Loading...
    </div>

    <div id="gbpSignal" class="signal wait">
      WAIT
    </div>

    <div class="details">
      Strategy: Demo trend rule<br>
      Status: Educational demo
    </div>

    <div id="gbpUpdated" class="updated"></div>
  </div>

  <button onclick="loadRates()">
    🔄 Refresh Market Data
  </button>

  <div class="notice">
    Demo signals are generated for educational/testing purposes only.
    They are not financial advice, guarantees, or recommendations to buy or sell.
  </div>

</div>

<script>

async function getRate(base, quote) {

  const response = await fetch(
    `https://api.frankfurter.dev/v2/rate/${base}/${quote}`
  );

  if (!response.ok) {
    throw new Error("Market data unavailable");
  }

  return await response.json();
}


function createDemoSignal(rate) {

  /*
    Simple demonstration rule.

    This is NOT a prediction system.
    It only demonstrates how software can
    turn incoming data into a signal label.
  */

  if (rate > 1.5) {
    return "BUY";
  }

  if (rate < 0.5) {
    return "SELL";
  }

  return "WAIT";
}


function showSignal(elementId, signal) {

  const element = document.getElementById(elementId);

  element.textContent = signal;

  element.className = "signal";

  if (signal === "BUY") {
    element.classList.add("buy");
  }

  else if (signal === "SELL") {
    element.classList.add("sell");
  }

  else {
    element.classList.add("wait");
  }
}


async function loadRates() {

  const status = document.getElementById("status");

  status.textContent = "Loading market data...";

  try {

    const eur = await getRate("EUR", "USD");
    const gbp = await getRate("GBP", "USD");

    document.getElementById("eurPrice").textContent =
      eur.rate.toFixed(5);

    document.getElementById("gbpPrice").textContent =
      gbp.rate.toFixed(5);

    showSignal(
      "eurSignal",
      createDemoSignal(eur.rate)
    );

    showSignal(
      "gbpSignal",
      createDemoSignal(gbp.rate)
    );

    document.getElementById("eurUpdated").textContent =
      "Reference date: " + eur.date;

    document.getElementById("gbpUpdated").textContent =
      "Reference date: " + gbp.date;

    status.textContent = "🟢 Market data loaded";

  }

  catch (error) {

    status.textContent =
      "⚠️ Could not load market data.";

  }
}


loadRates();

</script>

</body>
</html>