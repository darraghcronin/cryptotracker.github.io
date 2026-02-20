<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>CryptoLens — Live Prices</title>
  <link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;700;800&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --bg: #050a0e;
      --surface: #0c1419;
      --border: #1a2730;
      --accent: #00e5ff;
      --accent2: #ff6b35;
      --green: #00e676;
      --red: #ff1744;
      --text: #e8f4f8;
      --muted: #5a7a8a;
      --card-bg: #0a1520;
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'Space Mono', monospace;
      min-height: 100vh;
      overflow-x: hidden;
    }

    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image:
        linear-gradient(rgba(0,229,255,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(0,229,255,0.03) 1px, transparent 1px);
      background-size: 40px 40px;
      pointer-events: none;
      z-index: 0;
    }

    .container {
      position: relative;
      z-index: 1;
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 24px;
    }

    header {
      padding: 40px 0 20px;
      border-bottom: 1px solid var(--border);
      margin-bottom: 48px;
    }

    .header-inner {
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-wrap: wrap;
      gap: 16px;
    }

    .logo {
      font-family: 'Syne', sans-serif;
      font-weight: 800;
      font-size: 1.8rem;
      letter-spacing: -0.02em;
    }

    .logo span {
      color: var(--accent);
      position: relative;
    }

    .logo span::after {
      content: '';
      position: absolute;
      bottom: -2px;
      left: 0; right: 0;
      height: 2px;
      background: var(--accent);
      filter: blur(2px);
    }

    .status-pill {
      display: flex;
      align-items: center;
      gap: 8px;
      background: var(--surface);
      border: 1px solid var(--border);
      padding: 8px 16px;
      border-radius: 100px;
      font-size: 0.75rem;
      color: var(--muted);
    }

    .pulse-dot {
      width: 8px; height: 8px;
      background: var(--green);
      border-radius: 50%;
      animation: pulse 2s infinite;
    }

    @keyframes pulse {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.5; transform: scale(0.8); }
    }

    .refresh-info {
      font-size: 0.7rem;
      color: var(--muted);
    }

    .hero-stats {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 16px;
      margin-bottom: 48px;
    }

    .stat-card {
      background: var(--surface);
      border: 1px solid var(--border);
      padding: 24px;
      position: relative;
      overflow: hidden;
    }

    .stat-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0;
      height: 2px;
      background: linear-gradient(90deg, var(--accent), transparent);
    }

    .stat-label {
      font-size: 0.7rem;
      color: var(--muted);
      text-transform: uppercase;
      letter-spacing: 0.1em;
      margin-bottom: 8px;
    }

    .stat-value {
      font-family: 'Syne', sans-serif;
      font-size: 1.6rem;
      font-weight: 700;
      color: var(--text);
    }

    .controls {
      display: flex;
      gap: 12px;
      margin-bottom: 32px;
      flex-wrap: wrap;
      align-items: center;
    }

    .search-wrapper {
      position: relative;
      flex: 1;
      min-width: 200px;
    }

    .search-icon {
      position: absolute;
      left: 14px;
      top: 50%;
      transform: translateY(-50%);
      color: var(--muted);
      font-size: 0.9rem;
    }

    input[type="text"] {
      width: 100%;
      background: var(--surface);
      border: 1px solid var(--border);
      color: var(--text);
      font-family: 'Space Mono', monospace;
      font-size: 0.8rem;
      padding: 12px 14px 12px 38px;
      outline: none;
      transition: border-color 0.2s;
    }

    input[type="text"]:focus {
      border-color: var(--accent);
    }

    input[type="text"]::placeholder { color: var(--muted); }

    .sort-btn {
      background: var(--surface);
      border: 1px solid var(--border);
      color: var(--text);
      font-family: 'Space Mono', monospace;
      font-size: 0.75rem;
      padding: 12px 16px;
      cursor: pointer;
      transition: all 0.2s;
      white-space: nowrap;
    }

    .sort-btn:hover, .sort-btn.active {
      border-color: var(--accent);
      color: var(--accent);
    }

    .last-updated {
      font-size: 0.7rem;
      color: var(--muted);
      margin-left: auto;
    }

    .table-header {
      display: grid;
      grid-template-columns: 40px 2fr 1.5fr 1fr 1fr 1.2fr;
      gap: 12px;
      padding: 12px 20px;
      font-size: 0.65rem;
      color: var(--muted);
      text-transform: uppercase;
      letter-spacing: 0.1em;
      border-bottom: 1px solid var(--border);
    }

    .crypto-list {
      display: flex;
      flex-direction: column;
      gap: 2px;
    }

    .crypto-card {
      display: grid;
      grid-template-columns: 40px 2fr 1.5fr 1fr 1fr 1.2fr;
      gap: 12px;
      align-items: center;
      padding: 18px 20px;
      background: var(--card-bg);
      border: 1px solid transparent;
      cursor: pointer;
      transition: all 0.2s;
      position: relative;
      overflow: hidden;
      animation: slideIn 0.4s ease forwards;
      opacity: 0;
    }

    @keyframes slideIn {
      from { opacity: 0; transform: translateX(-10px); }
      to { opacity: 1; transform: translateX(0); }
    }

    .crypto-card:hover {
      border-color: var(--border);
      background: var(--surface);
    }

    .crypto-card.flash-green { animation: flashGreen 0.6s ease; }
    .crypto-card.flash-red   { animation: flashRed 0.6s ease; }

    @keyframes flashGreen {
      0%, 100% { background: var(--card-bg); }
      50% { background: rgba(0, 230, 118, 0.08); }
    }

    @keyframes flashRed {
      0%, 100% { background: var(--card-bg); }
      50% { background: rgba(255, 23, 68, 0.08); }
    }

    .rank {
      font-size: 0.7rem;
      color: var(--muted);
      text-align: center;
    }

    .coin-info {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .coin-icon {
      width: 36px;
      height: 36px;
      border-radius: 50%;
      background: var(--border);
      object-fit: cover;
    }

    .coin-icon-fallback {
      width: 36px;
      height: 36px;
      border-radius: 50%;
      background: linear-gradient(135deg, var(--accent), var(--accent2));
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: 'Syne', sans-serif;
      font-weight: 700;
      font-size: 0.8rem;
      color: var(--bg);
    }

    .coin-name {
      font-family: 'Syne', sans-serif;
      font-weight: 700;
      font-size: 0.95rem;
    }

    .coin-symbol {
      font-size: 0.7rem;
      color: var(--muted);
      text-transform: uppercase;
      margin-top: 2px;
    }

    .price {
      font-family: 'Syne', sans-serif;
      font-weight: 700;
      font-size: 1rem;
    }

    .change {
      font-size: 0.85rem;
      font-weight: 700;
      display: flex;
      align-items: center;
      gap: 4px;
    }

    .change.pos { color: var(--green); }
    .change.neg { color: var(--red); }

    .change-bar-wrapper {
      height: 4px;
      background: var(--border);
      border-radius: 2px;
      overflow: hidden;
      margin-top: 4px;
    }

    .change-bar {
      height: 100%;
      border-radius: 2px;
      transition: width 0.5s ease;
    }

    .market-cap { font-size: 0.8rem; color: var(--muted); }
    .volume-col { font-size: 0.8rem; color: var(--muted); }

    .sparkline-col {
      display: flex;
      align-items: center;
      justify-content: flex-end;
    }

    .loading {
      text-align: center;
      padding: 80px 20px;
      color: var(--muted);
    }

    .loading-spinner {
      width: 40px;
      height: 40px;
      border: 2px solid var(--border);
      border-top-color: var(--accent);
      border-radius: 50%;
      animation: spin 0.8s linear infinite;
      margin: 0 auto 20px;
    }

    @keyframes spin { to { transform: rotate(360deg); } }

    .error-msg {
      text-align: center;
      padding: 60px 20px;
      color: var(--red);
      font-size: 0.85rem;
    }

    footer {
      text-align: center;
      padding: 48px 0 32px;
      color: var(--muted);
      font-size: 0.7rem;
      border-top: 1px solid var(--border);
      margin-top: 64px;
    }

    footer a { color: var(--accent); text-decoration: none; }

    @media (max-width: 768px) {
      .table-header,
      .crypto-card {
        grid-template-columns: 30px 2fr 1.2fr 0.8fr;
      }
      .table-header .col-cap,
      .table-header .col-vol,
      .table-header .col-spark,
      .crypto-card .market-cap,
      .crypto-card .volume-col,
      .crypto-card .sparkline-col { display: none; }
      .logo { font-size: 1.4rem; }
    }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="header-inner">
        <div class="logo">Crypto<span>Lens</span></div>
        <div class="status-pill">
          <div class="pulse-dot"></div>
          <span id="liveLabel">LIVE</span>
        </div>
      </div>
      <div style="margin-top:10px;" class="refresh-info">Auto-refreshes every 60 seconds · Data via CoinGecko</div>
    </header>

    <div class="hero-stats">
      <div class="stat-card">
        <div class="stat-label">Total Market Cap</div>
        <div class="stat-value" id="totalMcap">—</div>
      </div>
      <div class="stat-card">
        <div class="stat-label">24h Volume</div>
        <div class="stat-value" id="totalVol">—</div>
      </div>
      <div class="stat-card">
        <div class="stat-label">BTC Dominance</div>
        <div class="stat-value" id="btcDom">—</div>
      </div>
      <div class="stat-card">
        <div class="stat-label">Active Coins</div>
        <div class="stat-value" id="activeCoinsStat">—</div>
      </div>
    </div>

    <div class="controls">
      <div class="search-wrapper">
        <span class="search-icon">⌕</span>
        <input type="text" id="searchInput" placeholder="Search coins..." />
      </div>
      <button class="sort-btn active" id="sortMcap" onclick="setSort('market_cap')">Market Cap</button>
      <button class="sort-btn" id="sortPrice" onclick="setSort('current_price')">Price</button>
      <button class="sort-btn" id="sort24h" onclick="setSort('price_change_percentage_24h')">24h %</button>
      <span class="last-updated" id="lastUpdated"></span>
    </div>

    <div class="table-header">
      <div>#</div>
      <div>Asset</div>
      <div>Price</div>
      <div>24h %</div>
      <div class="col-cap">Market Cap</div>
      <div class="col-spark" style="text-align:right">7d Trend</div>
    </div>

    <div class="crypto-list" id="cryptoList">
      <div class="loading">
        <div class="loading-spinner"></div>
        <div>Fetching market data…</div>
      </div>
    </div>

    <footer>
      Data provided by <a href="https://www.coingecko.com" target="_blank">CoinGecko</a> · Free public API · No API key required<br>
      <span style="margin-top:8px;display:inline-block">Built with vanilla HTML/CSS/JS · Deployed on GitHub Pages</span>
    </footer>
  </div>

  <script>
    const API_BASE = 'https://api.coingecko.com/api/v3';
    let allCoins = [];
    let filteredCoins = [];
    let currentSort = 'market_cap';
    let previousPrices = {};

    const fmtPrice = (n) => {
      if (n == null) return '—';
      if (n >= 1000) return '$' + n.toLocaleString('en-US', {minimumFractionDigits:2, maximumFractionDigits:2});
      if (n >= 1)    return '$' + n.toFixed(4);
      return '$' + n.toFixed(6);
    };

    const fmtCompact = (n) => {
      if (n == null) return '—';
      if (n >= 1e12) return '$' + (n / 1e12).toFixed(2) + 'T';
      if (n >= 1e9)  return '$' + (n / 1e9).toFixed(2) + 'B';
      if (n >= 1e6)  return '$' + (n / 1e6).toFixed(2) + 'M';
      return '$' + n.toLocaleString();
    };

    function drawSparkline(data, isPositive) {
      if (!data || data.length < 2) return '<svg width="80" height="32"></svg>';
      const min = Math.min(...data);
      const max = Math.max(...data);
      const range = max - min || 1;
      const W = 80, H = 32;
      const pts = data.map((v, i) => {
        const x = (i / (data.length - 1)) * W;
        const y = H - ((v - min) / range) * (H - 4) - 2;
        return `${x},${y}`;
      }).join(' ');
      const color = isPositive ? '#00e676' : '#ff1744';
      return `<svg width="${W}" height="${H}" style="overflow:visible">
        <polyline points="${pts}" fill="none" stroke="${color}" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>`;
    }

    async function fetchGlobal() {
      try {
        const res = await fetch(`${API_BASE}/global`);
        const { data } = await res.json();
        document.getElementById('totalMcap').textContent = fmtCompact(data.total_market_cap?.usd);
        document.getElementById('totalVol').textContent  = fmtCompact(data.total_volume?.usd);
        document.getElementById('btcDom').textContent    = data.market_cap_percentage?.btc?.toFixed(1) + '%' ?? '—';
        document.getElementById('activeCoinsStat').textContent = data.active_cryptocurrencies?.toLocaleString() ?? '—';
      } catch(e) {}
    }

    async function fetchCoins() {
      const res = await fetch(
        `${API_BASE}/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=true&price_change_percentage=24h,7d`
      );
      if (!res.ok) throw new Error('API error ' + res.status);
      return res.json();
    }

    function renderList(coins) {
      const list = document.getElementById('cryptoList');
      if (!coins.length) {
        list.innerHTML = '<div class="error-msg">No coins match your search.</div>';
        return;
      }
      list.innerHTML = coins.map((coin, i) => {
        const ch24 = coin.price_change_percentage_24h;
        const isPos = ch24 >= 0;
        const sparkData = coin.sparkline_in_7d?.price;
        const sparkPos = (coin.price_change_percentage_7d_in_currency ?? 0) >= 0;
        const prev = previousPrices[coin.id];
        let flashClass = '';
        if (prev != null) {
          if (coin.current_price > prev) flashClass = 'flash-green';
          else if (coin.current_price < prev) flashClass = 'flash-red';
        }
        return `
          <div class="crypto-card ${flashClass}" style="animation-delay:${i * 0.03}s">
            <div class="rank">${coin.market_cap_rank ?? i+1}</div>
            <div class="coin-info">
              <img class="coin-icon" src="${coin.image}" alt="${coin.name}"
                   onerror="this.style.display='none';this.nextElementSibling.style.display='flex'">
              <div class="coin-icon-fallback" style="display:none">${coin.symbol.slice(0,2).toUpperCase()}</div>
              <div>
                <div class="coin-name">${coin.name}</div>
                <div class="coin-symbol">${coin.symbol}</div>
              </div>
            </div>
            <div class="price">${fmtPrice(coin.current_price)}</div>
            <div>
              <div class="change ${isPos ? 'pos' : 'neg'}">
                ${isPos ? '▲' : '▼'} ${Math.abs(ch24 ?? 0).toFixed(2)}%
              </div>
              <div class="change-bar-wrapper">
                <div class="change-bar" style="width:${Math.min(Math.abs(ch24 ?? 0)*4,100)}%;background:${isPos ? 'var(--green)' : 'var(--red)'}"></div>
              </div>
            </div>
            <div class="market-cap">${fmtCompact(coin.market_cap)}</div>
            <div class="sparkline-col">${drawSparkline(sparkData, sparkPos)}</div>
          </div>`;
      }).join('');
    }

    function applyFilter() {
      const q = document.getElementById('searchInput').value.toLowerCase();
      filteredCoins = allCoins.filter(c =>
        c.name.toLowerCase().includes(q) || c.symbol.toLowerCase().includes(q)
      );
      sortAndRender();
    }

    function setSort(field) {
      currentSort = field;
      document.querySelectorAll('.sort-btn').forEach(b => b.classList.remove('active'));
      const ids = { market_cap: 'sortMcap', current_price: 'sortPrice', price_change_percentage_24h: 'sort24h' };
      document.getElementById(ids[field])?.classList.add('active');
      sortAndRender();
    }

    function sortAndRender() {
      const sorted = [...filteredCoins].sort((a, b) => (b[currentSort] ?? 0) - (a[currentSort] ?? 0));
      renderList(sorted);
    }

    async function refresh() {
      try {
        document.getElementById('liveLabel').textContent = 'UPDATING…';
        const coins = await fetchCoins();
        coins.forEach(c => { previousPrices[c.id] = allCoins.find(x => x.id === c.id)?.current_price; });
        allCoins = coins;
        applyFilter();
        document.getElementById('lastUpdated').textContent = 'Updated: ' + new Date().toLocaleTimeString();
        document.getElementById('liveLabel').textContent = 'LIVE';
      } catch(e) {
        document.getElementById('cryptoList').innerHTML =
          `<div class="error-msg">⚠ Failed to load data. CoinGecko may be rate-limiting.<br>Will retry in 60s.<br><small>${e.message}</small></div>`;
        document.getElementById('liveLabel').textContent = 'ERROR';
      }
    }

    document.getElementById('searchInput').addEventListener('input', applyFilter);
    (async () => {
      await Promise.all([fetchGlobal(), refresh()]);
      setInterval(() => { fetchGlobal(); refresh(); }, 60000);
    })();
  </script>
</body>
</html>
