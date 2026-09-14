# sarver
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gemini Pro // Cadet Tactical AI Assistant</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<style>
  :root {
    --bg-main: #F4F6F9;
    --sidebar-bg: #0F172A;
    --sidebar-hover: #1E293B;
    --card-surface: #FFFFFF;
    --border-line: #CBD5E1;
    --text-dark: #0F172A;
    --text-dim: #475569;
    --tactical-blue: #0284C7;
    --officer-gold: #B45309;
    --online-green: #15803D;
    --alert-red: #DC2626;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', system-ui, -apple-system, sans-serif; }
  body { background: var(--bg-main); color: var(--text-dark); display: flex; height: 100vh; overflow: hidden; font-size: 16px; line-height: 1.5; }

  /* SIDEBAR NAVIGATION */
  aside {
    width: 310px;
    background: var(--sidebar-bg);
    color: #F8FAFC;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    border-right: 1px solid #334155;
    flex-shrink: 0;
    transition: transform 0.3s ease;
    z-index: 1000;
  }
  @media(max-width: 900px) {
    aside { position: absolute; height: 100%; transform: translateX(-100%); }
    aside.open { transform: translateX(0); }
  }

  .sidebar-top { padding: 18px 16px; overflow-y: auto; }
  .brand-row { display: flex; justify-content: space-between; align-items: center; margin-bottom: 24px; padding: 0 8px; }
  .brand-name { font-size: 22px; font-weight: 700; color: #FFFFFF; letter-spacing: 0.5px; }

  .nav-btn {
    display: flex; align-items: center; gap: 14px; width: 100%;
    background: transparent; border: none; color: #E2E8F0;
    padding: 12px 14px; border-radius: 8px; font-size: 15px;
    font-weight: 600; cursor: pointer; text-align: left; transition: 0.2s;
    margin-bottom: 4px;
  }
  .nav-btn:hover { background: var(--sidebar-hover); color: #FFFFFF; }
  .nav-btn i { font-size: 18px; width: 22px; color: #94A3B8; }
  .badge-beta { font-size: 10px; background: #334155; color: #38BDF8; padding: 2px 6px; border-radius: 4px; font-weight: 800; margin-left: auto; }

  .side-section-title { font-size: 12px; color: #94A3B8; font-weight: 700; text-transform: uppercase; margin: 18px 8px 8px; letter-spacing: 0.5px; }
  
  .recent-item {
    padding: 10px 14px; border-radius: 8px; font-size: 14px; color: #CBD5E1;
    cursor: pointer; display: flex; align-items: center; gap: 10px; margin-bottom: 2px;
    white-space: nowrap; overflow: hidden; text-overflow: ellipsis;
  }
  .recent-item:hover, .recent-item.active { background: var(--sidebar-hover); color: #38BDF8; font-weight: 600; }

  /* SIDEBAR FOOTER */
  .sidebar-footer {
    border-top: 1px solid #1E293B;
    padding: 14px 16px;
    display: flex; justify-content: space-between; align-items: center;
    background: #090E17;
  }
  .user-profile { display: flex; align-items: center; gap: 12px; }
  .avatar {
    width: 40px; height: 40px; border-radius: 50%;
    background: linear-gradient(135deg, #0284C7, #B45309);
    display: flex; align-items: center; justify-content: center;
    color: #fff; font-weight: bold; font-size: 16px;
    border: 2px solid #38BDF8;
  }
  .user-meta .name { font-size: 14px; font-weight: 700; color: #FFFFFF; }
  .user-meta .sub { font-size: 11px; color: #38BDF8; font-weight: 600; }

  /* MAIN CONTENT CANVAS */
  main { flex: 1; display: flex; flex-direction: column; background: var(--bg-main); height: 100vh; overflow-y: auto; }

  /* TOP HEADER STRIP */
  .chat-header {
    background: var(--card-surface);
    border-bottom: 2px solid var(--border-line);
    padding: 14px 20px;
    display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 10px;
  }
  .toggle-btn { display: none; background: transparent; border: none; font-size: 20px; color: var(--text-dark); cursor: pointer; }
  @media(max-width: 900px) { .toggle-btn { display: block; } }

  .header-info h2 { font-size: 18px; color: var(--text-dark); font-weight: 800; }
  .header-info p { font-size: 13px; color: var(--text-dim); font-weight: 600; }
  .day-pill {
    background: #E0F2FE; border: 2px solid var(--tactical-blue); color: var(--tactical-blue);
    padding: 6px 14px; border-radius: 6px; font-size: 14px; font-weight: 800; display: flex; align-items: center; gap: 8px;
  }

  /* COUNTDOWN ROW */
  .metrics-grid {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 14px; padding: 16px 20px 0;
  }
  .metric-card {
    background: var(--card-surface); border: 2px solid var(--border-line); border-radius: 8px; padding: 14px; text-align: center;
  }
  .metric-card h4 { font-size: 12px; color: var(--text-dim); text-transform: uppercase; font-weight: 700; }
  .metric-val { font-size: 26px; font-weight: 800; color: var(--tactical-blue); margin: 4px 0; }
  .metric-val.gold { color: var(--officer-gold); }
  .metric-val.green { color: var(--online-green); }

  /* DUAL RECON SEARCH CONSOLE */
  .search-console {
    background: var(--card-surface); border: 2px solid var(--border-line); border-left: 5px solid var(--tactical-blue);
    border-radius: 8px; padding: 14px 18px; margin: 16px 20px 0;
  }
  .search-row { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 10px; }
  .search-row input {
    flex: 1; min-width: 240px; background: #F8FAFC; border: 2px solid var(--border-line);
    padding: 10px 14px; border-radius: 6px; color: var(--text-dark); font-size: 14px; font-weight: 600; outline: none;
  }
  .search-row input:focus { border-color: var(--tactical-blue); }
  .filter-chips { display: flex; gap: 6px; flex-wrap: wrap; align-items: center; }
  .chip {
    font-size: 12px; padding: 5px 12px; border-radius: 4px; border: 1.5px solid var(--border-line);
    color: var(--text-dim); background: #F1F5F9; cursor: pointer; font-weight: 600; transition: 0.2s;
  }
  .chip.active, .chip:hover { border-color: var(--tactical-blue); color: var(--tactical-blue); background: #E0F2FE; }

  /* DASHBOARD TWO-COLUMN LAYOUT */
  .main-workspace {
    display: grid; grid-template-columns: 2fr 1fr; gap: 16px; padding: 16px 20px 24px;
  }
  @media(max-width: 1024px) { .main-workspace { grid-template-columns: 1fr; } }

  .card {
    background: var(--card-surface); border: 2px solid var(--border-line); border-radius: 8px; padding: 18px; margin-bottom: 16px;
  }
  .card-head {
    display: flex; justify-content: space-between; align-items: center;
    border-bottom: 2px solid var(--border-line); padding-bottom: 10px; margin-bottom: 14px;
  }
  .card-head h3 { font-size: 15px; color: var(--text-dark); text-transform: uppercase; font-weight: 800; letter-spacing: 0.5px; display: flex; align-items: center; gap: 8px; }

  /* BUTTONS */
  .btn {
    background: var(--tactical-blue); color: #fff; border: none; padding: 9px 15px;
    font-size: 12px; font-weight: 700; border-radius: 6px; cursor: pointer;
    display: inline-flex; align-items: center; gap: 6px; text-transform: uppercase; transition: 0.2s;
  }
  .btn:hover { opacity: 0.9; }
  .btn.gold { background: var(--officer-gold); }
  .btn.outline { background: transparent; border: 2px solid var(--border-line); color: var(--text-dim); }
  .btn.outline:hover { border-color: var(--tactical-blue); color: var(--tactical-blue); }

  /* TASK LIST */
  .task-list { display: flex; flex-direction: column; gap: 10px; }
  .task-row {
    background: #F8FAFC; border: 1.5px solid var(--border-line); padding: 12px 14px;
    border-radius: 6px; display: flex; justify-content: space-between; align-items: center; font-size: 14px; font-weight: 600;
  }
  .task-left { display: flex; align-items: center; gap: 12px; }
  .task-left input { accent-color: var(--tactical-blue); transform: scale(1.3); cursor: pointer; }
  .tag { font-size: 11px; padding: 3px 6px; border-radius: 4px; font-weight: 800; }
  .tag.blue { background: #E0F2FE; color: var(--tactical-blue); }
  .tag.green { background: #DCFCE7; color: var(--online-green); }
  .tag.gold { background: #FEF3C7; color: var(--officer-gold); }

  /* NEWS FEED */
  .news-stream {
    background: #F8FAFC; border: 1.5px solid var(--border-line); border-radius: 6px;
    padding: 12px; max-height: 320px; overflow-y: auto; display: flex; flex-direction: column; gap: 12px;
  }
  .news-card {
    background: #FFFFFF; border: 1px solid var(--border-line); border-left: 4px solid var(--tactical-blue);
    border-radius: 6px; padding: 10px 12px; font-size: 13px;
  }
  .news-title { color: var(--text-dark); font-weight: 800; font-size: 14px; margin-bottom: 4px; }
  .news-meta { font-size: 11px; color: var(--text-dim); margin-bottom: 6px; font-weight: 600; }
  .news-analysis {
    background: #F1F5F9; border-radius: 4px; padding: 6px 8px; margin-top: 6px; font-size: 12px; font-weight: 600;
  }

  /* CHAT STREAM */
  .chat-stream {
    background: #F8FAFC; border: 1.5px solid var(--border-line); border-radius: 6px;
    padding: 14px; height: 300px; overflow-y: auto; font-size: 14px; display: flex; flex-direction: column; gap: 10px;
  }
  .msg-row { display: flex; gap: 10px; align-items: flex-start; }
  .msg-row.user { justify-content: flex-end; }
  .msg-avatar {
    width: 32px; height: 32px; border-radius: 50%; display: flex; align-items: center; justify-content: center;
    flex-shrink: 0; font-size: 13px; font-weight: bold;
  }
  .msg-avatar.ai { background: var(--tactical-blue); color: #fff; }
  .msg-avatar.user { background: var(--officer-gold); color: #fff; }
  .bubble {
    background: #FFFFFF; border: 1.5px solid var(--border-line); padding: 12px 14px;
    border-radius: 8px; max-width: 85%; line-height: 1.5;
  }
  .bubble.user { background: #0F172A; color: #FFFFFF; border-color: #0F172A; }
  .protocol-box {
    background: #F8FAFC; border-left: 4px solid var(--tactical-blue); padding: 8px 10px;
    margin-top: 8px; border-radius: 4px; font-size: 12.5px; border: 1px solid var(--border-line); border-left-width: 4px;
  }
  .protocol-row { margin-bottom: 4px; }
  .protocol-tag { font-weight: 800; color: var(--officer-gold); text-transform: uppercase; font-size: 11px; }

  .chat-input-bar { display: flex; gap: 8px; margin-top: 10px; }
  .chat-input-bar input {
    flex: 1; background: #FFFFFF; border: 2px solid var(--border-line); padding: 10px 14px;
    border-radius: 6px; color: var(--text-dark); font-size: 14px; outline: none;
  }
  .chat-input-bar input:focus { border-color: var(--tactical-blue); }

  /* SETTINGS MODAL */
  .api-modal {
    display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%;
    background: rgba(0,0,0,0.5); z-index: 2000; align-items: center; justify-content: center;
  }
  .modal-card {
    background: #FFFFFF; border-radius: 8px; padding: 22px; max-width: 480px; width: 90%;
    border: 2px solid var(--border-line); box-shadow: 0 8px 24px rgba(0,0,0,0.15);
  }
</style>
</head>
<body>

<!-- SIDEBAR -->
<aside id="sidebar">
  <div class="sidebar-top">
    <div class="brand-row">
      <div class="brand-name"><i class="fa-solid fa-sparkles" style="color:#38BDF8;"></i> Gemini</div>
      <i class="fa-solid fa-xmark" style="font-size:20px; cursor:pointer;" onclick="toggleSidebar()"></i>
    </div>

    <button class="nav-btn" onclick="startNewChat()"><i class="fa-solid fa-pen-to-square"></i> New chat</button>
    <button class="nav-btn" onclick="searchChats()"><i class="fa-solid fa-magnifying-glass"></i> Search chats</button>
    <button class="nav-btn"><i class="fa-solid fa-wand-magic-sparkles"></i> Spark <span class="badge-beta">BETA</span></button>
    <button class="nav-btn"><i class="fa-solid fa-graduation-cap"></i> Students</button>
    <button class="nav-btn"><i class="fa-solid fa-image"></i> Images</button>
    <button class="nav-btn"><i class="fa-solid fa-video"></i> Videos</button>
    <button class="nav-btn"><i class="fa-solid fa-layer-group"></i> Library</button>

    <div class="side-section-title">Notebooks</div>
    <button class="nav-btn" onclick="createNotebook()"><i class="fa-solid fa-plus"></i> New notebook</button>

    <div class="side-section-title">Recent</div>
    <div class="recent-item active" onclick="loadChat('hq')">
      <i class="fa-regular fa-message"></i> Cadet Command HQ Tactical Suite
    </div>
    <div class="recent-item" onclick="loadChat('cds')">
      <i class="fa-regular fa-message"></i> CDS Study Planner Evaluation
    </div>
    <div class="recent-item" onclick="loadChat('jarvis')">
      <i class="fa-regular fa-message"></i> JARVIS Pro Defence Tactical OS
    </div>
  </div>

  <div class="sidebar-footer">
    <div class="user-profile">
      <div class="avatar">S</div>
      <div class="user-meta">
        <div class="name">Saravanan .v</div>
        <div class="sub">PRO DEFENCE ASPIRANT</div>
      </div>
    </div>
    <button class="btn outline" style="padding:6px 10px; border-color:#334155; color:#94A3B8;" onclick="openSettings()"><i class="fa-solid fa-gear"></i></button>
  </div>
</aside>

<!-- MAIN CONTENT CANVAS -->
<main>
  <div class="chat-header">
    <div style="display:flex; align-items:center; gap:12px;">
      <button class="toggle-btn" onclick="toggleSidebar()"><i class="fa-solid fa-bars"></i></button>
      <div class="header-info">
        <h2>Cadet Tactical Command // Intelligence Engine</h2>
        <p>Target: CDS 1 2027 (11 April 2027) | Work Shift: 09:00 - 18:00 Accommodated</p>
      </div>
    </div>
    <div class="day-pill">
      <i class="fa-solid fa-calendar-day"></i> <span id="currentDayText">DAY 1 OF 84</span>
    </div>
  </div>

  <!-- COUNTDOWN DECK -->
  <div class="metrics-grid">
    <div class="metric-card">
      <h4>CDS 1 2027 TARGET</h4>
      <div class="metric-val gold" id="cdsTimer">--d</div>
      <p style="font-size: 11px; color: var(--text-dim); font-weight:600;">UPSC Exam: 11 April 2027</p>
    </div>
    <div class="metric-card">
      <h4>AFCAT 1 2027 TARGET</h4>
      <div class="metric-val" id="afcatTimer">--d</div>
      <p style="font-size: 11px; color: var(--text-dim); font-weight:600;">IAF Cycle: February 2027</p>
    </div>
    <div class="metric-card">
      <h4>DEFENCE MASS TARGET</h4>
      <div class="metric-val green">49.0 / 58 KG</div>
      <p style="font-size: 11px; color: var(--online-green); font-weight:600;">+9 kg Calorie Retention Plan</p>
    </div>
    <div class="metric-card">
      <h4>TODAY'S MISSION PROGRESS</h4>
      <div class="metric-val" id="dailyPct">0%</div>
      <p style="font-size: 11px; color: var(--text-dim); font-weight:600;" id="taskStat">0 / 6 Milestones Cleared</p>
    </div>
  </div>

  <!-- DUAL RECON SEARCH RADAR -->
  <div class="search-console">
    <div class="search-row">
      <input type="text" id="omniQueryInput" placeholder="Tactical Search: Type formula, grammar rule, or defence event (e.g., 'Divisibility Rules', 'BrahMos PIB', 'S1-S6 Tricks')..." onkeydown="if(event.key==='Enter') executeReconSearch()">
      <button class="btn" onclick="executeReconSearch()"><i class="fa-solid fa-magnifying-glass"></i> Recon Launch</button>
    </div>
    <div class="filter-chips">
      <span style="font-size:11px; color:var(--officer-gold); font-weight:bold;"><i class="fa-solid fa-crosshairs"></i> Target Engine:</span>
      <span class="chip active" data-engine="local" onclick="switchEngine(this)"><i class="fa-solid fa-list-check"></i> In-App Syllabus</span>
      <span class="chip" data-engine="google" onclick="switchEngine(this)"><i class="fa-brands fa-google"></i> Google</span>
      <span class="chip" data-engine="upsc" onclick="switchEngine(this)"><i class="fa-solid fa-landmark"></i> UPSC Portal</span>
      <span class="chip" data-engine="pib" onclick="switchEngine(this)"><i class="fa-solid fa-newspaper"></i> PIB Defence</span>
      <span class="chip" data-engine="youtube" onclick="switchEngine(this)"><i class="fa-brands fa-youtube"></i> Video Lectures</span>
      <span class="chip" data-engine="scholar" onclick="switchEngine(this)"><i class="fa-solid fa-graduation-cap"></i> Scholar</span>
    </div>
  </div>

  <!-- MAIN WORKSPACE -->
  <div class="main-workspace">
    <!-- LEFT COLUMN -->
    <div>
      <!-- ACTIVE MISSION PLANNER -->
      <div class="card">
        <div class="card-head">
          <h3><i class="fa-solid fa-list-check" style="color:var(--tactical-blue);"></i> Active Mission Planner (<span id="dayHeaderLabel">Day 1</span>)</h3>
          <div style="display:flex; gap:6px;">
            <button class="btn outline" onclick="changeDay(-1)"><i class="fa-solid fa-chevron-left"></i> Prev</button>
            <select id="daySelector" onchange="jumpToDay(this.value)" style="border:2px solid var(--border-line); border-radius:6px; padding:6px 10px; font-size:13px; font-weight:700;"></select>
            <button class="btn outline" onclick="changeDay(1)">Next <i class="fa-solid fa-chevron-right"></i></button>
          </div>
        </div>
        <div style="font-size: 13px; color: var(--text-dim); margin-bottom: 12px; font-weight: 600;">
          <i class="fa-solid fa-arrows-rotate"></i> Auto-Resets at 00:00 Midnight. Routine tailored around your 09:00 - 18:00 work schedule.
        </div>
        <div class="task-list" id="taskList"></div>
      </div>

      <!-- J.A.R.V.I.S. / GEMINI CHAT INTERACTION -->
      <div class="card">
        <div class="card-head">
          <h3><i class="fa-solid fa-robot" style="color:var(--officer-gold);"></i> J.A.R.V.I.S. Cognitive Assistant</h3>
          <span style="font-size:12px; color:var(--online-green); font-weight:700;"><i class="fa-solid fa-circle"></i> ONLINE</span>
        </div>
        <div class="chat-stream" id="chatStream"></div>
        <div class="chat-input-bar">
          <input type="text" id="cadetInput" placeholder="Ask questions, request grammar drills, or practice SSB topics..." onkeydown="if(event.key==='Enter') sendCadetChat()">
          <button class="btn" onclick="sendCadetChat()"><i class="fa-solid fa-paper-plane"></i> Send</button>
          <button class="btn gold" onclick="triggerVoice()"><i class="fa-solid fa-microphone"></i> Voice</button>
        </div>
      </div>
    </div>

    <!-- RIGHT COLUMN -->
    <div>
      <!-- LIVE DEFENCE NEWS FEED -->
      <div class="card">
        <div class="card-head">
          <h3><i class="fa-solid fa-newspaper" style="color:var(--tactical-blue);"></i> Live Defence & PIB Intel</h3>
          <button class="btn outline" style="padding:4px 8px; font-size:11px;" onclick="loadLiveDefenceNews()"><i class="fa-solid fa-rotate"></i> Refresh</button>
        </div>
        <div class="news-stream" id="newsFeed">
          <div style="text-align:center; color:var(--text-dim); padding:20px;">
            <i class="fa-solid fa-spinner fa-spin"></i> Connecting to live defence news wire...
          </div>
        </div>
      </div>

      <!-- ACCURACY RADAR -->
      <div class="card">
        <div class="card-head">
          <h3><i class="fa-solid fa-chart-pie" style="color:var(--officer-gold);"></i> Competency Radar</h3>
        </div>
        <canvas id="cadetRadar" style="max-height: 200px;"></canvas>
      </div>
    </div>
  </div>
</main>

<!-- API SETTINGS MODAL -->
<div class="api-modal" id="settingsModal">
  <div class="modal-card">
    <h3 style="margin-bottom:12px; font-size:17px; color:var(--text-dark);"><i class="fa-solid fa-gear"></i> AI Provider & Model Settings</h3>
    <p style="font-size:13px; color:var(--text-dim); margin-bottom:14px;">
      Select your preferred AI backend. Use <strong>Built-in Cognitive Engine</strong> for immediate offline replies, or provide a Hugging Face / OpenAI API token.
    </p>

    <label style="font-size:12px; font-weight:700; display:block; margin-bottom:4px;">MODEL GATEWAY</label>
    <select id="providerChoice" style="width:100%; padding:9px; border:2px solid var(--border
