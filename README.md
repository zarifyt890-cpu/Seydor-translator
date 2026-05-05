# Seydor-translator
Just a random translator
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cyrothasim Translator</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 100%);
      color: #fff;
      padding: 20px;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .container {
      background: #222;
      border-radius: 12px;
      padding: 30px;
      max-width: 600px;
      width: 100%;
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
    }

    h1 {
      text-align: center;
      margin-bottom: 10px;
      font-size: 28px;
      background: linear-gradient(135deg, #00d4ff, #0099ff);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .subtitle {
      text-align: center;
      color: #aaa;
      margin-bottom: 25px;
      font-size: 14px;
    }

    .tabs {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
      border-bottom: 2px solid #444;
    }

    .tab-btn {
      padding: 10px 20px;
      background: none;
      border: none;
      color: #aaa;
      cursor: pointer;
      font-size: 14px;
      font-weight: 600;
      transition: all 0.3s ease;
      border-bottom: 3px solid transparent;
      margin-bottom: -2px;
    }

    .tab-btn:hover {
      color: #00d4ff;
    }

    .tab-btn.active {
      color: #00d4ff;
      border-bottom-color: #00d4ff;
    }

    .tab-content {
      display: none;
    }

    .tab-content.active {
      display: block;
    }

    textarea {
      width: 100%;
      height: 120px;
      padding: 12px;
      margin-bottom: 15px;
      font-size: 16px;
      background: #333;
      color: #fff;
      border: 2px solid #444;
      border-radius: 8px;
      resize: vertical;
      font-family: 'Courier New', monospace;
      transition: border-color 0.3s ease;
    }

    textarea:focus {
      outline: none;
      border-color: #00d4ff;
      box-shadow: 0 0 8px rgba(0, 212, 255, 0.2);
    }

    textarea::placeholder {
      color: #666;
    }

    .button-group {
      display: flex;
      gap: 10px;
      margin-bottom: 15px;
    }

    button {
      flex: 1;
      padding: 12px;
      background: linear-gradient(135deg, #00d4ff, #0099ff);
      color: #000;
      border: none;
      border-radius: 8px;
      font-size: 14px;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s ease;
    }

    button:hover {
      transform: translateY(-2px);
      box-shadow: 0 4px 16px rgba(0, 212, 255, 0.3);
    }

    button:active {
      transform: translateY(0);
    }

    .clear-btn {
      background: linear-gradient(135deg, #ff6b6b, #ff4757);
      color: white;
    }

    .clear-btn:hover {
      box-shadow: 0 4px 16px rgba(255, 71, 87, 0.3);
    }

    .copy-btn {
      background: linear-gradient(135deg, #34a853, #4caf50);
      color: white;
      width: auto;
      padding: 10px 15px;
    }

    .copy-btn:hover {
      box-shadow: 0 4px 16px rgba(76, 175, 80, 0.3);
    }

    .output {
      font-size: 24px;
      padding: 15px;
      background: #1a1a1a;
      border: 2px solid #444;
      border-radius: 8px;
      min-height: 80px;
      word-wrap: break-word;
      word-break: break-all;
      font-family: 'Courier New', monospace;
      line-height: 1.6;
      color: #00d4ff;
    }

    .output.empty {
      color: #666;
    }

    .character-map {
      margin-top: 25px;
      padding-top: 20px;
      border-top: 2px solid #444;
    }

    .character-map h3 {
      color: #00d4ff;
      margin-bottom: 15px;
      font-size: 14px;
    }

    .map-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(80px, 1fr));
      gap: 8px;
    }

    .map-item {
      background: #333;
      padding: 8px;
      border-radius: 4px;
      text-align: center;
      font-size: 12px;
      border: 1px solid #444;
    }

    .map-item-latin {
      color: #0099ff;
      font-weight: 600;
    }

    .map-item-cyro {
      color: #00d4ff;
      font-size: 16px;
      margin-top: 4px;
    }

    .toast {
      position: fixed;
      bottom: 20px;
      right: 20px;
      background: #34a853;
      color: white;
      padding: 12px 20px;
      border-radius: 8px;
      opacity: 0;
      transition: opacity 0.3s ease;
      pointer-events: none;
    }

    .toast.show {
      opacity: 1;
      pointer-events: auto;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>⚔️ Cyrothasim Translator</h1>
    <p class="subtitle">Convert between English and Ancient Cyrothasim Script</p>

    <div class="tabs">
      <button class="tab-btn active" onclick="switchTab('translate')">Translate</button>
      <button class="tab-btn" onclick="switchTab('reverse')">Reverse</button>
      <button class="tab-btn" onclick="switchTab('map')">Character Map</button>
    </div>

    <!-- Translate Tab -->
    <div id="translate" class="tab-content active">
      <textarea id="input" placeholder="Type English text here..."></textarea>
      <div class="button-group">
        <button onclick="translateText()">Translate to Cyrothasim</button>
        <button class="clear-btn" onclick="clearInput()">Clear</button>
      </div>
      <div class="output empty" id="output">Translation will appear here</div>
      <button class="copy-btn" onclick="copyToClipboard('output')">Copy</button>
    </div>

    <!-- Reverse Tab -->
    <div id="reverse" class="tab-content">
      <textarea id="input-reverse" placeholder="Paste Cyrothasim text here..."></textarea>
      <div class="button-group">
        <button onclick="reverseTranslate()">Translate to English</button>
        <button class="clear-btn" onclick="clearReverse()">Clear</button>
      </div>
      <div class="output empty" id="output-reverse">Reverse translation will appear here</div>
      <button class="copy-btn" onclick="copyToClipboard('output-reverse')">Copy</button>
    </div>

    <!-- Character Map Tab -->
    <div id="map" class="tab-content">
      <div class="character-map">
        <h3>📋 Character Mappings</h3>
        <div class="map-grid" id="mapGrid"></div>
      </div>
    </div>
  </div>

  <div class="toast" id="toast"></div>

  <script>
    const charMap = {
      "h": "𐌇",
      "e": "𐌄",
      "a": "𐌀",
      "r": "𐌑",
      "m": "𐌌",
      "o": "𐌎",
      "n": "𐌍",
      "f": "𐌅",
      "i": "𐌈",
      "s": "𐌒",
      "t": "𐌓",
      "w": "𐌕",
      "y": "𐌖",
      "b": "𐌁",
      "d": "𐌃",
      "k": "𐌂",
      "c": "𐌂",
      "p": "𐌏",
      "v": "𐌔",
      "j": "𐌉",
      "z": "𐌗",
      "q": "𐌐"
    };

    // Create reverse map
    const reverseMap = {};
    Object.entries(charMap).forEach(([key, value]) => {
      reverseMap[value] = key;
    });

    function switchTab(tabName) {
      // Hide all tabs
      document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
      document.querySelectorAll('.tab-btn').forEach(el => el.classList.remove('active'));

      // Show selected tab
      document.getElementById(tabName).classList.add('active');
      event.target.classList.add('active');

      // Generate character map if needed
      if (tabName === 'map' && !document.getElementById('mapGrid').innerHTML) {
        generateCharacterMap();
      }
    }

    function translateText() {
      const input = document.getElementById('input').value.toLowerCase();
      let output = '';

      for (let char of input) {
        output += charMap[char] || char;
      }

      const outputEl = document.getElementById('output');
      outputEl.textContent = output || 'Translation will appear here';
      outputEl.classList.toggle('empty', !output);
    }

    function reverseTranslate() {
      const input = document.getElementById('input-reverse').value;
      let output = '';

      for (let char of input) {
        output += reverseMap[char] || char;
      }

      const outputEl = document.getElementById('output-reverse');
      outputEl.textContent = output || 'Reverse translation will appear here';
      outputEl.classList.toggle('empty', !output);
    }

    function clearInput() {
      document.getElementById('input').value = '';
      const outputEl = document.getElementById('output');
      outputEl.textContent = 'Translation will appear here';
      outputEl.classList.add('empty');
    }

    function clearReverse() {
      document.getElementById('input-reverse').value = '';
      const outputEl = document.getElementById('output-reverse');
      outputEl.textContent = 'Reverse translation will appear here';
      outputEl.classList.add('empty');
    }

    function copyToClipboard(elementId) {
      const text = document.getElementById(elementId).textContent;
      if (text === 'Translation will appear here' || text === 'Reverse translation will appear here') {
        showToast('Nothing to copy!');
        return;
      }
      navigator.clipboard.writeText(text).then(() => {
        showToast('Copied to clipboard!');
      }).catch(() => {
        showToast('Failed to copy');
      });
    }

    function showToast(message) {
      const toast = document.getElementById('toast');
      toast.textContent = message;
      toast.classList.add('show');
      setTimeout(() => toast.classList.remove('show'), 2000);
    }

    function generateCharacterMap() {
      const mapGrid = document.getElementById('mapGrid');
      Object.entries(charMap).forEach(([latin, cyro]) => {
        const item = document.createElement('div');
        item.className = 'map-item';
        item.innerHTML = `<div class="map-item-latin">${latin.toUpperCase()}</div><div class="map-item-cyro">${cyro}</div>`;
        mapGrid.appendChild(item);
      });
    }

    // Keyboard shortcuts
    document.addEventListener('keydown', (e) => {
      if (e.ctrlKey && e.key === 'Enter') {
        const activeTab = document.querySelector('.tab-content.active');
        if (activeTab.id === 'translate') translateText();
        else if (activeTab.id === 'reverse') reverseTranslate();
      }
    });

    // Live translation
    document.getElementById('input').addEventListener('input', translateText);
    document.getElementById('input-reverse').addEventListener('input', reverseTranslate);
  </script>
</body>
</html>
