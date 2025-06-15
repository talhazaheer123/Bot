<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>DREAM TRADER BOT</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to right, #1a1a2e, #16213e, #0f3460);
      color: #fff;
      text-align: center;
      padding: 30px;
    }
    .box {
      background: #212f45;
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0 0 20px rgba(0,255,200,0.2);
      max-width: 600px;
      margin: auto;
    }
    select, input[type="password"], button {
      width: 85%;
      padding: 12px;
      margin: 12px 0;
      border-radius: 12px;
      border: none;
      font-size: 16px;
    }
    button {
      background-color: #00ffa1;
      color: #000;
      cursor: pointer;
      font-weight: bold;
      transition: background 0.3s ease;
    }
    button:hover:enabled {
      background-color: #00cc88;
    }
    .hidden { display: none; }
    .signal {
      background: #fff;
      color: #000;
      margin: 10px;
      padding: 12px;
      border-radius: 12px;
      font-weight: bold;
      animation: fadeIn 0.5s ease-in-out;
    }
    #timer {
      font-size: 20px;
      margin-top: 10px;
    }
    @keyframes fadeIn {
      from {opacity: 0;}
      to {opacity: 1;}
    }
  </style>
</head>
<body>
  <div class="box" id="loginBox">
    <h2>🔐 Enter Password</h2>
    <input type="password" id="passwordInput" placeholder="Enter Password"/>
    <button onclick="checkPassword()">Unlock</button>
  </div>

  <div class="box hidden" id="mainBox">
    <h2>💹 DREAM TRADER BOT 😎</h2>

    <select id="pairSelect">
      <option value="USD/BRL-OTC">USD/BRL-OTC</option>
      <option value="USD/ARS-OTC">USD/ARS-OTC</option>
      <option value="USD/PKR-OTC">USD/PKR-OTC</option>
      <option value="USD/INR-OTC">USD/INR-OTC</option>
      <option value="USD/BDT-OTC">USD/BDT-OTC</option>
      <option value="USD/JPY-OTC">USD/JPY-OTC</option>
      <option value="EUR/USD-OTC">EUR/USD-OTC</option>
      <option value="EUR/GBP-OTC">EUR/GBP-OTC</option>
      <option value="EUR/AUD-OTC">EUR/AUD-OTC</option>
      <option value="GBP/USD-OTC">GBP/USD-OTC</option>
      <option value="BRL/USD-OTC">BRL/USD-OTC</option>
      <option value="USD/MXN-OTC">USD/MXN-OTC</option>
      <option value="NZD/USD-OTC">NZD/USD-OTC</option>
    </select>

    <select id="timeframeSelect">
      <option value="1m">1 Minute</option>
      <option value="5m">5 Minute</option>
      <option value="15m">15 Minute</option>
      <option value="30m">30 Minute</option>
      <option value="1h">1 Hour</option>
    </select>

    <button id="generateBtn" onclick="generateSignal()">📡 Generate Signal</button>
    <div id="timer"></div>
    <div id="signalsContainer"></div>
  </div>

  <script>
    const PASSWORD = "12345";

    function checkPassword() {
      const input = document.getElementById('passwordInput').value;
      if (input === PASSWORD) {
        document.getElementById('loginBox').classList.add('hidden');
        document.getElementById('mainBox').classList.remove('hidden');
      } else {
        alert('Wrong password!');
      }
    }

    function generateSignal() {
      const pair = document.getElementById('pairSelect').value;
      const time = document.getElementById('timeframeSelect').value;
      const direction = Math.random() < 0.5 ? "BUY ⬆️" : "SELL ⬇️";
      const accuracy = Math.floor(Math.random() * 6) + 94; // 94% - 99%
      const now = new Date();
      const hour = String(now.getHours()).padStart(2, '0');
      const minute = String(now.getMinutes()).padStart(2, '0');

      const signalText = `${hour}:${minute} - ${pair} - ${direction} 🎯 (Accuracy: ${accuracy}%)`;

      const div = document.createElement('div');
      div.className = 'signal';
      div.innerText = signalText;

      const container = document.getElementById('signalsContainer');
      container.innerHTML = "";
      container.appendChild(div);

      // Disable button and start 3-second timer
      const btn = document.getElementById('generateBtn');
      btn.disabled = true;
      const timer = document.getElementById('timer');

      let timeLeft = 3;
      timer.innerText = `⏳ Next signal in ${timeLeft} seconds...`;
      const countdown = setInterval(() => {
        timeLeft--;
        if (timeLeft > 0) {
          timer.innerText = `⏳ Next signal in ${timeLeft} seconds...`;
        } else {
          clearInterval(countdown);
          timer.innerText = "";
          btn.disabled = false;
        }
      }, 1000);
    }
  </script>
</body>
</html>
