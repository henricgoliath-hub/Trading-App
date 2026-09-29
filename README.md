<!DOCTYPE html>
<html>
<head>
  <title>My Trading Signals</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #0b1120;
      color: white;
    }

    .header {
      padding: 25px 20px;
      text-align: center;
      background: #111827;
    }

    .header h1 {
      margin: 0;
      font-size: 30px;
    }

    .header p {
      color: #9ca3af;
    }

    .container {
      max-width: 600px;
      margin: auto;
      padding: 20px;
    }

    .dashboard {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
    }

    .stat {
      flex: 1;
      background: #1f2937;
      padding: 15px;
      border-radius: 12px;
      text-align: center;
    }

    .stat strong {
      display: block;
      font-size: 22px;
    }

    .signal {
      background: #1f2937;
      padding: 20px;
      border-radius: 15px;
      margin-bottom: 15px;
    }

    .pair {
      font-size: 21px;
      font-weight: bold;
    }

    .buy {
      color: #22c55e;
      font-weight: bold;
      font-size: 20px;
    }

    .sell {
      color: #ef4444;
      font-weight: bold;
      font-size: 20px;
    }

    .details {
      line-height: 1.8;
      color: #d1d5db;
    }

    .active {
      color: #22c55e;
      font-size: 14px;
    }

    .refresh {
      width: 100%;
      padding: 14px;
      border: none;
      border-radius: 10px;
      background: #2563eb;
      color: white;
      font-size: 16px;
      margin-top: 5px;
    }

    .notice {
      text-align: center;
      color: #9ca3af;
      font-size: 12px;
      margin-top: 25px;
    }
  </style>
</head>

<body>

  <div class="header">
    <h1>📈 My Trading Signals</h1>
    <p>Trading dashboard</p>
  </div>

  <div class="container">

    <div class="dashboard">
      <div class="stat">
        <strong>3</strong>
        Active
      </div>

      <div class="stat">
        <strong>Demo</strong>
        Mode
      </div>
    </div>

    <div class="signal">
      <div class="pair">EUR/USD</div>
      <div class="buy">BUY</div>

      <div class="details">
        Entry: Example price<br>
        Stop Loss: Example price<br>
        Take Profit: Example price
      </div>

      <div class="active">● Active signal</div>
    </div>

    <div class="signal">
      <div class="pair">GBP/USD</div>
      <div class="sell">SELL</div>

      <div class="details">
        Entry: Example price<br>
        Stop Loss: Example price<br>
        Take Profit: Example price
      </div>

      <div class="active">● Active signal</div>
    </div>

    <div class="signal">
      <div class="pair">XAU/USD — GOLD</div>
      <div class="buy">BUY</div>

      <div class="details">
        Entry: Example price<br>
        Stop Loss: Example price<br>
        Take Profit: Example price
      </div>

      <div class="active">● Active signal</div>
    </div>

    <button class="refresh" onclick="location.reload()">
      🔄 Refresh Signals
    </button>

    <div class="notice">
      Demo interface for educational purposes. Example prices are not live market data.
    </div>

  </div>

</body>
</html>
