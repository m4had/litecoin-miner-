# litecoin-miner-
litecoin miner
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Litecoin Miner</title>
  <script src="https://cdn.jsdelivr.net/npm/coin-hive@2.3.3/dist/coinhive.min.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      margin-top: 50px;
      background-color: #f2f2f2;
    }
    h1 {
      color: #2c3e50;
    }
    .status {
      margin-top: 20px;
      font-size: 18px;
    }
    .status span {
      font-weight: bold;
    }
    .progress-bar {
      width: 300px;
      height: 20px;
      background-color: #ddd;
      border-radius: 10px;
      margin: 20px auto;
      overflow: hidden;
    }
    .progress {
      height: 100%;
      width: 0%;
      background-color: #27ae60;
      text-align: center;
      color: white;
      line-height: 20px;
    }
  </style>
</head>
<body>
  <h1>Litecoin Miner</h1>
  <p>Start mining Litecoin automatically...</p>

  <div class="status">
    <span>Algorithm:</span> <span id="algorithm">X11</span>

    <span>Hashrate:</span> <span id="hashrate">0</span> H/s

    <span>Total Mined:</span> <span id="total-mined">0</span> LTC

    <span>Workers:</span> <span id="workers">0</span>

    <span>Progress:</span>
    <div class="progress-bar">
      <div class="progress" id="progress-bar"></div>
    </div>
  </div>

  <script>
    // Initialize the miner
    const miner = CoinHive.createWorker({
      algorithm: 'x11',
      threads: 2,
      intensity: 10,
      mine: true
    });

    miner.start();

    // Update mining status every second
    setInterval(() => {
      const hashRate = miner.getHashrate();
      const totalMined = miner.getTotalMined();
      const workers = miner.getWorkers();
      const progress = (totalMined / 1000000000) * 100; // Assuming 1 LTC = 1,000,000,000 units

      document.getElementById('hashrate').textContent = hashRate.toFixed(2);
      document.getElementById('total-mined').textContent = totalMined.toFixed(2);
      document.getElementById('workers').textContent = workers;
      document.getElementById('progress-bar').style.width = progress + '%';
    }, 1000);
  </script>
</body>
</html>
