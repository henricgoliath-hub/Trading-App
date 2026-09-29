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
      color: #f8fafc;
    }

    .container {
      max-width: 1000px;
      margin: auto;
      padding: 25px 18px 40px;
    }

    header {
      text-align: center;
      padding: 20px 0 30px;
    }

    header h1 {
      margin: 0;
      font-size: 32px;
    }

    header p {
      color: #94a3b8;
      margin-top: 8px;
    }

    .status {
      display: inline-block;
      margin-top: 12px;
      padding: 7px 12px;
      border-radius: 20px;
      background: #132e22;
      color: #4ade80;
      font-size: 13px;
    }

    .cards {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 18px;
    }

    .card {
      background: #111827;
      border: 1px solid #243044;
      border-radius: 18px;
      padding: 22px;
      box-shadow: 0 8px 25px rgba(0,0,0,0.2);
    }

    .top {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .pair {
      font-size: 22px;
      font-weight: bold;
    }

    .market {
      color: #64748b;
      font-size: 12px;
      margin-top: 5px;
    }

    .signal-box {
      margin-top: 22px;
      padding: 18px;
      border-radius: 14px;
      background: #0b1220;
      text-align: center;
    }

    .signal-label {
      color: #94a3b8;
      font-size: 12px;
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    .signal {
      font-size: 30px;
      font-weight: bold;
      margin-top: 7px;
    }

    .buy {
      color: #22c55e;
    }

    .sell {
      color: #ef4444;
    }

    .wait {
      color: #facc15;
    }

    .price {
      margin-top: 18px;
      color: #cbd5e1;
    }

    .strategy {
      margin-top: 10px;
      color: #94a3b8;
      font-size: 13px;
    }

    button {
      display: block;
      margin: 25px auto;
      padding: 14px 25px;
      border: 0;
      border-radius: 12px;
      background: #2563eb;
      color: white;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
    }

    button:hover {
      background: #1d4ed8;
    }

    .section {
      margin-top: 35px;
    }

    .section h2 {
      font-size: 22px;
    }

    .history-item {
      background: #111827;
      border: 1px solid #243044;
      border-radius: 12px;
      padding: 15px;
      margin-bottom: 10px;
    }

    .history-top {
      display: flex;
      justify-content: space-between;
      gap: 10px;
      flex-wrap: wrap;
    }

    .history-time {
      color: #64748b;
      font-size: 12px;
      margin-top: 8px;
    }

    .disclaimer {
      margin-top: 35px;
      padding: 18px;
      border-radius: 14px;
      background: #111827;
      border: 1px solid #243044;
      color: #94a3b8;
      font-size: 13px;
      line-height: 1.5;
      text-align: center;
    }

    footer {
      text-align: center;
      margin-top: 25px;
      color: #475569;
      font-size: 12px;
    }
  </style>
</head>

<body>

<div class="container">

  <header>
    <h1>📈 My Trading Signals</h1>
    <p>Automated Demo Trading Dashboard</p>
    <div class="status">● System Online</div>
  </header>

  <div class="cards">

    <div class="card">

      <div class="top">
        <div>
          <div class="pair">EUR/USD</div>
          <div class="market">Forex Reference Rate</div>
        </div>
      </div>

      <div class="signal-box">
        <div class="signal-label">Demo Signal</div>
        <div id="eurSignal" class="signal wait">Loading...</div>
      </div>

      <div id="eurPrice" class="price">
        Reference Price: Loading...
      </div>

      <div id="eurStrategy" class="strategy">
        Checking demo strategy...
      </div>

    </div>


    <div class="card">

      <div class="top">
        <div>
          <div class="pair">GBP/USD</div>
          <div class="market">Forex Reference Rate</div>
        </div>
      </div>

      <div class="signal-box">
        <div class="signal-label">Demo Signal</div>
        <div id="gbpSignal" class="signal wait">Loading...</div>
      </div>

      <div id="gbpPrice" class="price">
        Reference Price: Loading...
      </div>

      <div id="gbpStrategy" class="strategy">
        Checking demo strategy...
      </div>

    </div>

  </div>


  <button onclick="loadMarketData()">
    🔄 Refresh Market Data
  </button>


  <div class="section">

    <h2>📋 Signal History</h2>

    <div id="historyList">
      No demo signals recorded yet.
    </div>

  </div>


  <div class="disclaimer">

    ⚠️ <strong>Educational Demo</strong><br>

    These signals are generated using a simple demonstration rule
    and reference exchange-rate data. They are for educational and
    software-testing purposes only and are not financial advice,
    guarantees, or recommendations to buy or sell.

  </div>


  <footer>
    My Trading Signals • Demo Dashboard
  </footer>

</div>


<script>

function createDemoSignal(rate) {

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


function saveHistory(pair, price, signal) {

  let history = JSON.parse(
    localStorage.getItem("demoSignalHistory") || "[]"
  );

  history.unshift({

    pair: pair,

    price: price,

    signal: signal,

    time: new Date().toLocaleString()

  });

  history = history.slice(0, 20);

  localStorage.setItem(
    "demoSignalHistory",
    JSON.stringify(history)
  );

  displayHistory();
}


function displayHistory() {

  const historyList =
    document.getElementById("historyList");

  const history = JSON.parse(
    localStorage.getItem("demoSignalHistory") || "[]"
  );

  if (history.length === 0) {

    historyList.innerHTML =
      "No demo signals recorded yet.";

    return;
  }

  historyList.innerHTML = "";

  history.forEach(item => {

    let signalClass = "wait";

    if (item.signal === "BUY") {
      signalClass = "buy";
    }

    if (item.signal === "SELL") {
      signalClass = "sell";
    }

    const div =
      document.createElement("div");

    div.className = "history-item";

    div.innerHTML = `

      <div class="history-top">

        <strong>${item.pair}</strong>

        <span class="${signalClass}">
          ${item.signal}
        </span>

        <span>
          ${item.price}
        </span>

      </div>

      <div class="history-time">
        ${item.time}
      </div>

    `;

    historyList.appendChild(div);

  });
}


async function loadMarketData() {

  try {

    const eurResponse =
      await fetch(
        "https://api.frankfurter.dev/v2/rate/EUR/USD"
      );

    const eurData =
      await eurResponse.json();

    const eurRate =
      eurData.rate;

    const eurSignal =
      createDemoSignal(eurRate);

    document.getElementById("eurPrice")
      .textContent =
      "Reference Price: " +
      eurRate.toFixed(5);

    showSignal(
      "eurSignal",
      eurSignal
    );

    document.getElementById("eurStrategy")
      .textContent =
      "Demo rule based on the reference rate.";

    saveHistory(
      "EUR/USD",
      eurRate.toFixed(5),
      eurSignal
    );


    const gbpResponse =
      await fetch(
        "https://api.frankfurter.dev/v2/rate/GBP/USD"
      );

    const gbpData =
      await gbpResponse.json();

    const gbpRate =
      gbpData.rate;

    const gbpSignal =
      createDemoSignal(gbpRate);

    document.getElementById("gbpPrice")
      .textContent =
      "Reference Price: " +
      gbpRate.toFixed(5);

    showSignal(
      "gbpSignal",
      gbpSignal
    );

    document.getElementById("gbpStrategy")
      .textContent =
      "Demo rule based on the reference rate.";

    saveHistory(
      "GBP/USD",
      gbpRate.toFixed(5),
      gbpSignal
    );

  }

  catch (error) {

    document.getElementById("eurPrice")
      .textContent =
      "Unable to load reference rate.";

    document.getElementById("gbpPrice")
      .textContent =
      "Unable to load reference rate.";

    console.log(error);

  }

}


displayHistory();

loadMarketData();

</script>

</body>
</html>