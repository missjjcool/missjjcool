<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
  <meta name="theme-color" content="#0a0a0a">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-title" content="WHUDDUP">
  <title>WHUDDUP</title>
  <link rel="manifest" href="manifest.json">
  <link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Bebas+Neue&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg: #0a0a0a;
      --surface: #141414;
      --border: #2a2a2a;
      --accent: #ff3d00;
      --accent2: #ffd600;
      --text: #f0f0f0;
      --muted: #666;
      --open: #ff3d00;
      --progress: #ffd600;
      --done: #00e676;
      --blocked: #e040fb;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'Space Mono', monospace;
      min-height: 100vh;
      padding-bottom: 80px;
    }

    /* HEADER */
    header {
      background: var(--bg);
      border-bottom: 2px solid var(--accent);
      padding: 16px 20px 12px;
      position: sticky;
      top: 0;
      z-index: 100;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .logo {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 2.2rem;
      letter-spacing: 4px;
      color: var(--accent);
      line-height: 1;
    }

    .logo span { color: var(--accent2); }

    .header-stats {
      font-size: 0.65rem;
      color: var(--muted);
      text-align: right;
      line-height: 1.6;
    }

    /* TABS */
    .tabs {
      display: flex;
      border-bottom: 1px solid var(--border);
      background: var(--surface);
      overflow-x: auto;
      scrollbar-width: none;
    }
    .tabs::-webkit-scrollbar { display: none; }

    .tab {
      flex: 1;
      min-width: 80px;
      padding: 12px 8px;
      text-align: center;
      font-family: 'Space Mono', monospace;
      font-size: 0.6rem;
      font-weight: 700;
      letter-spacing: 1px;
      text-transform: uppercase;
      color: var(--muted);
      background: none;
      border: none;
      cursor: pointer;
      border-bottom: 3px solid transparent;
      transition: all 0.15s;
    }

    .tab.active {
      color: var(--accent2);
      border-bottom-color: var(--accent2);
    }

    /* SITREP */
    .sitrep {
      padding: 20px;
    }

    .sitrep-header {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.4rem;
      letter-spacing: 3px;
      color: var(--accent2);
      margin-bottom: 16px;
    }

    .sitrep-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
      margin-bottom: 16px;
    }

    .sitrep-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-left: 3px solid var(--accent);
      padding: 12px;
      border-radius: 2px;
    }

    .sitrep-card.yellow { border-left-color: var(--accent2); }
    .sitrep-card.green { border-left-color: var(--done); }
    .sitrep-card.purple { border-left-color: var(--blocked); }

    .sitrep-label {
      font-size: 0.55rem;
      letter-spacing: 2px;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 4px;
    }

    .sitrep-value {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.6rem;
      color: var(--text);
      line-height: 1;
    }

    .sitrep-sub {
      font-size: 0.6rem;
      color: var(--muted);
      margin-top: 2px;
    }

    /* DAILY CHECKLIST */
    .daily-section {
      padding: 20px;
    }

    .section-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 14px;
    }

    .section-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.4rem;
      letter-spacing: 3px;
      color: var(--accent2);
    }

    .section-count {
      font-size: 0.6rem;
      color: var(--muted);
    }

    .daily-item {
      display: flex;
      align-items: center;
      gap: 12px;
      padding: 12px 0;
      border-bottom: 1px solid var(--border);
      cursor: pointer;
    }

    .daily-item:last-child { border-bottom: none; }

    .check-box {
      width: 22px;
      height: 22px;
      border: 2px solid var(--border);
      border-radius: 2px;
      flex-shrink: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.15s;
    }

    .daily-item.done .check-box {
      background: var(--done);
      border-color: var(--done);
    }

    .check-mark {
      display: none;
      color: #000;
      font-size: 0.8rem;
      font-weight: 700;
    }

    .daily-item.done .check-mark { display: block; }

    .daily-item-text {
      font-size: 0.78rem;
      line-height: 1.3;
      flex: 1;
    }

    .daily-item.done .daily-item-text {
      color: var(--muted);
      text-decoration: line-through;
    }

    .reset-btn {
      background: none;
      border: 1px solid var(--border);
      color: var(--muted);
      font-family: 'Space Mono', monospace;
      font-size: 0.6rem;
      letter-spacing: 1px;
      padding: 4px 10px;
      cursor: pointer;
      border-radius: 2px;
    }
    .reset-btn:hover { border-color: var(--accent); color: var(--accent); }

    /* ISSUES */
    .issues-section {
      padding: 20px;
    }

    .issue-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 2px;
      padding: 14px;
      margin-bottom: 10px;
      cursor: pointer;
      transition: border-color 0.15s;
    }

    .issue-card:hover { border-color: var(--accent2); }

    .issue-top {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 8px;
      margin-bottom: 6px;
    }

    .issue-id {
      font-size: 0.55rem;
      color: var(--muted);
      white-space: nowrap;
      margin-top: 2px;
    }

    .issue-title {
      font-size: 0.82rem;
      font-weight: 700;
      line-height: 1.3;
      flex: 1;
    }

    .issue-status {
      font-size: 0.55rem;
      letter-spacing: 1px;
      text-transform: uppercase;
      padding: 3px 7px;
      border-radius: 2px;
      white-space: nowrap;
      font-weight: 700;
    }

    .status-OPEN { background: rgba(255,61,0,0.2); color: var(--open); border: 1px solid var(--open); }
    .status-IN_PROGRESS { background: rgba(255,214,0,0.15); color: var(--progress); border: 1px solid var(--progress); }
    .status-DONE { background: rgba(0,230,118,0.15); color: var(--done); border: 1px solid var(--done); }
    .status-BLOCKED { background: rgba(224,64,251,0.15); color: var(--blocked); border: 1px solid var(--blocked); }

    .issue-meta {
      display: flex;
      gap: 10px;
      align-items: center;
    }

    .issue-priority {
      font-size: 0.6rem;
      color: var(--muted);
    }

    .priority-HIGH { color: var(--open); }
    .priority-MED { color: var(--progress); }
    .priority-LOW { color: var(--muted); }

    .issue-tag {
      font-size: 0.55rem;
      background: var(--border);
      padding: 2px 6px;
      border-radius: 2px;
      color: var(--muted);
    }

    .issue-desc {
      font-size: 0.7rem;
      color: var(--muted);
      margin-top: 6px;
      line-height: 1.5;
    }

    /* ADD BUTTON */
    .fab {
      position: fixed;
      bottom: 24px;
      right: 20px;
      width: 56px;
      height: 56px;
      background: var(--accent);
      border: none;
      border-radius: 50%;
      font-size: 1.6rem;
      color: white;
      cursor: pointer;
      box-shadow: 0 4px 20px rgba(255,61,0,0.4);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 200;
      transition: transform 0.15s, box-shadow 0.15s;
    }
    .fab:hover { transform: scale(1.08); box-shadow: 0 6px 28px rgba(255,61,0,0.6); }

    /* MODAL */
    .modal-overlay {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.85);
      z-index: 300;
      align-items: flex-end;
    }
    .modal-overlay.open { display: flex; }

    .modal {
      background: var(--surface);
      border-top: 2px solid var(--accent);
      width: 100%;
      max-height: 90vh;
      overflow-y: auto;
      padding: 24px 20px 40px;
      border-radius: 8px 8px 0 0;
    }

    .modal-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.6rem;
      letter-spacing: 3px;
      color: var(--accent);
      margin-bottom: 20px;
    }

    .form-group { margin-bottom: 16px; }

    .form-label {
      display: block;
      font-size: 0.6rem;
      letter-spacing: 2px;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 6px;
    }

    .form-input, .form-select, .form-textarea {
      width: 100%;
      background: var(--bg);
      border: 1px solid var(--border);
      color: var(--text);
      font-family: 'Space Mono', monospace;
      font-size: 0.8rem;
      padding: 10px 12px;
      border-radius: 2px;
      outline: none;
    }
    .form-input:focus, .form-select:focus, .form-textarea:focus {
      border-color: var(--accent2);
    }
    .form-textarea { min-height: 80px; resize: vertical; }
    .form-select option { background: var(--surface); }

    .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }

    .btn-row { display: flex; gap: 10px; margin-top: 20px; }

    .btn {
      flex: 1;
      padding: 12px;
      font-family: 'Space Mono', monospace;
      font-size: 0.75rem;
      font-weight: 700;
      letter-spacing: 2px;
      text-transform: uppercase;
      border: none;
      border-radius: 2px;
      cursor: pointer;
    }

    .btn-primary { background: var(--accent); color: white; }
    .btn-secondary { background: var(--border); color: var(--muted); }

    /* FILTER BAR */
    .filter-bar {
      display: flex;
      gap: 8px;
      padding: 12px 20px;
      overflow-x: auto;
      scrollbar-width: none;
      border-bottom: 1px solid var(--border);
    }
    .filter-bar::-webkit-scrollbar { display: none; }

    .filter-chip {
      flex-shrink: 0;
      padding: 5px 12px;
      border: 1px solid var(--border);
      border-radius: 20px;
      font-family: 'Space Mono', monospace;
      font-size: 0.6rem;
      letter-spacing: 1px;
      color: var(--muted);
      background: none;
      cursor: pointer;
    }
    .filter-chip.active { border-color: var(--accent2); color: var(--accent2); }

    .empty-state {
      text-align: center;
      padding: 60px 20px;
      color: var(--muted);
      font-size: 0.75rem;
      line-height: 2;
    }

    .empty-state .big { font-family: 'Bebas Neue'; font-size: 3rem; color: var(--border); letter-spacing: 4px; }

    /* PANEL CONTENT */
    .panel { display: none; }
    .panel.active { display: block; }
  </style>
</head>
<body>

<header>
  <div class="logo">WHUD<span>DUP</span></div>
  <div class="header-stats" id="headerStats">
    Loading...
  </div>
</header>

<div class="tabs">
  <button class="tab active" onclick="switchTab('sitrep')">SITREP</button>
  <button class="tab" onclick="switchTab('daily')">DAILY</button>
  <button class="tab" onclick="switchTab('issues')">ISSUES</button>
  <button class="tab" onclick="switchTab('projects')">PROJECTS</button>
</div>

<!-- SITREP TAB -->
<div class="panel active" id="panel-sitrep">
  <div class="sitrep">
    <div class="sitrep-header">// SITREP</div>
    <div class="sitrep-grid" id="sitrep-grid">
      <!-- Populated by JS -->
    </div>
    <div id="sitrep-recent"></div>
  </div>
</div>

<!-- DAILY TAB -->
<div class="panel" id="panel-daily">
  <div class="daily-section">
    <div class="section-header">
      <div class="section-title">// DAILY OPS</div>
      <button class="reset-btn" onclick="resetDaily()">RESET</button>
    </div>
    <div id="daily-list"></div>
  </div>
</div>

<!-- ISSUES TAB -->
<div class="panel" id="panel-issues">
  <div class="filter-bar" id="filter-bar">
    <button class="filter-chip active" onclick="setFilter('ALL')">ALL</button>
    <button class="filter-chip" onclick="setFilter('OPEN')">OPEN</button>
    <button class="filter-chip" onclick="setFilter('IN_PROGRESS')">IN PROGRESS</button>
    <button class="filter-chip" onclick="setFilter('BLOCKED')">BLOCKED</button>
    <button class="filter-chip" onclick="setFilter('DONE')">DONE</button>
  </div>
  <div class="issues-section" id="issues-list"></div>
</div>

<!-- PROJECTS TAB -->
<div class="panel" id="panel-projects">
  <div class="issues-section" id="projects-list"></div>
</div>

<!-- FAB -->
<button class="fab" onclick="openModal()" id="fab">+</button>

<!-- ADD ISSUE MODAL -->
<div class="modal-overlay" id="modal">
  <div class="modal">
    <div class="modal-title" id="modal-title">// NEW ISSUE</div>
    <div class="form-group">
      <label class="form-label">Title *</label>
      <input class="form-input" id="f-title" placeholder="What needs doing?" />
    </div>
    <div class="form-group">
      <label class="form-label">Description</label>
      <textarea class="form-textarea" id="f-desc" placeholder="Details..."></textarea>
    </div>
    <div class="form-row">
      <div class="form-group">
        <label class="form-label">Type</label>
        <select class="form-select" id="f-type">
          <option value="ISSUE">Issue</option>
          <option value="PROJECT">Project</option>
          <option value="LEARNING">Learning</option>
        </select>
      </div>
      <div class="form-group">
        <label class="form-label">Status</label>
        <select class="form-select" id="f-status">
          <option value="OPEN">Open</option>
          <option value="IN_PROGRESS">In Progress</option>
          <option value="BLOCKED">Blocked</option>
          <option value="DONE">Done</option>
        </select>
      </div>
    </div>
    <div class="form-row">
      <div class="form-group">
        <label class="form-label">Priority</label>
        <select class="form-select" id="f-priority">
          <option value="HIGH">High</option>
          <option value="MED">Med</option>
          <option value="LOW">Low</option>
        </select>
      </div>
      <div class="form-group">
        <label class="form-label">Tag</label>
        <input class="form-input" id="f-tag" placeholder="e.g. personal" />
      </div>
    </div>
    <div class="btn-row">
      <button class="btn btn-secondary" onclick="closeModal()">CANCEL</button>
      <button class="btn btn-primary" onclick="saveIssue()">SAVE ISSUE</button>
    </div>
  </div>
</div>

<script>
// ============ DATA ============
const DAILY_DEFAULTS = [
  "Shower",
  "Sweep",
  "Sex work",
  "Security",
  "Meds",
  "Messages",
  "Money",
  "Mindset",
  "Web",
  "Weather",
  "Water",
  "Workout",
];

function loadData() {
  return {
    issues: JSON.parse(localStorage.getItem('ww_issues') || '[]'),
    daily: JSON.parse(localStorage.getItem('ww_daily') || 'null'),
    dailyDate: localStorage.getItem('ww_daily_date') || '',
  };
}

function saveIssues(issues) {
  localStorage.setItem('ww_issues', JSON.stringify(issues));
}

function getDailyState() {
  const today = new Date().toDateString();
  const saved = localStorage.getItem('ww_daily_date');
  if (saved !== today) {
    // New day — reset
    const fresh = DAILY_DEFAULTS.map((t, i) => ({ id: i, text: t, done: false }));
    localStorage.setItem('ww_daily', JSON.stringify(fresh));
    localStorage.setItem('ww_daily_date', today);
    return fresh;
  }
  return JSON.parse(localStorage.getItem('ww_daily') || '[]');
}

function saveDailyState(items) {
  localStorage.setItem('ww_daily', JSON.stringify(items));
  localStorage.setItem('ww_daily_date', new Date().toDateString());
}

// ============ TABS ============
let currentTab = 'sitrep';
let currentFilter = 'ALL';
let editingId = null;

function switchTab(tab) {
  currentTab = tab;
  document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.panel').forEach(p => p.classList.remove('active'));
  event.target.classList.add('active');
  document.getElementById('panel-' + tab).classList.add('active');

  // Show/hide FAB
  document.getElementById('fab').style.display = (tab === 'issues' || tab === 'projects') ? 'flex' : 'none';

  render();
}

// ============ RENDER ============
function render() {
  renderHeader();
  if (currentTab === 'sitrep') renderSitrep();
  if (currentTab === 'daily') renderDaily();
  if (currentTab === 'issues') renderIssues();
  if (currentTab === 'projects') renderProjects();
}

function renderHeader() {
  const { issues } = loadData();
  const open = issues.filter(i => i.status === 'OPEN' && i.type !== 'PROJECT').length;
  const inprog = issues.filter(i => i.status === 'IN_PROGRESS').length;
  const blocked = issues.filter(i => i.status === 'BLOCKED').length;
  document.getElementById('headerStats').innerHTML =
    `<span style="color:var(--open)">${open} open</span> · <span style="color:var(--progress)">${inprog} active</span> · <span style="color:var(--blocked)">${blocked} blocked</span><br>${new Date().toLocaleDateString('en-CA', {weekday:'short', month:'short', day:'numeric'})}`;
}

function renderSitrep() {
  const { issues } = loadData();
  const daily = getDailyState();
  const doneCnt = daily.filter(d => d.done).length;
  const open = issues.filter(i => i.status === 'OPEN').length;
  const blocked = issues.filter(i => i.status === 'BLOCKED').length;
  const projects = issues.filter(i => i.type === 'PROJECT' && i.status !== 'DONE').length;
  const learning = issues.filter(i => i.type === 'LEARNING' && i.status !== 'DONE').length;

  document.getElementById('sitrep-grid').innerHTML = `
    <div class="sitrep-card">
      <div class="sitrep-label">Daily Ops</div>
      <div class="sitrep-value">${doneCnt}/${daily.length}</div>
      <div class="sitrep-sub">tasks done today</div>
    </div>
    <div class="sitrep-card yellow">
      <div class="sitrep-label">Open Issues</div>
      <div class="sitrep-value">${open}</div>
      <div class="sitrep-sub">need attention</div>
    </div>
    <div class="sitrep-card purple">
      <div class="sitrep-label">Blocked</div>
      <div class="sitrep-value">${blocked}</div>
      <div class="sitrep-sub">waiting on something</div>
    </div>
    <div class="sitrep-card green">
      <div class="sitrep-label">Projects</div>
      <div class="sitrep-value">${projects}</div>
      <div class="sitrep-sub">${learning} learning tracks</div>
    </div>
  `;

  // Recent issues
  const recent = issues.filter(i => i.status !== 'DONE').slice(-5).reverse();
  if (recent.length) {
    document.getElementById('sitrep-recent').innerHTML = `
      <div class="sitrep-header" style="margin-top:20px">// ACTIVE</div>
      ${recent.map(i => `
        <div class="issue-card" onclick="editIssue(${i.id})">
          <div class="issue-top">
            <div class="issue-title">${i.title}</div>
            <span class="issue-status status-${i.status}">${i.status.replace('_',' ')}</span>
          </div>
          <div class="issue-meta">
            <span class="issue-priority priority-${i.priority}">▲ ${i.priority}</span>
            ${i.tag ? `<span class="issue-tag">${i.tag}</span>` : ''}
          </div>
        </div>
      `).join('')}
    `;
  } else {
    document.getElementById('sitrep-recent').innerHTML = '';
  }
}

function renderDaily() {
  const items = getDailyState();
  const done = items.filter(d => d.done).length;
  const countEl = document.querySelector('.section-count');
  if (countEl) countEl.textContent = `${done}/${items.length} done`;
  document.getElementById('daily-list').innerHTML = items.map(item => `
    <div class="daily-item ${item.done ? 'done' : ''}" onclick="toggleDaily(${item.id})">
      <div class="check-box"><span class="check-mark">✓</span></div>
      <div class="daily-item-text">${item.text}</div>
    </div>
    
