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
      margin-bottom: 0;
    }

    .container {
      width: 92%;
      max-width: 650px;
      margin: 25px auto;
    }

    .stats {
      display: flex;
      gap: 12px;
      margin-bottom: 25px;
    }

    .stat {
      flex: 1;
      background: #1f2937;
      padding: 18px;
      border-radius: 14px;
      text-align: center;
    }

    .stat-number {
      display: block;
      font-size: 24px;
      font-weight: bold;
      margin-bottom: 5px;
    }

    .stat-label {
      color: #9ca3af;
      font-size: 13px;
    }

    .signal {
      background: #1f2937;
      border: 1px solid #374151;
      border-radius: 16px;
      padding: 20px;
      margin-bottom: 18px;
    }

    .signal-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .pair {
      font-size: 21px;
      font-weight: bold;
    }

    .buy {
      color: #22c55e;
      font-size: 18px;
      font-weight: bold;
    }

    .sell {
      color: #ef4444;
      font-size: 18px;
      font-weight: bold;
    }

    .details {
      margin-top: 18px;
      display: grid;
      gap: 10px;
    }

    .detail {
      background: #111827;
      padding: 12px;
      border-radius: 9px;
      color: #d1d5db;
    }

    .status {
      margin-top: 15px;
      color: #22c55e;
      font-size: 14px;
    }

    .refresh {
      width: 100%;
      padding: 15px;
      border: none;
      border-radius: 10px;
      background: #2563eb;
      color: white;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
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
  <p>Trading Signals Dashboard</p>
</header>

<div class="container">

  <div class="stats">

    <div class="stat">
      <span class="stat-number">3</span>
      <span class="stat-label">Signals</span>
    </div>

    <div class="stat">
      <span class="stat-number">DEMO</span>
      <span class="stat-label">Mode</span>
    </div>

  </div>

  <!-- EUR/USD -->
  <div class="signal">

    <div class="signal-top">
      <div class="pair">EUR/USD</div>
      <div class="buy">BUY</div>
    </div>

    <div class="details">
      <div class="detail">Entry: Example price</div>
      <div class="detail">Stop Loss: Example price</div>
      <div class="detail">Take Profit: Example price</div>
    </div>

    <div class="status">● Example signal</div>

  </div>

  <!-- GBP/USD -->
  <div class="signal">

    <div class="signal-top">
      <div class="pair">GBP/USD</div>
      <div class="sell">SELL</div>
    </div>

    <div class="details">
      <div class="detail">Entry: Example price</div>
      <div class="detail">Stop Loss: Example price</div>
      <div class="detail">Take Profit: Example price</div>
    </div>

    <div class="status">● Example signal</div>

  </div>

  <!-- GOLD -->
  <div class="signal">

    <div class="signal-top">
      <div class="pair">XAU/USD — GOLD</div>
      <div class="buy">BUY</div>
    </div>

    <div class="details">
      <div class="detail">Entry: Example price</div>
      <div class="detail">Stop Loss: Example price</div>
      <div class="detail">Take Profit: Example price</div>
    </div>

    <div class="status">● Example signal</div>

  </div>

  <button class="refresh" onclick="location.reload()">
    🔄 Refresh Dashboard
  </button>

  <p class="notice">
    Demo interface for educational purposes. The displayed prices are examples
    and are not live market data or financial advice.
  </p>

</div>

</body>
</html>
