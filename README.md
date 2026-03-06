<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DOS Education - Digital Online Studies</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;600&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0f;
    --surface: #111118;
    --card: #16161f;
    --border: #1e1e2e;
    --accent: #00ffe0;
    --accent2: #ff3e6c;
    --accent3: #ffe100;
    --text: #e0e0f0;
    --muted: #555577;
    --glow: 0 0 12px #00ffe055;
  }
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { background: var(--bg); color: var(--text); font-family: 'Rajdhani', sans-serif; min-height: 100vh; overflow-x: hidden; }
  body::before { content: ''; position: fixed; inset: 0; background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,255,224,0.015) 2px, rgba(0,255,224,0.015) 4px); pointer-events: none; z-index: 9999; }
  body::after { content: ''; position: fixed; inset: 0; background-image: linear-gradient(rgba(0,255,224,0.03) 1px, transparent 1px), linear-gradient(90deg, rgba(0,255,224,0.03) 1px, transparent 1px); background-size: 40px 40px; pointer-events: none; z-index: 0; }
  header { position: sticky; top: 0; z-index: 100; background: rgba(10,10,15,0.92); backdrop-filter: blur(12px); border-bottom: 1px solid var(--border); padding: 14px 32px; display: flex; align-items: center; justify-content: space-between; }
  .logo { font-family: 'Orbitron', monospace; font-size: 1.4rem; font-weight: 900; letter-spacing: 2px; color: var(--accent); text-shadow: var(--glow); }
  .logo span { color: var(--text); }
  .tagline { font-size: 0.75rem; letter-spacing: 4px; color: var(--muted); text-transform: uppercase; margin-top: 2px; }
  .nav-right { display: flex; gap: 20px; font-size: 0.85rem; letter-spacing: 1px; color: var(--muted); align-items: center; }
  .nav-right > span { cursor: pointer; transition: color 0.2s; }
  .nav-right > span:hover { color: var(--accent); }

  /* Resources dropdown */
  .nav-resources { position: relative; }
  .nav-resources > span { cursor: pointer; transition: color 0.2s; }
  .nav-resources > span:hover, .nav-resources:hover > span { color: var(--accent); }
  .resources-dropdown { display: none; position: absolute; top: calc(100% + 14px); right: 0; background: rgba(10,10,15,0.97); border: 1px solid var(--border); border-radius: 8px; min-width: 230px; z-index: 200; box-shadow: 0 12px 40px rgba(0,0,0,0.7); overflow: hidden; animation: dropIn 0.15s ease; }
  @keyframes dropIn { from { opacity: 0; transform: translateY(-6px); } to { opacity: 1; transform: translateY(0); } }
  .nav-resources:hover .resources-dropdown { display: block; }
  .dropdown-label { font-family: 'Orbitron', monospace; font-size: 0.6rem; letter-spacing: 3px; color: var(--muted); padding: 12px 16px 8px; text-transform: uppercase; border-bottom: 1px solid var(--border); }
  .dropdown-item { display: flex; align-items: center; gap: 10px; padding: 11px 16px; color: var(--text); font-size: 0.83rem; letter-spacing: 0.5px; cursor: pointer; transition: background 0.15s, color 0.15s; text-decoration: none; border-bottom: 1px solid var(--border); }
  .dropdown-item:last-child { border-bottom: none; }
  .dropdown-item:hover { background: rgba(0,255,224,0.07); color: var(--accent); }
  .di-icon { font-size: 1rem; flex-shrink: 0; }
  .di-text { display: flex; flex-direction: column; }
  .di-name { font-weight: 600; }
  .di-sub { font-size: 0.7rem; color: var(--muted); margin-top: 1px; }

  .scroll-target { scroll-margin-top: 74px; }
  .hero { position: relative; z-index: 1; padding: 48px 32px 24px; text-align: center; }
  .hero h1 { font-family: 'Orbitron', monospace; font-size: clamp(1.5rem, 4vw, 3rem); font-weight: 900; letter-spacing: 3px; color: var(--text); margin-bottom: 10px; }
  .hero h1 em { font-style: normal; color: var(--accent); text-shadow: var(--glow); }
  .hero p { color: var(--muted); font-size: 1rem; letter-spacing: 2px; text-transform: uppercase; margin-bottom: 28px; }
  .controls { position: relative; z-index: 1; display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; padding: 0 32px 28px; }
  .search-box { background: var(--card); border: 1px solid var(--border); border-radius: 4px; padding: 10px 20px; color: var(--text); font-family: 'Rajdhani', sans-serif; font-size: 1rem; letter-spacing: 1px; width: 280px; outline: none; transition: border-color 0.2s, box-shadow 0.2s; }
  .search-box:focus { border-color: var(--accent); box-shadow: var(--glow); }
  .filter-btn { background: var(--card); border: 1px solid var(--border); border-radius: 4px; padding: 10px 18px; color: var(--muted); font-family: 'Rajdhani', sans-serif; font-size: 0.9rem; letter-spacing: 1px; cursor: pointer; transition: all 0.2s; text-transform: uppercase; }
  .filter-btn:hover, .filter-btn.active { border-color: var(--accent); color: var(--accent); box-shadow: var(--glow); }
  .section { position: relative; z-index: 1; padding: 0 32px 48px; }
  .section-title { font-family: 'Orbitron', monospace; font-size: 0.85rem; letter-spacing: 4px; color: var(--muted); text-transform: uppercase; margin-bottom: 20px; padding-bottom: 10px; border-bottom: 1px solid var(--border); display: flex; align-items: center; gap: 12px; }
  .section-title::before { content: ''; display: block; width: 4px; height: 16px; background: var(--accent); box-shadow: var(--glow); }
  .game-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 16px; }
  .game-card { background: var(--card); border: 1px solid var(--border); border-radius: 6px; overflow: hidden; cursor: pointer; transition: all 0.25s; text-decoration: none; display: block; position: relative; }
  .game-card:hover { border-color: var(--accent); transform: translateY(-4px); box-shadow: 0 8px 32px rgba(0,255,224,0.12); }
  .game-thumb-placeholder { width: 100%; height: 120px; display: flex; align-items: center; justify-content: center; font-size: 3rem; background: linear-gradient(135deg, #0d0d1a 0%, #12121e 100%); }
  .game-info { padding: 12px 14px; }
  .game-name { font-family: 'Orbitron', monospace; font-size: 0.75rem; font-weight: 700; letter-spacing: 1px; color: var(--text); margin-bottom: 4px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
  .game-desc { font-size: 0.8rem; color: var(--muted); line-height: 1.4; }
  .game-tag { position: absolute; top: 8px; right: 8px; background: rgba(0,0,0,0.75); backdrop-filter: blur(6px); border-radius: 3px; padding: 2px 7px; font-size: 0.65rem; font-family: 'Orbitron', monospace; letter-spacing: 1px; text-transform: uppercase; }
  .tag-all { color: var(--accent); border: 1px solid #00ffe044; }
  .tag-13 { color: var(--accent2); border: 1px solid #ff3e6c44; }
  .tag-hot { color: var(--accent3); border: 1px solid #ffe10044; }
  .overlay { display: none; position: fixed; inset: 0; z-index: 9998; background: rgba(0,0,0,0.92); flex-direction: column; align-items: center; justify-content: center; backdrop-filter: blur(8px); }
  .overlay.open { display: flex; }
  .launch-box { background: var(--card); border: 1px solid var(--accent); border-radius: 10px; padding: 48px 56px; text-align: center; max-width: 420px; width: 90%; box-shadow: 0 0 60px rgba(0,255,224,0.15); animation: popIn 0.2s ease; }
  @keyframes popIn { from { transform: scale(0.9); opacity: 0; } to { transform: scale(1); opacity: 1; } }
  .launch-emoji { font-size: 4rem; margin-bottom: 16px; }
  .overlay-title { font-family: 'Orbitron', monospace; font-size: 1rem; color: var(--accent); letter-spacing: 2px; margin-bottom: 10px; }
  .launch-desc { color: var(--muted); font-size: 0.85rem; letter-spacing: 1px; margin-bottom: 28px; line-height: 1.6; }
  .btn-play { background: var(--accent); color: #000; border: none; border-radius: 5px; padding: 12px 32px; font-family: 'Orbitron', monospace; font-size: 0.85rem; font-weight: 700; letter-spacing: 2px; cursor: pointer; transition: opacity 0.2s, transform 0.15s; display: block; width: 100%; margin-bottom: 12px; }
  .btn-play:hover { opacity: 0.85; transform: scale(1.02); }
  .overlay-close { background: transparent; color: var(--muted); border: 1px solid var(--border); border-radius: 5px; padding: 10px 32px; font-family: 'Orbitron', monospace; font-size: 0.75rem; letter-spacing: 1px; cursor: pointer; transition: all 0.2s; display: block; width: 100%; }
  .overlay-close:hover { border-color: var(--accent2); color: var(--accent2); }
  .ticker { background: var(--accent); color: #000; padding: 6px 0; overflow: hidden; position: relative; z-index: 1; margin-bottom: 32px; }
  .ticker-inner { display: flex; gap: 60px; animation: ticker 30s linear infinite; white-space: nowrap; font-family: 'Orbitron', monospace; font-size: 0.7rem; font-weight: 700; letter-spacing: 2px; }
  @keyframes ticker { from { transform: translateX(0); } to { transform: translateX(-50%); } }
  @keyframes pulse { 0%, 100% { opacity: 1; transform: scale(1); } 50% { opacity: 0.4; transform: scale(0.85); } }
  .proxy-card { display: flex; gap: 16px; background: var(--card); border: 1px solid var(--border); border-radius: 8px; padding: 18px; text-decoration: none; transition: all 0.25s; align-items: flex-start; }
  .proxy-card:hover { border-color: #5865F2; transform: translateY(-3px); box-shadow: 0 8px 28px rgba(88,101,242,0.15); }
  .proxy-icon { font-size: 2rem; flex-shrink: 0; margin-top: 2px; }
  .proxy-name { font-family: 'Orbitron', monospace; font-size: 0.78rem; font-weight: 700; letter-spacing: 1px; color: var(--text); margin-bottom: 6px; }
  .proxy-desc { font-size: 0.82rem; color: var(--muted); line-height: 1.5; margin-bottom: 10px; }
  .proxy-tags { display: flex; flex-wrap: wrap; gap: 6px; }
  .ptag { background: rgba(88,101,242,0.12); border: 1px solid rgba(88,101,242,0.3); color: #9aa0f5; border-radius: 3px; padding: 2px 8px; font-size: 0.7rem; font-family: 'Orbitron', monospace; }
  .app-card { display: flex; align-items: center; gap: 14px; background: var(--card); border: 1px solid var(--border); border-radius: 8px; padding: 14px 16px; text-decoration: none; transition: all 0.22s; }
  .app-card:hover { border-color: var(--c, var(--accent)); transform: translateY(-2px); box-shadow: 0 6px 20px rgba(0,0,0,0.3); }
  .app-icon { font-size: 1.8rem; flex-shrink: 0; }
  .app-name { font-family: 'Orbitron', monospace; font-size: 0.72rem; font-weight: 700; letter-spacing: 1px; color: var(--text); margin-bottom: 3px; }
  .app-desc { font-size: 0.78rem; color: var(--muted); }
  @media(max-width: 600px) { header { padding: 12px 16px; } .section { padding: 0 16px 32px; } .controls { padding: 0 16px 20px; } .hero { padding: 32px 16px 16px; } .game-grid { grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); gap: 12px; } }
</style>
</head>
<body>

<header>
  <div>
    <div class="logo">DOS<span>education</span></div>
    <div class="tagline">Digital Online Studies — Interactive Learning Portal</div>
  </div>
  <div class="nav-right">
    <span onclick="document.getElementById('games-section').scrollIntoView({behavior:'smooth'})">Curriculum</span>
    <span onclick="window.location.href='https://destiny.follettlearning.com'" style="color:var(--accent3); border:1px solid #ffe10044; padding:6px 14px; border-radius:4px; font-family:'Orbitron',monospace; font-size:0.72rem; letter-spacing:1px; cursor:pointer; transition:all 0.2s;" onmouseover="this.style.background='#ffe10022'" onmouseout="this.style.background='transparent'">&#128218; DESTINY</span>
    <span onclick="stealthTab()" style="color:var(--accent2); border:1px solid #ff3e6c44; padding:6px 14px; border-radius:4px; font-family:'Orbitron',monospace; font-size:0.72rem; letter-spacing:1px; cursor:pointer; transition:all 0.2s;" onmouseover="this.style.background='#ff3e6c22'" onmouseout="this.style.background='transparent'">&#128272; CLOAK</span>

    <div class="nav-resources">
      <span>Resources &#9662;</span>
      <div class="resources-dropdown">
        <div class="dropdown-label">Jump to section</div>
        <a class="dropdown-item" onclick="goTo('resources-music')">
          <span class="di-icon">&#127925;</span>
          <span class="di-text"><span class="di-name">Music</span><span class="di-sub">Spotify, SoundCloud, YouTube Music</span></span>
        </a>
        <a class="dropdown-item" onclick="goTo('resources-chat')">
          <span class="di-icon">&#128172;</span>
          <span class="di-text"><span class="di-name">Chat</span><span class="di-sub">Discord, Telegram, Guilded</span></span>
        </a>
        <a class="dropdown-item" onclick="goTo('resources-video')">
          <span class="di-icon">&#127916;</span>
          <span class="di-text"><span class="di-name">Video &amp; Anime</span><span class="di-sub">YouTube, Crunchyroll, Twitch</span></span>
        </a>
        <a class="dropdown-item" onclick="goTo('resources-social')">
          <span class="di-icon">&#128241;</span>
          <span class="di-text"><span class="di-name">Social Media</span><span class="di-sub">Instagram, TikTok, Reddit</span></span>
        </a>
        <a class="dropdown-item" onclick="goTo('resources-tools')">
          <span class="di-icon">&#128296;</span>
          <span class="di-text"><span class="di-name">Tools &amp; Utilities</span><span class="di-sub">Canva, Figma, Notion, Replit</span></span>
        </a>
      </div>
    </div>

    <a href="https://discord.com/users/xuaoxiaolingy" target="_blank" style="text-decoration:none; display:flex; align-items:center; gap:8px; background:#5865F222; border:1px solid #5865F255; border-radius:5px; padding:7px 14px; color:#fff; font-family:'Rajdhani',sans-serif; font-size:0.85rem; letter-spacing:1px; transition:all 0.2s;" onmouseover="this.style.background='#5865F244';this.style.borderColor='#5865F2'" onmouseout="this.style.background='#5865F222';this.style.borderColor='#5865F255'">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="#5865F2"><path d="M20.317 4.37a19.791 19.791 0 0 0-4.885-1.515.074.074 0 0 0-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 0 0-5.487 0 12.64 12.64 0 0 0-.617-1.25.077.077 0 0 0-.079-.037A19.736 19.736 0 0 0 3.677 4.37a.07.07 0 0 0-.032.027C.533 9.046-.32 13.58.099 18.057c.002.022.015.043.032.053a19.9 19.9 0 0 0 5.993 3.03.077.077 0 0 0 .084-.028 14.09 14.09 0 0 0 1.226-1.994.076.076 0 0 0-.041-.106 13.107 13.107 0 0 1-1.872-.892.077.077 0 0 1-.008-.128 10.2 10.2 0 0 0 .372-.292.074.074 0 0 1 .077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 0 1 .078.01c.12.098.246.198.373.292a.077.077 0 0 1-.006.127 12.299 12.299 0 0 1-1.873.892.077.077 0 0 0-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 0 0 .084.028 19.839 19.839 0 0 0 6.002-3.03.077.077 0 0 0 .032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 0 0-.031-.03zM8.02 15.33c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.956-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.956 2.418-2.157 2.418zm7.975 0c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.955-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.946 2.418-2.157 2.418z"/></svg>
      <span style="color:#5865F2; font-weight:600;">xuaoxiaolingy</span>
    </a>
  </div>
</header>

<div class="ticker">
  <div class="ticker-inner">
    KRUNKER.IO &nbsp;&#183;&nbsp; SHELL SHOCKERS &nbsp;&#183;&nbsp; 1V1.LOL &nbsp;&#183;&nbsp; SLITHER.IO &nbsp;&#183;&nbsp; AGAR.IO &nbsp;&#183;&nbsp; DIEP.IO &nbsp;&#183;&nbsp; PAPER.IO &nbsp;&#183;&nbsp; ZOMBS.IO &nbsp;&#183;&nbsp; MINESWEEPER &nbsp;&#183;&nbsp; 2048 &nbsp;&#183;&nbsp; TETRIS &nbsp;&#183;&nbsp; SNAKE &nbsp;&#183;&nbsp; DRIFT BOSS &nbsp;&#183;&nbsp; VENGE.IO &nbsp;&#183;&nbsp; LORDZ.IO &nbsp;&#183;&nbsp; NOW LOADING... KRUNKER.IO &nbsp;&#183;&nbsp; SHELL SHOCKERS &nbsp;&#183;&nbsp; 1V1.LOL &nbsp;&#183;&nbsp; SLITHER.IO &nbsp;&#183;&nbsp; AGAR.IO &nbsp;&#183;&nbsp; DIEP.IO &nbsp;&#183;&nbsp; PAPER.IO &nbsp;&#183;&nbsp; ZOMBS.IO &nbsp;&#183;&nbsp; MINESWEEPER &nbsp;&#183;&nbsp; 2048 &nbsp;&#183;&nbsp; TETRIS &nbsp;&#183;&nbsp; SNAKE &nbsp;&#183;&nbsp; DRIFT BOSS &nbsp;&#183;&nbsp; VENGE.IO &nbsp;&#183;&nbsp; LORDZ.IO &nbsp;&#183;&nbsp; NOW LOADING...
  </div>
</div>

<div class="hero">
  <h1>DOS <em>UNBLOCKED</em> GAMES 2.0</h1>
  <p>Engage your brain &#8212; all platforms, all speeds</p>
</div>

<div class="controls">
  <input class="search-box" type="text" placeholder="Search modules..." id="searchInput" oninput="filterGames()">
  <button class="filter-btn active" onclick="setFilter('all', this)">All</button>
  <button class="filter-btn" onclick="setFilter('action', this)">Action</button>
  <button class="filter-btn" onclick="setFilter('io', this)">IO Games</button>
  <button class="filter-btn" onclick="setFilter('puzzle', this)">Puzzle</button>
  <button class="filter-btn" onclick="setFilter('racing', this)">Racing</button>
  <button class="filter-btn" onclick="setFilter('shooter', this)">Shooter</button>

  <button class="filter-btn" onclick="setFilter('idle', this)">Idle</button>
  <button class="filter-btn" onclick="setFilter('gore', this)">🩸 Gore</button>
</div>

<div class="section" id="games-section">
  <div class="section-title">&#128293; HOT RIGHT NOW</div>
  <div class="game-grid" id="gameGrid"></div>
</div>

<!-- ROBLOX -->
<div class="section" style="margin-top:8px;">
  <div class="section-title">&#127EB5; ROBLOX &#8212; PLAY ON CHROMEBOOK</div>
  <p style="color:var(--muted); font-size:0.85rem; letter-spacing:1px; margin-bottom:20px; line-height:1.7;">Roblox normally needs an app &#8212; but these cloud &amp; browser options let you play straight from Chrome with no downloads!</p>
  <a href="https://now.gg/apps/roblox-corporation/5349/roblox.html" target="_blank" style="display:flex; gap:20px; background: linear-gradient(135deg, #1a1a0f 0%, #2a2200 100%); border:2px solid #ffe10066; border-radius:10px; padding:24px; text-decoration:none; margin-bottom:20px; align-items:center; transition: all 0.25s;" onmouseover="this.style.borderColor='#ffe100';this.style.boxShadow='0 8px 32px rgba(255,225,0,0.2)'" onmouseout="this.style.borderColor='#ffe10066';this.style.boxShadow='none'">
    <div style="font-size:4rem; flex-shrink:0;">&#127918;</div>
    <div>
      <div style="font-family:'Orbitron',monospace; font-size:1rem; font-weight:900; color:#ffe100; letter-spacing:2px; margin-bottom:8px;">NOW.GG &#8212; CLOUD ROBLOX &#11088; BEST OPTION</div>
      <div style="color:#aaa; font-size:0.88rem; line-height:1.7; margin-bottom:12px;">Play Roblox <strong style="color:#fff">directly in your browser</strong> &#8212; no download, no install. Works on Chromebooks and school computers!</div>
      <div style="display:flex; gap:8px; flex-wrap:wrap;">
        <span style="background:#ffe10022; border:1px solid #ffe10055; color:#ffe100; border-radius:3px; padding:3px 10px; font-size:0.7rem; font-family:'Orbitron',monospace;">&#9989; NO DOWNLOAD</span>
        <span style="background:#ffe10022; border:1px solid #ffe10055; color:#ffe100; border-radius:3px; padding:3px 10px; font-size:0.7rem; font-family:'Orbitron',monospace;">&#9989; CHROMEBOOK</span>
        <span style="background:#ffe10022; border:1px solid #ffe10055; color:#ffe100; border-radius:3px; padding:3px 10px; font-size:0.7rem; font-family:'Orbitron',monospace;">&#9989; FREE</span>
      </div>
    </div>
  </a>
  <div style="display:grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap:14px;">
    <a href="https://www.coolmathgames.com/0-build-and-crush" target="_blank" class="proxy-card" style="flex-direction:column; gap:10px;"><div style="font-size:2.2rem;">&#127959;</div><div><div class="proxy-name">Build &amp; Crush</div><div class="proxy-desc">Build structures then destroy others &#8212; pure Roblox energy in the browser.</div></div></a>
    <a href="https://voxiom.io" target="_blank" class="proxy-card" style="flex-direction:column; gap:10px;"><div style="font-size:2.2rem;">&#9935;</div><div><div class="proxy-name">Voxiom.io</div><div class="proxy-desc">Minecraft + Fortnite vibes. Build, mine and battle in a voxel world.</div></div></a>
    <a href="https://www.kogama.com" target="_blank" class="proxy-card" style="flex-direction:column; gap:10px;"><div style="font-size:2.2rem;">&#127961;</div><div><div class="proxy-name">KoGaMa City</div><div class="proxy-desc">User-made worlds you can explore &#8212; literally Roblox in the browser.</div></div></a>
    <a href="https://www.coolmathgames.com/0-eggy-party" target="_blank" class="proxy-card" style="flex-direction:column; gap:10px;"><div style="font-size:2.2rem;">&#129370;</div><div><div class="proxy-name">Eggy Party</div><div class="proxy-desc">Fall Guys-style party game. Multiplayer chaos!</div></div></a>
  </div>
</div>

<!-- PROXIES -->
<div class="section" style="margin-top:8px; padding-bottom:60px;">
  <div class="section-title">&#127760; WEB PROXIES &#8212; BYPASS FILTERS</div>
  <p style="color:var(--muted); font-size:0.85rem; letter-spacing:1px; margin-bottom:20px; line-height:1.7;">These proxies let you access Roblox, YouTube, and other blocked sites through your browser.</p>
  <div style="display:grid; grid-template-columns: repeat(auto-fill, minmax(260px, 1fr)); gap:16px;">
    <a href="https://titaniumnetwork.org" target="_blank" class="proxy-card"><div class="proxy-icon">&#128311;</div><div class="proxy-info"><div class="proxy-name">Titanium Network</div><div class="proxy-desc">Ultraviolet proxy &#8212; supports Roblox, YouTube and most sites.</div><div class="proxy-tags"><span class="ptag">Roblox</span><span class="ptag">YouTube</span><span class="ptag">UV Proxy</span></div></div></a>
    <a href="https://holyubofficial.net" target="_blank" class="proxy-card"><div class="proxy-icon">&#128519;</div><div class="proxy-info"><div class="proxy-name">Holy Unblocker</div><div class="proxy-desc">Popular school bypass with built-in games and proxy tabs.</div><div class="proxy-tags"><span class="ptag">Games</span><span class="ptag">Sites</span><span class="ptag">Stealth</span></div></div></a>
    <a href="https://interstellarnetwork.pages.dev" target="_blank" class="proxy-card"><div class="proxy-icon">&#128640;</div><div class="proxy-info"><div class="proxy-name">Interstellar</div><div class="proxy-desc">Fast Cloudflare-hosted proxy with Ultraviolet backend.</div><div class="proxy-tags"><span class="ptag">Fast</span><span class="ptag">Cloudflare</span><span class="ptag">Games</span></div></div></a>
    <a href="https://3kh0.github.io" target="_blank" class="proxy-card"><div class="proxy-icon">&#127918;</div><div class="proxy-info"><div class="proxy-name">3kh0 Games + Proxy</div><div class="proxy-desc">GitHub-hosted unblocked games + web proxy. Tons of games included.</div><div class="proxy-tags"><span class="ptag">GitHub</span><span class="ptag">Games</span><span class="ptag">Proxy</span></div></div></a>
    <a href="https://hypertabs.cc" target="_blank" class="proxy-card"><div class="proxy-icon">&#128209;</div><div class="proxy-info"><div class="proxy-name">HyperTabs</div><div class="proxy-desc">Disguises browsing as Google Classroom. Perfect if teachers walk by.</div><div class="proxy-tags"><span class="ptag">Stealth</span><span class="ptag">&#128293; Smart</span></div></div></a>
    <a href="https://nebulaproxy.io" target="_blank" class="proxy-card"><div class="proxy-icon">&#127756;</div><div class="proxy-info"><div class="proxy-name">Nebula Proxy</div><div class="proxy-desc">Clean dark proxy. Good for social media and games at school.</div><div class="proxy-tags"><span class="ptag">Social</span><span class="ptag">Games</span></div></div></a>
  </div>
  <div style="margin-top:24px; background:var(--card); border:1px solid var(--border); border-left:3px solid var(--accent3); border-radius:6px; padding:16px 20px;">
    <div style="font-family:'Orbitron',monospace; font-size:0.75rem; color:var(--accent3); letter-spacing:2px; margin-bottom:8px;">&#128161; PRO TIPS</div>
    <div style="color:var(--muted); font-size:0.85rem; line-height:1.8;">
      &#8226; <strong style="color:var(--text)">Cloudflare Pages (.pages.dev)</strong> and <strong style="color:var(--text)">GitHub Pages (.github.io)</strong> are hardest to block<br>
      &#8226; Use <strong style="color:var(--text)">HyperTabs</strong> if teachers walk by &#8212; it looks like Google Classroom<br>
      &#8226; For Roblox specifically, <strong style="color:var(--text)">Ultraviolet proxy</strong> (Titanium/Interstellar) works best
    </div>
  </div>
</div>

<!-- RESOURCES / APPS SECTION -->
<div class="section scroll-target" id="resources" style="margin-top:8px;">
  <div class="section-title">&#128241; UNBLOCKED APPS &amp; RESOURCES</div>
  <p style="color:var(--muted); font-size:0.85rem; letter-spacing:1px; margin-bottom:24px; line-height:1.7;">All browser-based &#8212; no downloads needed. Works on Chromebook &amp; school computers.</p>

  <div id="resources-music" class="scroll-target" style="font-family:'Orbitron',monospace; font-size:0.72rem; color:var(--muted); letter-spacing:3px; margin-bottom:12px;">&#127925; MUSIC</div>
  <div style="display:grid; grid-template-columns:repeat(auto-fill,minmax(200px,1fr)); gap:12px; margin-bottom:28px;">
    <a href="https://open.spotify.com" target="_blank" class="app-card" style="--c:#1DB954"><span class="app-icon">&#127911;</span><div><div class="app-name">Spotify Web</div><div class="app-desc">Stream any song free in browser</div></div></a>
    <a href="https://soundcloud.com" target="_blank" class="app-card" style="--c:#ff5500"><span class="app-icon">&#9729;</span><div><div class="app-name">SoundCloud</div><div class="app-desc">Free music &amp; underground tracks</div></div></a>
    <a href="https://music.youtube.com" target="_blank" class="app-card" style="--c:#ff0000"><span class="app-icon">&#9654;</span><div><div class="app-name">YouTube Music</div><div class="app-desc">Free YouTube Music web player</div></div></a>
    <a href="https://www.pandora.com" target="_blank" class="app-card" style="--c:#005483"><span class="app-icon">&#128251;</span><div><div class="app-name">Pandora</div><div class="app-desc">Free radio &amp; music stations</div></div></a>
  </div>

  <div id="resources-chat" class="scroll-target" style="font-family:'Orbitron',monospace; font-size:0.72rem; color:var(--muted); letter-spacing:3px; margin-bottom:12px;">&#128172; CHAT</div>
  <div style="display:grid; grid-template-columns:repeat(auto-fill,minmax(200px,1fr)); gap:12px; margin-bottom:28px;">
    <a href="https://discord.com/app" target="_blank" class="app-card" style="--c:#5865F2"><span class="app-icon">&#127918;</span><div><div class="app-name">Discord Web</div><div class="app-desc">Chat with friends in browser</div></div></a>
    <a href="https://web.telegram.org" target="_blank" class="app-card" style="--c:#2AABEE"><span class="app-icon">&#9992;</span><div><div class="app-name">Telegram Web</div><div class="app-desc">Instant messaging, no app needed</div></div></a>
    <a href="https://app.guilded.gg" target="_blank" class="app-card" style="--c:#F5C518"><span class="app-icon">&#128737;</span><div><div class="app-name">Guilded</div><div class="app-desc">Discord alternative &#8212; less blocked</div></div></a>
    <a href="https://groupme.com" target="_blank" class="app-card" style="--c:#00b5e2"><span class="app-icon">&#128172;</span><div><div class="app-name">GroupMe</div><div class="app-desc">Group chat for free in browser</div></div></a>
  </div>

  <div id="resources-video" class="scroll-target" style="font-family:'Orbitron',monospace; font-size:0.72rem; color:var(--muted); letter-spacing:3px; margin-bottom:12px;">&#127916; VIDEO &amp; ANIME</div>
  <div style="display:grid; grid-template-columns:repeat(auto-fill,minmax(200px,1fr)); gap:12px; margin-bottom:28px;">
    <a href="https://www.youtube.com" target="_blank" class="app-card" style="--c:#ff0000"><span class="app-icon">&#128250;</span><div><div class="app-name">YouTube</div><div class="app-desc">Watch videos free</div></div></a>
    
    
    <a href="https://9animetv.to" target="_blank" class="app-card" style="--c:#9b59b6"><span class="app-icon">&#127800;</span><div><div class="app-name">9AnimeTV</div><div class="app-desc">Watch anime free, no login</div></div></a>
    <a href="https://www.twitch.tv" target="_blank" class="app-card" style="--c:#9146FF"><span class="app-icon">&#128995;</span><div><div class="app-name">Twitch</div><div class="app-desc">Watch live game streams</div></div></a>
    
  </div>

  <div id="resources-social" class="scroll-target" style="font-family:'Orbitron',monospace; font-size:0.72rem; color:var(--muted); letter-spacing:3px; margin-bottom:12px;">&#128241; SOCIAL MEDIA</div>
  <div style="display:grid; grid-template-columns:repeat(auto-fill,minmax(200px,1fr)); gap:12px; margin-bottom:28px;">
    <a href="https://www.instagram.com" target="_blank" class="app-card" style="--c:#e1306c"><span class="app-icon">&#128248;</span><div><div class="app-name">Instagram</div><div class="app-desc">Browse IG in browser</div></div></a>
    <a href="https://twitter.com" target="_blank" class="app-card" style="--c:#1DA1F2"><span class="app-icon">&#128038;</span><div><div class="app-name">Twitter / X</div><div class="app-desc">Browse X without the app</div></div></a>
    <a href="https://www.tiktok.com" target="_blank" class="app-card" style="--c:#ff0050"><span class="app-icon">&#127925;</span><div><div class="app-name">TikTok Web</div><div class="app-desc">Scroll TikTok in Chrome</div></div></a>
    <a href="https://www.reddit.com" target="_blank" class="app-card" style="--c:#ff4500"><span class="app-icon">&#128125;</span><div><div class="app-name">Reddit</div><div class="app-desc">Browse memes &amp; communities</div></div></a>
    <a href="https://www.pinterest.com" target="_blank" class="app-card" style="--c:#e60023"><span class="app-icon">&#128204;</span><div><div class="app-name">Pinterest</div><div class="app-desc">Browse aesthetic content</div></div></a>
    <a href="https://www.snapchat.com/web" target="_blank" class="app-card" style="--c:#FFFC00"><span class="app-icon">&#128123;</span><div><div class="app-name">Snapchat Web</div><div class="app-desc">Send snaps from browser</div></div></a>
  </div>

  <div id="resources-tools" class="scroll-target" style="font-family:'Orbitron',monospace; font-size:0.72rem; color:var(--muted); letter-spacing:3px; margin-bottom:12px;">&#128296; TOOLS &amp; UTILITIES</div>
  <div style="display:grid; grid-template-columns:repeat(auto-fill,minmax(200px,1fr)); gap:12px; margin-bottom:8px;">
    <a href="https://docs.google.com" target="_blank" class="app-card" style="--c:#4285F4"><span class="app-icon">&#128196;</span><div><div class="app-name">Google Docs</div><div class="app-desc">Free word processing online</div></div></a>
    <a href="https://www.canva.com" target="_blank" class="app-card" style="--c:#00c4cc"><span class="app-icon">&#127912;</span><div><div class="app-name">Canva</div><div class="app-desc">Design graphics &amp; posters free</div></div></a>
    <a href="https://www.figma.com" target="_blank" class="app-card" style="--c:#f24e1e"><span class="app-icon">&#9999;</span><div><div class="app-name">Figma</div><div class="app-desc">UI design tool &#8212; browser based</div></div></a>
    <a href="https://replit.com" target="_blank" class="app-card" style="--c:#f26207"><span class="app-icon">&#128187;</span><div><div class="app-name">Replit</div><div class="app-desc">Code anything in browser</div></div></a>
    <a href="https://www.photopea.com" target="_blank" class="app-card" style="--c:#1b73e8"><span class="app-icon">&#128444;</span><div><div class="app-name">Photopea</div><div class="app-desc">Free Photoshop in browser</div></div></a>
    <a href="https://www.notion.so" target="_blank" class="app-card" style="--c:#ffffff"><span class="app-icon">&#128221;</span><div><div class="app-name">Notion</div><div class="app-desc">Notes, todos &amp; planning</div></div></a>
  </div>
</div>

<!-- LIVE CHAT -->
<div class="section" style="margin-top:8px; padding-bottom:60px;">
  <div class="section-title">&#128172; LIVE CHAT &#8212; TALK TO VISITORS</div>
  <p style="color:var(--muted); font-size:0.85rem; letter-spacing:1px; margin-bottom:20px; line-height:1.7;">Chat live with everyone visiting the site right now! Messages are real &#8212; anyone on the site sees them. &#128293;</p>
  <div style="background:var(--card); border:1px solid var(--border); border-radius:10px; overflow:hidden; max-width:720px;">
    <div style="padding:12px 18px; background:var(--surface); border-bottom:1px solid var(--border); display:flex; align-items:center; justify-content:space-between;">
      <div style="display:flex; align-items:center; gap:10px;">
        <span style="display:inline-block; width:9px; height:9px; background:#00ffe0; border-radius:50%; box-shadow:0 0 8px #00ffe0; animation: pulse 1.5s infinite;"></span>
        <span style="font-family:'Orbitron',monospace; font-size:0.72rem; color:var(--accent); letter-spacing:2px;">DOSEDUCATION LIVE CHAT</span>
      </div>
      <span style="font-size:0.75rem; color:var(--muted);">powered by tlk.io</span>
    </div>
    <iframe src="https://tlk.io/doseducation?skin=dark" style="width:100%; height:500px; border:none; display:block;" allow="microphone"></iframe>
  </div>
</div>

<!-- Game iframe overlay -->
<div id="game-overlay" style="display:none; position:fixed; inset:0; z-index:9998; background:rgba(0,0,0,0.97); flex-direction:column;">
  <div style="display:flex; align-items:center; justify-content:space-between; padding:10px 20px; background:#0a0a0f; border-bottom:1px solid #1e1e2e; flex-shrink:0;">
    <div style="display:flex; align-items:center; gap:12px;">
      <span id="game-overlay-emoji" style="font-size:1.4rem;"></span>
      <span id="game-overlay-title" style="font-family:'Orbitron',monospace; font-size:0.82rem; letter-spacing:2px; color:#00ffe0;"></span>
    </div>
    <div style="display:flex; gap:10px;">
      <button onclick="fullscreenGame()" style="background:transparent; border:1px solid #1e1e2e; border-radius:4px; padding:7px 14px; color:#555577; font-family:'Orbitron',monospace; font-size:0.7rem; letter-spacing:1px; cursor:pointer; transition:all 0.2s;" onmouseover="this.style.borderColor='#00ffe0';this.style.color='#00ffe0'" onmouseout="this.style.borderColor='#1e1e2e';this.style.color='#555577'">⛶ FULLSCREEN</button>
      <button onclick="closeGame()" style="background:transparent; border:1px solid #1e1e2e; border-radius:4px; padding:7px 14px; color:#555577; font-family:'Orbitron',monospace; font-size:0.7rem; letter-spacing:1px; cursor:pointer; transition:all 0.2s;" onmouseover="this.style.borderColor='#ff3e6c';this.style.color='#ff3e6c'" onmouseout="this.style.borderColor='#1e1e2e';this.style.color='#555577'">✕ CLOSE</button>
    </div>
  </div>
  <iframe id="game-frame" src="" style="flex:1; border:none; width:100%; background:#000;" allowfullscreen allow="fullscreen *"></iframe>
</div>

<script>




function stealthTab() {
  const w = window.open('about:blank', '_blank');
  const html = document.documentElement.outerHTML;
  w.document.open();
  w.document.write(html);
  w.document.close();
  // Change the new tab's title to look innocent
  w.document.title = 'Google Classroom';
  try {
    const link = w.document.createElement('link');
    link.rel = 'shortcut icon';
    link.href = 'https://ssl.gstatic.com/classroom/favicon.png';
    w.document.head.appendChild(link);
  } catch(e) {}
}

function goTo(id) {
  const el = document.getElementById(id);
  if (el) el.scrollIntoView({ behavior: 'smooth' });
}

const games = [
  // IO / MULTIPLAYER
  { name: "Slope", desc: "Roll a ball down an endless neon slope", emoji: "&#9917;", url: "https://slope-game.github.io", cat: "action", age: "all", hot: true },
  { name: "Smash Karts", desc: "Kart racing battle royale", emoji: "&#127950;", url: "https://smashkarts.io", cat: "racing", age: "all", hot: true },
  { name: "Krunker.io", desc: "Fast paced browser FPS", emoji: "&#128299;", url: "https://krunker.io", cat: "shooter", age: "13+", hot: true },
  { name: "Shell Shockers", desc: "Egg-based FPS shooter", emoji: "&#129370;", url: "https://shellshock.io", cat: "shooter", age: "13+", hot: true },
  { name: "1v1.lol", desc: "Build and battle like Fortnite", emoji: "&#127979;", url: "https://1v1.lol", cat: "shooter", age: "13+", hot: true },
  { name: "Paper.io 2", desc: "Claim territory in multiplayer", emoji: "&#128220;", url: "https://html5.gamedistribution.com/rvvASdzgitPlkHs9Kf5GHYtiWzivUQ/", cat: "action", age: "all", hot: true },
  { name: "Agar.io", desc: "Eat others to grow bigger", emoji: "&#128299;", url: "https://agar.io", cat: "action", age: "all", hot: true },
  { name: "Slither.io", desc: "Snake multiplayer with power-ups", emoji: "&#128013;", url: "https://slither.io", cat: "action", age: "all", hot: true },
  { name: "Diep.io", desc: "Tank shooter upgrade game", emoji: "&#128312;", url: "https://diep.io", cat: "shooter", age: "all", hot: true },
  { name: "Hole.io", desc: "Swallow the city as a black hole", emoji: "&#11035;", url: "https://hole-io.com", cat: "action", age: "all", hot: true },
  { name: "Voxiom.io", desc: "Minecraft meets Fortnite browser game", emoji: "&#9935;", url: "https://voxiom.io", cat: "action", age: "all", hot: true },
  { name: "Skribbl.io", desc: "Draw and guess multiplayer game", emoji: "&#127912;", url: "https://skribbl.io", cat: "puzzle", age: "all", hot: true },

  // PLATFORMERS
  { name: "Vex 7", desc: "Deadly obstacle course platformer", emoji: "&#128680;", url: "https://html5.gamedistribution.com/vex7/", cat: "action", age: "all", hot: true },
  { name: "Vex 6", desc: "Intense spike-filled level runner", emoji: "&#128314;", url: "https://html5.gamedistribution.com/vex6/", cat: "action", age: "all", hot: false },
  { name: "Vex 5", desc: "Brutal platformer obstacle gauntlet", emoji: "&#128128;", url: "https://html5.gamedistribution.com/vex5/", cat: "action", age: "all", hot: false },
  { name: "Stickman Hook", desc: "Swing stickman through levels", emoji: "&#128373;", url: "https://html5.gamedistribution.com/StickmanHook/", cat: "action", age: "all", hot: true },
  { name: "Stickman Boost 2", desc: "Insane stickman speed runner", emoji: "&#127939;", url: "https://html5.gamedistribution.com/StickmanBoost2/", cat: "action", age: "all", hot: false },
  { name: "Red Ball 4", desc: "Roll and jump through levels", emoji: "&#128308;", url: "https://html5.gamedistribution.com/RedBall4/", cat: "action", age: "all", hot: false },
  { name: "Short Life", desc: "Guide ragdoll through deadly traps", emoji: "&#128128;", url: "https://html5.gamedistribution.com/ShortLife/", cat: "gore", age: "13+", hot: true },
  { name: "Short Life 2", desc: "Even more brutal ragdoll traps", emoji: "&#129657;", url: "https://html5.gamedistribution.com/ShortLife2/", cat: "gore", age: "13+", hot: true },
  { name: "Moto X3M", desc: "Insane bike stunt obstacle course", emoji: "&#127949;", url: "https://html5.gamedistribution.com/MotoX3M/", cat: "racing", age: "all", hot: true },
  { name: "Moto X3M Spooky Land", desc: "Halloween themed bike stunts", emoji: "&#127875;", url: "https://html5.gamedistribution.com/MotoX3MSpookyLand/", cat: "racing", age: "all", hot: true },
  { name: "Moto X3M Pool Party", desc: "Summer water park bike stunts", emoji: "&#127946;", url: "https://html5.gamedistribution.com/MotoX3MPoolParty/", cat: "racing", age: "all", hot: false },
  { name: "Elastic Man", desc: "Stretch a face with your cursor", emoji: "&#129488;", url: "https://html5.gamedistribution.com/ElasticMan/", cat: "action", age: "all", hot: true },
  { name: "Subway Surfers", desc: "Run from the inspector on the rails", emoji: "&#128668;", url: "https://html5.gamedistribution.com/SubwaySurfers/", cat: "action", age: "all", hot: true },
  { name: "Temple Run 2", desc: "Endless jungle escape run", emoji: "&#127939;", url: "https://html5.gamedistribution.com/TempleRun2/", cat: "action", age: "all", hot: false },
  { name: "Snail Bob 2", desc: "Guide snail Bob through puzzles", emoji: "&#128012;", url: "https://html5.gamedistribution.com/SnailBob2/", cat: "puzzle", age: "all", hot: false },
  { name: "Adam and Eve 5", desc: "Cave man puzzle adventure", emoji: "&#129489;", url: "https://html5.gamedistribution.com/AdamAndEve5/", cat: "puzzle", age: "all", hot: false },

  // PUZZLE
  { name: "2048", desc: "Slide tiles to reach 2048", emoji: "&#127922;", url: "https://play2048.co", cat: "puzzle", age: "all", hot: true },
  { name: "Bloxorz", desc: "Roll the block to the hole", emoji: "&#129521;", url: "https://html5.gamedistribution.com/Bloxorz/", cat: "puzzle", age: "all", hot: false },
  { name: "Bubble Shooter", desc: "Pop color-matched bubble chains", emoji: "&#128308;", url: "https://html5.gamedistribution.com/BubbleShooter/", cat: "puzzle", age: "all", hot: false },
  { name: "Brain Test", desc: "Tricky riddle brain teaser puzzles", emoji: "&#129504;", url: "https://html5.gamedistribution.com/BrainTest/", cat: "puzzle", age: "all", hot: true },
  { name: "Cut the Rope", desc: "Feed candy to cute monster Om Nom", emoji: "&#129354;", url: "https://www.cuttherope.net", cat: "puzzle", age: "all", hot: false },
  { name: "Uno Online", desc: "Classic Uno card game multiplayer", emoji: "&#127183;", url: "https://html5.gamedistribution.com/UnoOnline/", cat: "puzzle", age: "all", hot: true },
  { name: "8 Ball Pool", desc: "Multiplayer pool against real players", emoji: "&#127921;", url: "https://html5.gamedistribution.com/8BallPool/", cat: "puzzle", age: "all", hot: true },
  { name: "Mahjong", desc: "Classic tile matching game", emoji: "&#127183;", url: "https://html5.gamedistribution.com/Mahjong/", cat: "puzzle", age: "all", hot: false },
  { name: "Jewel Burst", desc: "Match jewels and blast combos", emoji: "&#128142;", url: "https://html5.gamedistribution.com/JewelBurst/", cat: "puzzle", age: "all", hot: false },
  { name: "Zuma Deluxe", desc: "Classic ball-shooting marble game", emoji: "&#128992;", url: "https://html5.gamedistribution.com/ZumaDeluxe/", cat: "puzzle", age: "all", hot: true },
  { name: "Wheely 8", desc: "Help Wheely the car solve puzzles", emoji: "&#128664;", url: "https://html5.gamedistribution.com/Wheely8/", cat: "puzzle", age: "all", hot: false },
  { name: "IQ Ball", desc: "Stretch a tentacle to reach the star", emoji: "&#129433;", url: "https://html5.gamedistribution.com/IQBall/", cat: "puzzle", age: "all", hot: false },
  { name: "Bomb It 7", desc: "Bomberman style multiplayer mayhem", emoji: "&#128163;", url: "https://html5.gamedistribution.com/BombIt7/", cat: "action", age: "all", hot: true },
  { name: "Bomb It 6", desc: "Bomb arenas with power-ups", emoji: "&#128163;", url: "https://html5.gamedistribution.com/BombIt6/", cat: "action", age: "all", hot: false },

  // IDLE
  { name: "Cookie Clicker", desc: "The OG idle clicking game", emoji: "&#127850;", url: "https://orteil.dashnet.org/cookieclicker/", cat: "idle", age: "all", hot: true },
  { name: "Antimatter Dimensions", desc: "Insane prestige idle math game", emoji: "&#9881;", url: "https://antimatter-dimensions.net", cat: "idle", age: "all", hot: true },
  { name: "Idle Breakout", desc: "Break bricks with auto-upgrading balls", emoji: "&#127921;", url: "https://idle-breakout.com", cat: "idle", age: "all", hot: true },
  { name: "Tiny Fishing", desc: "Simple relaxing fishing clicker", emoji: "&#127907;", url: "https://html5.gamedistribution.com/TinyFishing/", cat: "idle", age: "all", hot: true },
  { name: "Adventure Capitalist", desc: "Build a business empire from scratch", emoji: "&#128176;", url: "https://html5.gamedistribution.com/AdventureCapitalist/", cat: "idle", age: "all", hot: true },
  { name: "Idle Ants", desc: "Grow an ant colony to destroy things", emoji: "&#128028;", url: "https://html5.gamedistribution.com/IdleAnts/", cat: "idle", age: "all", hot: true },
  { name: "Clicker Heroes", desc: "Click monsters and hire heroes", emoji: "&#9876;", url: "https://html5.gamedistribution.com/ClickerHeroes/", cat: "idle", age: "all", hot: true },

  // MINECRAFT
  { name: "Eaglercraft", desc: "Minecraft in the browser, no download", emoji: "&#9935;", url: "https://eaglercraft.com/mc/1.8.8/", cat: "action", age: "all", hot: true },

  // STICKMAN
  { name: "Stick War Legacy", desc: "Command stick figure armies", emoji: "&#128481;", url: "https://html5.gamedistribution.com/StickWarLegacy/", cat: "action", age: "13+", hot: true },
  { name: "Stick War 3", desc: "Huge stickman strategy war game", emoji: "&#9876;", url: "https://html5.gamedistribution.com/StickWar3/", cat: "action", age: "13+", hot: true },
  { name: "Stickman Fighter Epic Battle", desc: "Stickman fighting tournament", emoji: "&#129354;", url: "https://html5.gamedistribution.com/StickmanFighterEpicBattle/", cat: "action", age: "13+", hot: true },
  { name: "Stickman Supreme Duelist 2", desc: "Ultimate stickman dueling game", emoji: "&#127942;", url: "https://html5.gamedistribution.com/StickmanSupremeDuelist2/", cat: "action", age: "13+", hot: true },
  { name: "Stickman Warrior Epic Fight", desc: "Epic stickman 1v1 showdowns", emoji: "&#128165;", url: "https://html5.gamedistribution.com/StickmanWarriorEpicFight/", cat: "action", age: "13+", hot: false },
  { name: "Madness Project Nexus", desc: "Madness Combat arena mayhem", emoji: "&#129354;", url: "https://html5.gamedistribution.com/MadnessProjectNexus/", cat: "gore", age: "13+", hot: true },

  // ARCHERS
  { name: "Stickman Archer 2", desc: "Duel archers with perfect aim", emoji: "&#127993;", url: "https://html5.gamedistribution.com/StickmanArcher2/", cat: "action", age: "all", hot: true },
  { name: "Stickman Archer 3", desc: "Ultimate stickman archery battles", emoji: "&#127993;", url: "https://html5.gamedistribution.com/StickmanArcher3/", cat: "action", age: "all", hot: false },
  { name: "Arrow Fest", desc: "Multiply arrows and wipe out enemies", emoji: "&#127993;", url: "https://html5.gamedistribution.com/ArrowFest/", cat: "action", age: "all", hot: true },
  { name: "Bowmaster", desc: "Aim and fire arrows at enemy troops", emoji: "&#127993;", url: "https://html5.gamedistribution.com/Bowmaster/", cat: "action", age: "all", hot: true },
  { name: "Archery World Tour", desc: "Precision archery across the globe", emoji: "&#127760;", url: "https://html5.gamedistribution.com/ArcheryWorldTour/", cat: "action", age: "all", hot: false },

  // RAGDOLL
  { name: "Ragdoll Hit", desc: "Launch a ragdoll and watch it suffer", emoji: "&#128165;", url: "https://html5.gamedistribution.com/RagdollHit/", cat: "gore", age: "13+", hot: true },
  { name: "Ragdoll Archers", desc: "Shoot ragdolls with arrows", emoji: "&#127993;", url: "https://html5.gamedistribution.com/RagdollArchers/", cat: "gore", age: "13+", hot: true },
  { name: "Kick the Buddy", desc: "Beat up buddy with every weapon", emoji: "&#128297;", url: "https://html5.gamedistribution.com/KickTheBuddy/", cat: "gore", age: "13+", hot: true },
  { name: "Stickman Turbo Dismounting", desc: "Launch stickmen into crashes", emoji: "&#128165;", url: "https://html5.gamedistribution.com/StickmanTurboDismounting/", cat: "gore", age: "13+", hot: true },

  // GORE / ZOMBIE
  { name: "Earn to Die", desc: "Drive through zombie hordes", emoji: "&#128664;", url: "https://html5.gamedistribution.com/EarnToDie/", cat: "gore", age: "13+", hot: true },
  { name: "Infectonator", desc: "Infect cities and watch chaos spread", emoji: "&#129440;", url: "https://html5.gamedistribution.com/Infectonator/", cat: "gore", age: "13+", hot: true },
  { name: "Zombocalypse 2", desc: "Mow down endless zombie waves", emoji: "&#128641;", url: "https://html5.gamedistribution.com/Zombocalypse2/", cat: "gore", age: "13+", hot: true },
  { name: "Age of War 2", desc: "Evolving warfare with bloody combat", emoji: "&#9876;", url: "https://html5.gamedistribution.com/AgeOfWar2/", cat: "gore", age: "13+", hot: true },
  { name: "Warfare 1917", desc: "WW1 trench warfare", emoji: "&#129686;", url: "https://html5.gamedistribution.com/Warfare1917/", cat: "gore", age: "13+", hot: true },
  { name: "Warfare 1944", desc: "WW2 squad combat", emoji: "&#128116;", url: "https://html5.gamedistribution.com/Warfare1944/", cat: "gore", age: "13+", hot: true },
  { name: "Raze 3", desc: "Sci-fi arena shooter", emoji: "&#128126;", url: "https://html5.gamedistribution.com/Raze3/", cat: "gore", age: "13+", hot: true },
  { name: "Dead Frontier 2", desc: "Zombie survival horror shooter", emoji: "&#128128;", url: "https://html5.gamedistribution.com/DeadFrontier2/", cat: "gore", age: "13+", hot: true },
  { name: "GoreBox", desc: "Extreme physics sandbox carnage", emoji: "&#128169;", url: "https://html5.gamedistribution.com/GoreBox/", cat: "gore", age: "13+", hot: true },
  { name: "The Last Stand 2", desc: "Survive zombie sieges night by night", emoji: "&#128308;", url: "https://html5.gamedistribution.com/TheLastStand2/", cat: "gore", age: "13+", hot: true },

  // RACING
  { name: "Burnout Drift", desc: "Satisfying burnout drift sim", emoji: "&#128168;", url: "https://html5.gamedistribution.com/BurnoutDrift/", cat: "racing", age: "all", hot: true },
  { name: "Racing Limits", desc: "Fast lane endless highway racer", emoji: "&#128661;", url: "https://html5.gamedistribution.com/RacingLimits/", cat: "racing", age: "all", hot: true },
  { name: "Crash of Cars", desc: "Real-time multiplayer car battle", emoji: "&#128165;", url: "https://html5.gamedistribution.com/CrashOfCars/", cat: "racing", age: "all", hot: true },
  { name: "Moto Road Rash 3D", desc: "Highway motorcycle dodging", emoji: "&#127949;", url: "https://html5.gamedistribution.com/MotoRoadRash3D/", cat: "racing", age: "all", hot: false },
  { name: "Drive or Die", desc: "Post apocalypse survival racing", emoji: "&#128128;", url: "https://html5.gamedistribution.com/DriveOrDie/", cat: "racing", age: "13+", hot: true },
  { name: "Zombie Derby 2", desc: "Drive through zombie hordes, splatter everything", emoji: "&#128663;", url: "https://html5.gamedistribution.com/ZombieDerby2/", cat: "gore", age: "13+", hot: true },
  { name: "Monster Truck Nitro 2", desc: "Insane monster truck stunts", emoji: "&#128665;", url: "https://html5.gamedistribution.com/MonsterTruckNitro2/", cat: "racing", age: "all", hot: false },
  { name: "Trial Bike Epic Stunts", desc: "Extreme trial bike obstacle course", emoji: "&#129313;", url: "https://html5.gamedistribution.com/TrialBikeEpicstunts/", cat: "racing", age: "all", hot: false },

  // TOWER DEFENSE
  { name: "Bloons Tower Defense 6", desc: "Ultimate balloon popping defense", emoji: "&#127880;", url: "https://html5.gamedistribution.com/BloonsMonkeyCity/", cat: "puzzle", age: "all", hot: true },
  { name: "GemCraft", desc: "Deep tower defense gem crafting", emoji: "&#128142;", url: "https://html5.gamedistribution.com/GemCraft/", cat: "puzzle", age: "all", hot: true },

  // CLASSIC ARCADE
  { name: "Pacman", desc: "The original maze muncher", emoji: "&#128123;", url: "https://freepacman.org", cat: "puzzle", age: "all", hot: true },
  { name: "Tetris", desc: "Classic block stacking game", emoji: "&#128315;", url: "https://html5.gamedistribution.com/Tetris/", cat: "puzzle", age: "all", hot: true },

  // FNAF
  { name: "FNaF 1", desc: "Survive the night at Freddy's", emoji: "&#128125;", url: "https://html5.gamedistribution.com/FiveNightsAtFreddys/", cat: "gore", age: "13+", hot: true },
  { name: "FNaF 2", desc: "New animatronics, no doors, good luck", emoji: "&#128125;", url: "https://html5.gamedistribution.com/FiveNightsAtFreddys2/", cat: "gore", age: "13+", hot: true },
  { name: "One Night at Flumpty's", desc: "Creepy FNaF fan game with an egg", emoji: "&#129370;", url: "https://html5.gamedistribution.com/OneNightAtFlumptys/", cat: "gore", age: "13+", hot: true },

  // BENDY
  { name: "Bendy Ink Machine Run", desc: "Run from Bendy through the studio", emoji: "&#128299;", url: "https://html5.gamedistribution.com/BendyInkMachineRun/", cat: "action", age: "13+", hot: true },

  // NEIGHBOR
  { name: "Scary Neighbor 3D", desc: "Spy on and escape your scary neighbor", emoji: "&#128065;", url: "https://html5.gamedistribution.com/ScaryNeighbor3D/", cat: "action", age: "13+", hot: true },
  { name: "Neighbor Escape", desc: "Sneak past your creepy neighbor", emoji: "&#127968;", url: "https://html5.gamedistribution.com/NeighborEscape/", cat: "action", age: "13+", hot: false },

  // EPIC RPG / STRATEGY
  { name: "Epic Battle Fantasy 5", desc: "Deep JRPG browser adventure", emoji: "&#129409;", url: "https://html5.gamedistribution.com/EpicBattleFantasy5/", cat: "action", age: "13+", hot: true },
  { name: "Warlords Heroes", desc: "Medieval hack and slash", emoji: "&#129504;", url: "https://html5.gamedistribution.com/WarlordsHeroes/", cat: "action", age: "13+", hot: true },
  { name: "Sonny", desc: "Zombie RPG with deep strategy", emoji: "&#129503;", url: "https://html5.gamedistribution.com/Sonny/", cat: "action", age: "13+", hot: true },
  { name: "Age of War", desc: "Evolve armies through time", emoji: "&#128481;", url: "https://html5.gamedistribution.com/AgeOfWar/", cat: "action", age: "13+", hot: true },

  // SPORTS
  { name: "Basketball Stars", desc: "1v1 online basketball showdowns", emoji: "&#127936;", url: "https://html5.gamedistribution.com/BasketballStars/", cat: "action", age: "all", hot: true },
  { name: "Soccer Skills World Cup", desc: "Dribble and shoot your way to glory", emoji: "&#9917;", url: "https://html5.gamedistribution.com/SoccerSkillsWorldCup/", cat: "action", age: "all", hot: false },
  { name: "Head Soccer", desc: "Wacky one-on-one soccer duels", emoji: "&#9917;", url: "https://html5.gamedistribution.com/HeadSoccer/", cat: "action", age: "all", hot: false },
  { name: "Baseball Pro", desc: "Hit home runs in this baseball game", emoji: "&#9918;", url: "https://html5.gamedistribution.com/BaseballPro/", cat: "action", age: "all", hot: false },
];

let currentFilter = 'all';

function renderGames(list) {
  const grid = document.getElementById('gameGrid');
  grid.innerHTML = '';
  list.forEach(game => {
    const card = document.createElement('div');
    card.className = 'game-card';
    card.onclick = () => openGame(game.url, game.name, game.emoji);
    card.innerHTML = '<div class="game-thumb-placeholder">' + game.emoji + '</div>' +
      '<span class="game-tag ' + (game.age === '13+' ? 'tag-13' : game.hot ? 'tag-hot' : 'tag-all') + '">' + (game.age === '13+' ? '13+' : game.hot ? 'HOT' : 'FREE') + '</span>' +
      '<div class="game-info"><div class="game-name">' + game.name + '</div><div class="game-desc">' + game.desc + '</div></div>';
    grid.appendChild(card);
  });
}




function setFilter(cat, btn) {
  currentFilter = cat;
  document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  filterGames();
}

function openGame(url, name, emoji) {
  const overlay = document.getElementById('game-overlay');
  document.getElementById('game-frame').src = url;
  document.getElementById('game-overlay-title').textContent = name.toUpperCase();
  document.getElementById('game-overlay-emoji').innerHTML = emoji;
  overlay.style.display = 'flex';
  document.body.style.overflow = 'hidden';
}

function closeGame() {
  document.getElementById('game-frame').src = '';
  document.getElementById('game-overlay').style.display = 'none';
  document.body.style.overflow = '';
}

function fullscreenGame() {
  const frame = document.getElementById('game-frame');
  if (frame.requestFullscreen) frame.requestFullscreen();
  else if (frame.webkitRequestFullscreen) frame.webkitRequestFullscreen();
}

document.addEventListener('keydown', e => { if (e.key === 'Escape') closeGame(); });
renderGames(games);

// ===================== BINARY ERROR CURSOR =====================
(function() {
  const style = document.createElement('style');
  style.textContent = `
    * { cursor: none !important; }
    #err-cursor {
      position: fixed;
      pointer-events: none;
      z-index: 999999;
      top: 0; left: 0;
      transform: translate(-2px, -2px);
      user-select: none;
    }
    #err-arrow {
      position: absolute;
      top: 0; left: 0;
      animation: errShake 0.07s steps(1) infinite;
    }
    @keyframes errShake {
      0%   { transform: translate(0,0);    filter: drop-shadow(0 0 4px #ff0000); }
      25%  { transform: translate(-2px,1px); filter: drop-shadow(2px 0 0 #00ffff) drop-shadow(-2px 0 0 #ff00ff); }
      50%  { transform: translate(2px,-1px); filter: drop-shadow(0 0 6px #ff0000); }
      75%  { transform: translate(-1px,2px); filter: drop-shadow(2px 0 0 #ff00ff) drop-shadow(-2px 0 0 #00ffff); }
    }
    .bin-particle {
      position: fixed;
      pointer-events: none;
      z-index: 999998;
      font-family: 'Orbitron', monospace;
      font-size: 10px;
      color: #ff0000;
      opacity: 0;
      user-select: none;
      text-shadow: 0 0 4px #ff0000;
    }
  `;
  document.head.appendChild(style);

  const ARROW_SVG = `<svg width="28" height="35" viewBox="0 0 28 35" xmlns="http://www.w3.org/2000/svg">
    <!-- red glitch copies -->
    <polygon points="1,1 1,28 8,21 12,32 16,30 12,19 20,19" fill="#ff000066" transform="translate(3,0)"/>
    <polygon points="1,1 1,28 8,21 12,32 16,30 12,19 20,19" fill="#00ffff44" transform="translate(-3,0)"/>
    <!-- main black arrow white border -->
    <polygon points="1,1 1,28 8,21 12,32 16,30 12,19 20,19" fill="#0a0a0a" stroke="#ff0000" stroke-width="1.5" stroke-linejoin="round"/>
    <!-- ERROR text on arrow -->
    <text x="3" y="16" font-family="monospace" font-size="4" fill="#ff0000" font-weight="bold">ERR</text>
  </svg>`;

  const wrap = document.createElement('div');
  wrap.id = 'err-cursor';
  wrap.innerHTML = `<div id="err-arrow">${ARROW_SVG}</div>`;
  document.body.appendChild(wrap);

  // Binary particles
  const BITS = ['0','1','01','10','11','00','101','010','1010','0110'];
  const pool = [];

  class Bit {
    constructor() {
      this.el = document.createElement('div');
      this.el.className = 'bin-particle';
      document.body.appendChild(this.el);
      this.active = false;
    }
    spawn(x, y) {
      this.x = x; this.y = y;
      this.vx = (Math.random() - 0.5) * 3;
      this.vy = (Math.random() * -3) - 0.5;
      this.life = 1;
      this.decay = 0.03 + Math.random() * 0.04;
      this.el.textContent = BITS[Math.floor(Math.random() * BITS.length)];
      // randomly red or cyan
      const col = Math.random() > 0.5 ? '#ff0000' : '#00ffff';
      this.el.style.color = col;
      this.el.style.textShadow = `0 0 4px ${col}`;
      this.active = true;
    }
    update() {
      if (!this.active) return;
      this.life -= this.decay;
      if (this.life <= 0) { this.active = false; this.el.style.opacity = 0; return; }
      this.x += this.vx;
      this.y += this.vy;
      this.vy += 0.05;
      this.el.style.opacity = this.life;
      this.el.style.left = this.x + 'px';
      this.el.style.top  = this.y + 'px';
    }
  }

  for (let i = 0; i < 24; i++) pool.push(new Bit());

  let lastSpawn = 0;
  document.addEventListener('mousemove', e => {
    wrap.style.left = e.clientX + 'px';
    wrap.style.top  = e.clientY + 'px';
    const now = Date.now();
    if (now - lastSpawn > 50) {
      lastSpawn = now;
      const b = pool.find(b => !b.active);
      if (b) b.spawn(e.clientX + (Math.random()*16-8), e.clientY + (Math.random()*16-8));
    }
  });

  // click burst
  document.addEventListener('click', e => {
    for (let i = 0; i < 8; i++) {
      const b = pool.find(b => !b.active);
      if (b) b.spawn(e.clientX, e.clientY);
    }
  });

  function animate() {
    pool.forEach(b => b.update());
    requestAnimationFrame(animate);
  }
  animate();
})();
</script>
</body>
</html>
