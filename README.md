<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Trading Signals</title>

  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #0f172a;
      color: white;
    }

    .container {
      max-width: 900px;
      margin: auto;
      padding: 25px;
    }

    h1 {
      text-align: center;
      margin-bottom: 5px;
    }

    .subtitle {
      text-align: center;
      color: #94a3b8;
      margin-bottom: 25px;
    }

    .cards {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 15px;
    }

    .card {
      background: #1e293b;
      padding: 20px;
      border-radius: 15px;
      border: 1px solid #334155;
    }

    .pair {
      font-size: 22px;
      font-weight: bold;
    }

    .price {
      color: #cbd5e1;
      margin: 12px 0;
    }

    .signal {
      font-size: 24px;
      font-weight: bold;
      margin: 10px 0;
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

    button {
      display: block;
      margin: 25px auto;
      padding: 13px 22px;
      border: none;
      border-radius: 10px;
      background: #2563eb;
      color: white;
      font-size: 16px;
      cursor: pointer;
    }

    button:hover {
      background: #1d4ed8;
    }

    .history {
      margin-top: 35px;
    }

    .history h2 {
      margin-bottom: 15px;
    }

    .history-item {
      background: #1e293b;
      border: 1px solid #334155;
      border-radius: 10px;
      padding: 15px;
      margin-bottom: 10px;
    }

    .history-item span {
      margin-right: 12px;
    }

    .disclaimer {
      margin-top: 30px;
      padding: 15px;
      background: #172033;
      border-radius: 10px;
      color: #94a3b8;
      font-size: 13px;
      text-align: center;
    }
  </style>
</head>

<body>

  <div class="container">

    <h1>📈 My Trading Signals</h1>
    <div class="subtitle">Automated Demo Dashboard</div>

    <div class="cards">

      <div class="card">
        <div class="pair">EUR/USD</div>
        <div class="price" id="eurPrice">Loading...</div>
        <div class="signal" id="eurSignal">...</div>
        <div id="eurStrategy">Checking demo signal...</div>
      </div>

      <div class="card">
        <div class="pair">GBP/USD</div>
        <div class="price" id="gbpPrice">Loading...</div>
        <div class="signal" id="gbpSignal">...</div>
        <div id="gbpStrategy">Checking demo signal...</div>
      </div>

    </div>

    <button onclick="loadMarketData()">🔄 Refresh Market Data</button>

    <div class="history">
      <h2>📋 Signal History</h2>
      <div id="historyList">
        No demo signals recorded yet.
      </div>
    </div>

    <div class="disclaimer">
      Demo signals are generated for educational and testing purposes only.
      They are not financial advice, guarantees, or recommendations to buy or sell.
    </div>

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
      } else if (signal === "SELL") {
        element.classList.add("sell");
      } else {
        element.classList.add("wait");
      }
    }

    function saveHistory(pair, price, signal) {

      let history = JSON.parse(
        localStorage.getItem("demoSignalHistory") || "[]"
      );

      const now = new Date();

      history.unshift({
        pair: pair,
        price: price,
        signal: signal,
        time: now.toLocaleString()
      });

      history = history.slice(0, 20);

      localStorage.setItem(
        "demoSignalHistory",
        JSON.stringify(history)
      );

      displayHistory();
    }

    function displayHistory() {

      const historyList = document.getElementById("historyList");

      let history = JSON.parse(
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

        const div = document.createElement("div");

        div.className = "history-item";

        div.innerHTML = `
          <strong>${item.pair}</strong>
          <span>Price: ${item.price}</span>
          <span class="${signalClass}">
            ${item.signal}
          </span>
          <br>
          <small>${item.time}</small>
        `;

        historyList.appendChild(div);
      });
    }

    async function loadMarketData() {

      try {

        const eurResponse =
          await fetch("https://api.frankfurter.dev/v2/rate/EUR/USD");

        const eurData = await eurResponse.json();

        const eurRate = eurData.rate;

        const eurSignal = createDemoSignal(eurRate);

        document.getElementById("eurPrice").textContent =
          "Reference Price: " + eurRate.toFixed(5);

        showSignal("eurSignal", eurSignal);

        document.getElementById("eurStrategy").textContent =
          "Demo rule based on the reference rate.";

        saveHistory(
          "EUR/USD",
          eurRate.toFixed(5),
          eurSignal
        );


        const gbpResponse =
          await fetch("https://api.frankfurter.dev/v2/rate/GBP/USD");

        const gbpData = await gbpResponse.json();

        const gbpRate = gbpData.rate;

        const gbpSignal = createDemoSignal(gbpRate);

        document.getElementById("gbpPrice").textContent =
          "Reference Price: " + gbpRate.toFixed(5);

        showSignal("gbpSignal", gbpSignal);

        document.getElementById("gbpStrategy").textContent =
          "Demo rule based on the reference rate.";

        saveHistory(
          "GBP/USD",
          gbpRate.toFixed(5),
          gbpSignal
        );

      } catch (error) {

        document.getElementById("eurPrice").textContent =
          "Unable to load rate";

        document.getElementById("gbpPrice").textContent =
          "Unable to load rate";

        console.log(error);
      }
    }

    displayHistory();
    loadMarketData();

  </script>

</body>
</html>