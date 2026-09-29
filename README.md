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
    }

    .status {
      display: inline-block;
      padding: 7px 12px;
      border-radius: 20px;
      background: #132e22;
      color: #4ade80;
      font-size: 13px;
    }

    .cards {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
      gap: 18px;
    }

    .card {
      background: #111827;
      border: 1px solid #243044;
      border-radius: 18px;
      padding: 22px;
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
      margin-top: 20px;
      padding: 18px;
      border-radius: 14px;
      background: #0b1220;
      text-align: center;
    }

    .label {
      color: #94a3b8;
      font-size: 12px;
      text-transform: uppercase;
    }

    .signal {
      font-size: 28px;
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
      margin-top: 9px;
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
    }

    .section {
      margin-top: 35px;
    }

    .history-item {
      background: #111827;
      border: 1px solid #243044;
      border-radius: 12px;
      padding: 15px;
      margin-bottom: 10px;
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
  </style>
</head>

<body>

<div class="container">

  <header>
    <h1>📈 My Trading Signals</h1>
    <p>Multi-Market Demo Dashboard</p>
    <div class="status">● System Online</div>
  </header>

  <div class="cards" id="marketCards"></div>

  <button onclick="loadMarkets()">
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
    Reference rates and demo signals are provided for software
    testing and educational purposes only. They are not financial
    advice, guarantees, or recommendations to buy or sell.
  </div>

</div>

<script>

const markets = [
  ["EUR/USD", "EUR", "USD"],
  ["GBP/USD", "GBP", "USD"],
  ["USD/JPY", "USD", "JPY"],
  ["AUD/USD", "AUD", "USD"],
  ["USD/CAD", "USD", "CAD"],
  ["USD/CHF", "USD", "CHF"],
  ["EUR/GBP", "EUR", "GBP"]
];


function createDemoSignal(rate) {

  /*
    Simple demonstration rule.
    This is NOT a validated trading strategy.
  */

  if (rate > 1.5) {
    return "BUY";
  }

  if (rate < 0.5) {
    return "SELL";
  }

  return "WAIT";
}


function signalClass(signal) {

  if (signal === "BUY") {
    return "buy";
  }

  if (signal === "SELL") {
    return "sell";
  }

  return "wait";
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

  history = history.slice(0, 30);

  localStorage.setItem(
    "demoSignalHistory",
    JSON.stringify(history)
  );
}


function displayHistory() {

  const list =
    document.getElementById("historyList");

  const history = JSON.parse(
    localStorage.getItem("demoSignalHistory") || "[]"
  );

  if (history.length === 0) {
    list.innerHTML =
      "No demo signals recorded yet.";
    return;
  }

  list.innerHTML = "";

  history.forEach(item => {

    const div =
      document.createElement("div");

    div.className = "history-item";

    div.innerHTML = `
      <strong>${item.pair}</strong>
      —
      <span class="${signalClass(item.signal)}">
        ${item.signal}
      </span>
      — ${item.price}
      <div class="history-time">
        ${item.time}
      </div>
    `;

    list.appendChild(div);
  });
}


function createCard(pair, id) {

  return `
    <div class="card">

      <div class="pair">
        ${pair}
      </div>

      <div class="market">
        Forex Reference Rate
      </div>

      <div class="signal-box">

        <div class="label">
          Demo Signal
        </div>

        <div
          id="${id}-signal"
          class="signal wait">
          Loading...
        </div>

      </div>

      <div
        id="${id}-price"
        class="price">
        Reference Price: Loading...
      </div>

      <div
        id="${id}-strategy"
        class="strategy">
        Checking demo strategy...
      </div>

    </div>
  `;
}


async function loadMarkets() {

  const cards =
    document.getElementById("marketCards");

  cards.innerHTML = "";

  markets.forEach((market, index) => {

    cards.innerHTML +=
      createCard(
        market[0],
        "market" + index
      );

  });


  for (let i = 0; i < markets.length; i++) {

    const pair = markets[i][0];
    const base = markets[i][1];
    const quote = markets[i][2];

    const id = "market" + i;

    try {

      const response =
        await fetch(
          `https://api.frankfurter.dev/v2/rate/${base}/${quote}`
        );

      if (!response.ok) {
        throw new Error("Rate unavailable");
      }

      const data =
        await response.json();

      const rate =
        data.rate;

      const signal =
        createDemoSignal(rate);

      document.getElementById(
        id + "-price"
      ).textContent =
        "Reference Price: " +
        rate.toFixed(5);

      const signalElement =
        document.getElementById(
          id + "-signal"
        );

      signalElement.textContent =
        signal;

      signalElement.className =
        "signal " +
        signalClass(signal);

      document.getElementById(
        id + "-strategy"
      ).textContent =
        "Demo rule • Reference date: " +
        data.date;

      saveHistory(
        pair,
        rate.toFixed(5),
        signal
      );

    }

    catch (error) {

      document.getElementById(
        id + "-price"
      ).textContent =
        "Reference rate unavailable.";

      document.getElementById(
        id + "-strategy"
      ).textContent =
        "Try refreshing later.";

    }

  }

  displayHistory();
}


displayHistory();

loadMarkets();

</script>

</body>
</html>