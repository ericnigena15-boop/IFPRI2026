<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>IFPRI Rwanda — Youth Survey Portal</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=IBM+Plex+Mono:wght@400;500&family=DM+Sans:wght@300;400;500&family=Raleway:wght@400;600;700;800;900&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#0a0e14;--surface:#111820;--surface2:#1a2330;--border:#1e2d3d;
  --accent:#00d4a8;--accent2:#ff6b6b;--accent3:#ffd166;--accent4:#74b9ff;
  --text:#e8edf2;--muted:#5a7a8a;
  --my:#74b9ff;--fy:#fd79a8;--mo:#00d4a8;--fo:#ffd166;
}
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;overflow-x:hidden;font-size:14px}

/* ── LOGIN ── */
#loginWrap{position:fixed;inset:0;background:var(--bg);display:flex;align-items:center;justify-content:center;z-index:999}
.lcard{background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:2rem;width:380px}
.llogo{font-family:'Syne',sans-serif;font-weight:800;font-size:12px;letter-spacing:3px;color:var(--accent);text-transform:uppercase;margin-bottom:6px}
.ltitle{font-family:'Syne',sans-serif;font-size:17px;font-weight:700;margin-bottom:3px}
.lsub{font-size:12px;color:var(--muted);margin-bottom:1.5rem}
.lfield{margin-bottom:12px}
.lfield label{display:block;font-family:'IBM Plex Mono',monospace;font-size:10px;letter-spacing:1.5px;color:var(--muted);text-transform:uppercase;margin-bottom:5px}
.lfield input{width:100%;background:var(--bg);border:1px solid var(--border);color:var(--text);padding:9px 12px;border-radius:5px;font-family:'DM Sans',sans-serif;font-size:13px;outline:none;transition:border-color .15s}
.lfield input:focus{border-color:var(--accent)}
.lbtn{width:100%;background:var(--accent);color:#0a0e14;border:none;padding:11px;border-radius:5px;font-family:'Syne',sans-serif;font-weight:700;font-size:12px;letter-spacing:1.5px;text-transform:uppercase;cursor:pointer;transition:opacity .15s;margin-top:4px}
.lbtn:hover{opacity:.88}
.lerr{font-size:12px;color:var(--accent2);margin-top:8px;display:none}


/* ── HEADER ── */
.hdr{background:var(--surface);border-bottom:1px solid var(--border);padding:0 24px;display:flex;align-items:center;height:52px;gap:16px;position:sticky;top:0;z-index:100}
.hdr-logo{font-family:'Syne',sans-serif;font-weight:800;font-size:11px;letter-spacing:3px;color:var(--accent);text-transform:uppercase}
.hdr-sep{width:1px;height:24px;background:var(--border)}
.hdr-title{font-family:'Syne',sans-serif;font-size:14px;font-weight:600}
.hdr-r{margin-left:auto;display:flex;align-items:center;gap:12px}
.role-pill{font-family:'IBM Plex Mono',monospace;font-size:10px;padding:3px 10px;border-radius:3px;letter-spacing:1px}
.rp-admin{background:rgba(0,212,168,.12);color:var(--accent);border:1px solid rgba(0,212,168,.2)}
.rp-sup{background:rgba(116,185,255,.12);color:var(--accent4);border:1px solid rgba(116,185,255,.2)}
.hdr-date{font-family:'IBM Plex Mono',monospace;font-size:11px;color:var(--muted)}
.logout-btn{font-family:'IBM Plex Mono',monospace;font-size:10px;background:transparent;border:1px solid var(--border);color:var(--muted);padding:4px 10px;border-radius:3px;cursor:pointer;letter-spacing:1px;text-transform:uppercase;transition:all .15s}
.logout-btn:hover{border-color:var(--muted);color:var(--text)}

/* ── TABS ── */
.tabs{background:var(--surface);border-bottom:1px solid var(--border);padding:0 24px;display:flex;overflow-x:auto}
.tab{padding:12px 16px;font-family:'Syne',sans-serif;font-size:12px;font-weight:600;letter-spacing:.5px;cursor:pointer;border-bottom:2px solid transparent;color:var(--muted);white-space:nowrap;display:flex;align-items:center;gap:7px;user-select:none;transition:color .15s}
.tab:hover{color:var(--text)}
.tab.on{color:var(--accent);border-bottom-color:var(--accent)}
.tab.on-b{color:var(--accent4);border-bottom-color:var(--accent4)}
.tab.on-y{color:var(--accent3);border-bottom-color:var(--accent3)}
.tab.on-r{color:var(--accent2);border-bottom-color:var(--accent2)}
.tpill{font-family:'IBM Plex Mono',monospace;font-size:10px;padding:1px 7px;border-radius:3px;background:var(--surface2)}
.tab.on .tpill{background:rgba(0,212,168,.15);color:var(--accent)}
.tab.on-b .tpill{background:rgba(116,185,255,.15);color:var(--accent4)}
.tab.on-y .tpill{background:rgba(255,209,102,.15);color:var(--accent3)}
.tab.on-r .tpill{background:rgba(255,107,107,.15);color:var(--accent2)}

/* ── CONTENT ── */
.content{padding:22px 24px;max-width:1700px}
.panel{display:none}.panel.on{display:block}

/* ── STAT CARDS ── */
.stat-grid{display:grid;grid-template-columns:repeat(6,1fr);gap:12px;margin-bottom:20px}
.sc{background:var(--surface);border:1px solid var(--border);border-radius:8px;padding:18px 20px 16px;position:relative;overflow:hidden}

.sc-icon{position:absolute;top:14px;right:14px;font-size:22px;opacity:0.18}
.sc-icon-sm{font-size:13px;margin-right:5px;vertical-align:middle}
.sc::before{content:'';position:absolute;top:0;left:0;right:0;height:2px}
.sc-g::before{background:var(--accent)}
.sc-b::before{background:var(--accent4)}
.sc-y::before{background:var(--accent3)}
.sc-r::before{background:var(--accent2)}
.sc-p::before{background:var(--fy)}
.sc-t::before{background:var(--mo)}
.sc-lbl{font-family:'IBM Plex Mono',monospace;font-size:9px;letter-spacing:1.5px;color:var(--muted);text-transform:uppercase;margin-bottom:10px}
.sc-val{font-family:'Raleway',sans-serif;font-size:38px;font-weight:900;line-height:1;letter-spacing:-1px}
.sc-sub{font-size:11px;color:var(--muted);margin-top:6px}
.sc-bar{height:3px;background:var(--border);border-radius:2px;margin-top:10px;overflow:hidden}
.sc-fill{height:100%;border-radius:2px;transition:width .5s ease}

/* ── STRATA CARDS ── */
.strata-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:20px}
.strc{background:var(--surface);border:1px solid var(--border);border-radius:8px;padding:15px 16px}
.strc-hd{display:flex;align-items:center;gap:8px;margin-bottom:10px}
.strc-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.strc-name{font-family:'Syne',sans-serif;font-size:12px;font-weight:600}
.strc-cnt{margin-left:auto;font-family:'IBM Plex Mono',monospace;font-size:10px;color:var(--muted)}
.strc-bar{height:5px;background:var(--border);border-radius:3px;overflow:hidden;margin-bottom:5px}
.strc-fill{height:100%;border-radius:3px;transition:width .6s ease}
.strc-nums{display:flex;justify-content:space-between;font-family:'IBM Plex Mono',monospace;font-size:10px;color:var(--muted)}

/* ── PANEL / TABLE ── */
.pnl{background:var(--surface);border:1px solid var(--border);border-radius:8px;overflow:hidden}
.pnl-hd{padding:13px 18px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between}
.pnl-title{font-family:'Syne',sans-serif;font-size:13px;font-weight:700}
.pnl-badge{font-family:'IBM Plex Mono',monospace;font-size:10px;color:var(--accent);background:rgba(0,212,168,.1);padding:3px 8px;border-radius:3px}
.pnl-badge-b{color:var(--accent4);background:rgba(116,185,255,.1)}
.pnl-badge-y{color:var(--accent3);background:rgba(255,209,102,.1)}
.pnl-badge-r{color:var(--accent2);background:rgba(255,107,107,.1)}

.two-col{display:grid;grid-template-columns:320px 1fr;gap:16px;margin-bottom:20px}
.three-col{display:grid;grid-template-columns:1fr 1fr 1fr;gap:16px;margin-bottom:20px}
.mb20{margin-bottom:20px}

/* District list */
.dist-list{padding:6px 0;max-height:440px;overflow-y:auto}
.dist-list::-webkit-scrollbar{width:4px}
.dist-list::-webkit-scrollbar-track{background:var(--bg)}
.dist-list::-webkit-scrollbar-thumb{background:var(--border);border-radius:2px}
.dist-item{padding:10px 18px;cursor:pointer;border-left:3px solid transparent;transition:all .15s}
.dist-item:hover{background:rgba(255,255,255,.02)}
.dist-item.act{background:rgba(0,212,168,.05);border-left-color:var(--accent)}
.dist-name{font-family:'Syne',sans-serif;font-size:12px;font-weight:600;margin-bottom:4px}
.dist-pr-row{display:flex;align-items:center;gap:8px}
.dist-bar{flex:1;height:3px;background:var(--border);border-radius:2px;overflow:hidden}
.dist-fill{height:100%;background:var(--accent);border-radius:2px;transition:width .5s ease}
.dist-pct{font-family:'IBM Plex Mono',monospace;font-size:10px;color:var(--muted);width:30px;text-align:right}
.dist-prov{font-size:10px;color:var(--muted);margin-bottom:2px}

/* Village table */
.vtw{overflow-y:auto;max-height:500px}
.vtw::-webkit-scrollbar{width:4px}
.vtw::-webkit-scrollbar-track{background:var(--bg)}
.vtw::-webkit-scrollbar-thumb{background:var(--border);border-radius:2px}
table{width:100%;border-collapse:collapse;font-size:12px}
thead tr{background:var(--surface2);position:sticky;top:0;z-index:10}
thead th{padding:9px 11px;text-align:left;font-family:'IBM Plex Mono',monospace;font-size:9px;letter-spacing:1px;color:var(--muted);text-transform:uppercase;white-space:nowrap;border-bottom:1px solid var(--border)}
tbody tr{border-bottom:1px solid rgba(30,45,61,.5);transition:background .1s}
tbody tr:hover{background:rgba(255,255,255,.02)}
tbody td{padding:9px 11px;white-space:nowrap;vertical-align:middle}
.td-r{text-align:right;font-family:'IBM Plex Mono',monospace}
.td-m{color:var(--muted);font-size:11px}
.sts{font-family:'IBM Plex Mono',monospace;font-size:9px;padding:2px 7px;border-radius:3px;display:inline-block}
.s-done{background:rgba(0,212,168,.15);color:var(--accent)}
.s-prog{background:rgba(255,209,102,.15);color:var(--accent3)}
.s-pend{background:rgba(90,122,138,.15);color:var(--muted)}
.s-comp{background:rgba(0,212,168,.15);color:var(--accent)}
.s-inc{background:rgba(255,209,102,.15);color:var(--accent3)}
.s-rep{background:rgba(255,107,107,.15);color:var(--accent2)}

/* ── MINI BAR CHART ── */
.bar-chart{display:flex;align-items:flex-end;gap:5px;height:90px;padding:0 18px 0}
.bar-col{flex:1;display:flex;flex-direction:column;align-items:center;gap:3px}
.bar-val{font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--text)}
.bar-stack{width:100%;display:flex;flex-direction:column-reverse;gap:1px}
.bar-seg{width:100%;border-radius:2px;min-height:2px}
.bar-lbl{font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--muted);text-align:center}

/* ── DONUT ── */
.donut-wrap{display:flex;align-items:center;gap:20px;padding:18px}
.leg-item{display:flex;align-items:center;gap:8px;padding:5px 0}
.leg-dot{width:7px;height:7px;border-radius:50%;flex-shrink:0}
.leg-lbl{font-size:12px;flex:1}
.leg-val{font-family:'IBM Plex Mono',monospace;font-size:12px;color:var(--muted)}

/* ── LOG ── */
.log-list{max-height:200px;overflow-y:auto;padding:6px 0}
.log-list::-webkit-scrollbar{width:4px}
.log-list::-webkit-scrollbar-track{background:var(--bg)}
.log-list::-webkit-scrollbar-thumb{background:var(--border);border-radius:2px}
.log-item{padding:8px 18px;display:flex;gap:10px;align-items:flex-start;border-bottom:1px solid rgba(30,45,61,.4)}
.log-dot{width:5px;height:5px;border-radius:50%;margin-top:5px;flex-shrink:0}
.log-time{font-family:'IBM Plex Mono',monospace;font-size:10px;color:var(--muted);flex-shrink:0;padding-top:1px}
.log-txt{font-size:12px;line-height:1.5}

/* ── FORM ── */
.form-pad{padding:16px 18px}
.form-label{font-family:'IBM Plex Mono',monospace;font-size:9px;letter-spacing:1.5px;color:var(--muted);text-transform:uppercase;margin-bottom:4px;display:block}
.form-row{display:flex;gap:8px;margin-bottom:10px;flex-wrap:wrap}
.form-grp{flex:1;min-width:90px}
select,input[type=number],input[type=date],input[type=text]{
  width:100%;background:var(--bg);border:1px solid var(--border);color:var(--text);
  padding:7px 10px;border-radius:4px;font-family:'DM Sans',sans-serif;font-size:12px;outline:none;transition:border-color .15s
}
select:focus,input:focus{border-color:var(--accent)}
select option{background:var(--surface)}
.sep-lbl{font-family:'IBM Plex Mono',monospace;font-size:9px;letter-spacing:1.5px;color:var(--muted);text-transform:uppercase;margin:14px 0 8px;padding-bottom:6px;border-bottom:1px solid var(--border)}
.fg{display:grid;gap:10px;margin-bottom:10px}
.fg2{grid-template-columns:1fr 1fr}
.fg3{grid-template-columns:1fr 1fr 1fr}
.fg4{grid-template-columns:1fr 1fr 1fr 1fr}
.ff{display:flex;flex-direction:column;gap:4px}
.ff label{font-family:'IBM Plex Mono',monospace;font-size:9px;letter-spacing:1.5px;color:var(--muted);text-transform:uppercase}
.ff input,.ff select,.ff textarea{background:var(--bg);border:1px solid var(--border);color:var(--text);padding:7px 10px;border-radius:4px;font-family:'DM Sans',sans-serif;font-size:12px;outline:none;transition:border-color .15s;width:100%}
.ff textarea{padding:8px 10px;resize:vertical;height:60px}
.ff input:focus,.ff select:focus,.ff textarea:focus{border-color:var(--accent)}
.ff input:disabled,.ff select:disabled{opacity:.4;cursor:not-allowed}
.submit-btn{width:100%;background:var(--accent);color:#0a0e14;border:none;padding:10px;border-radius:4px;font-family:'Syne',sans-serif;font-weight:700;font-size:11px;letter-spacing:1.5px;text-transform:uppercase;cursor:pointer;transition:opacity .15s;margin-top:8px}
.submit-btn:hover{opacity:.88}
.f-ok{font-size:11px;color:var(--accent);text-align:center;margin-top:6px;display:none}
.f-err{font-size:11px;color:var(--accent2);text-align:center;margin-top:6px;display:none}
.dist-prog-row{margin-bottom:8px}
.dist-prog-hd{display:flex;justify-content:space-between;font-size:11px;margin-bottom:3px}
.dist-prog-name{font-family:'Syne',sans-serif;font-size:11px;font-weight:600}
.dist-prog-nums{font-family:'IBM Plex Mono',monospace;font-size:10px;color:var(--muted)}
.dp-bar{height:4px;background:var(--border);border-radius:2px;overflow:hidden}
.dp-fill{height:100%;border-radius:2px;transition:width .5s ease}
.empty-msg{padding:20px 18px;font-size:12px;color:var(--muted)}
@keyframes fadeIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:translateY(0)}}
.content>*{animation:fadeIn .35s ease both}
@media(max-width:1200px){
  .stat-grid{grid-template-columns:repeat(3,1fr)}
  .two-col{grid-template-columns:1fr}
  .three-col{grid-template-columns:1fr 1fr}
}
@media(max-width:768px){
  .stat-grid{grid-template-columns:repeat(2,1fr)}
  .strata-grid{grid-template-columns:repeat(2,1fr)}
  .three-col{grid-template-columns:1fr}
}
</style>
</head>
<body>

<!-- LOGIN -->
<div id="loginWrap">
  <div class="lcard">
    <div class="llogo">IFPRI Rwanda</div>
    <div class="ltitle">Youth Survey Portal</div>
    <div class="lsub">Sign in with your role credentials to continue</div>
    <div class="lfield"><label>Username</label><input id="lu" type="text" placeholder="Enter username" autocomplete="off" /></div>
    <div class="lfield"><label>Password</label><input id="lp" type="password" placeholder="Enter password" /></div>
    <div class="lerr" id="lerr">Incorrect username or password.</div>
    <button class="lbtn" onclick="doLogin()">Sign in</button>

  </div>
</div>

<!-- APP -->
<div id="appWrap" style="display:none">

<div class="hdr">
  <div class="hdr-logo">IFPRI RW</div>
  <div class="hdr-sep"></div>
  <div class="hdr-title" id="hdrTitle">Youth Survey — Field Progress Dashboard</div>
  <div class="hdr-r">
    <div class="hdr-date" id="hdrDate"></div>
    <button onclick="document.getElementById('setupModal').style.display='flex'" style="height:28px;padding:0 12px;background:rgba(255,209,102,.08);border:1px solid rgba(255,209,102,.2);color:var(--accent3);border-radius:3px;font-family:'IBM Plex Mono',monospace;font-size:10px;cursor:pointer;letter-spacing:.5px">⚙ SETUP</button>
    <button id="refreshBtn" onclick="loadRecordsFromSheet()" style="display:none;height:28px;padding:0 12px;background:rgba(0,212,168,.1);border:1px solid rgba(0,212,168,.2);color:var(--accent);border-radius:3px;font-family:'IBM Plex Mono',monospace;font-size:10px;cursor:pointer;letter-spacing:.5px">⟳ REFRESH</button>
    <div class="role-pill" id="rolePill">ADMIN</div>
    <button class="logout-btn" onclick="doLogout()">Sign out</button>
  </div>
</div>

<div class="tabs" id="adminTabs" style="display:none">
  <div class="tab on" data-panel="overview" onclick="swTab(this)">Overview</div>
  <div class="tab" data-panel="villages" onclick="swTab(this)">Villages</div>
  <div class="tab on-b" data-panel="completed" onclick="swTab(this)">Completed <span class="tpill" id="tp-c">0</span></div>
  <div class="tab on-y" data-panel="incomplete" onclick="swTab(this)">Incomplete <span class="tpill" id="tp-i">0</span></div>
  <div class="tab on-r" data-panel="replacement" onclick="swTab(this)">Replacements <span class="tpill" id="tp-r">0</span></div>
  <div class="tab" data-panel="entry" onclick="swTab(this)">Log data</div>
  <div class="tab" data-panel="share" onclick="swTab(this)">Share</div>
</div>

<div class="tabs" id="supTabs" style="display:none">
  <div class="tab on" data-panel="entry" onclick="swTab(this)">Enter daily data</div>
  <div class="tab" data-panel="mylog" onclick="swTab(this)">My submissions <span class="tpill" id="tp-my">0</span></div>
</div>

<div class="content">

<!-- ═══ OVERVIEW ═══ -->
<div class="panel on" id="p-overview">
  <div class="stat-grid">
    <div class="sc sc-g">
      <div class="sc-icon">👥</div>
      <div class="sc-lbl">Total respondents</div>
      <div class="sc-val" id="s-tot" style="color:var(--accent)">0</div>
      <div class="sc-sub" id="s-tot-sub">of 3,200 target</div>
      <div class="sc-bar"><div class="sc-fill" id="sp-tot" style="background:var(--accent);width:0%"></div></div>
    </div>
    <div class="sc sc-b">
      <div class="sc-icon">📍</div>
      <div class="sc-lbl">Villages active</div>
      <div class="sc-val" id="s-act" style="color:var(--accent4)">0</div>
      <div class="sc-sub">of 160 villages</div>
      <div class="sc-bar"><div class="sc-fill" id="sp-act" style="background:var(--accent4);width:0%"></div></div>
    </div>
    <div class="sc sc-y">
      <div class="sc-icon">✅</div>
      <div class="sc-lbl">Villages completed</div>
      <div class="sc-val" id="s-don" style="color:var(--accent3)">0</div>
      <div class="sc-sub">20 respondents reached</div>
      <div class="sc-bar"><div class="sc-fill" id="sp-don" style="background:var(--accent3);width:0%"></div></div>
    </div>
    <div class="sc sc-r">
      <div class="sc-icon">⏸</div>
      <div class="sc-lbl">Incomplete surveys</div>
      <div class="sc-val" id="s-inc" style="color:var(--accent2)">0</div>
      <div class="sc-sub" id="s-inc-sub">logged submissions</div>
      <div class="sc-bar"><div class="sc-fill" id="sp-inc" style="background:var(--accent2);width:0%"></div></div>
    </div>
    <div class="sc sc-p">
      <div class="sc-icon">🔄</div>
      <div class="sc-lbl">Replacements done</div>
      <div class="sc-val" id="s-rep" style="color:var(--fy)">0</div>
      <div class="sc-sub" id="s-rep-sub">replacement surveys</div>
      <div class="sc-bar"><div class="sc-fill" id="sp-rep" style="background:var(--fy);width:0%"></div></div>
    </div>
    <div class="sc sc-t">
      <div class="sc-icon">📊</div>
      <div class="sc-lbl">Overall progress</div>
      <div class="sc-val" id="s-pct" style="color:var(--mo)">0%</div>
      <div class="sc-sub" id="s-rem">3,200 remaining</div>
      <div class="sc-bar"><div class="sc-fill" id="sp-pct" style="background:var(--mo);width:0%"></div></div>
    </div>
  </div>

  <div class="strata-grid">
    <div class="strc">
      <div class="strc-hd"><div class="strc-dot" style="background:var(--my)"></div><div class="strc-name">Male 15–24</div><div class="strc-cnt" id="st1-c">0/800</div></div>
      <div class="strc-bar"><div class="strc-fill" id="st1-b" style="background:var(--my);width:0%"></div></div>
      <div class="strc-nums"><span>0%</span><span id="st1-p">0%</span></div>
    </div>
    <div class="strc">
      <div class="strc-hd"><div class="strc-dot" style="background:var(--fy)"></div><div class="strc-name">Female 15–24</div><div class="strc-cnt" id="st2-c">0/800</div></div>
      <div class="strc-bar"><div class="strc-fill" id="st2-b" style="background:var(--fy);width:0%"></div></div>
      <div class="strc-nums"><span>0%</span><span id="st2-p">0%</span></div>
    </div>
    <div class="strc">
      <div class="strc-hd"><div class="strc-dot" style="background:var(--mo)"></div><div class="strc-name">Male 25–35</div><div class="strc-cnt" id="st3-c">0/800</div></div>
      <div class="strc-bar"><div class="strc-fill" id="st3-b" style="background:var(--mo);width:0%"></div></div>
      <div class="strc-nums"><span>0%</span><span id="st3-p">0%</span></div>
    </div>
    <div class="strc">
      <div class="strc-hd"><div class="strc-dot" style="background:var(--fo)"></div><div class="strc-name">Female 25–35</div><div class="strc-cnt" id="st4-c">0/800</div></div>
      <div class="strc-bar"><div class="strc-fill" id="st4-b" style="background:var(--fo);width:0%"></div></div>
      <div class="strc-nums"><span>0%</span><span id="st4-p">0%</span></div>
    </div>
  </div>

  <div class="two-col mb20">
    <div class="pnl">
      <div class="pnl-hd"><span class="pnl-title">Districts</span><span class="pnl-badge">27 districts · 160 villages</span></div>
      <div class="dist-list" id="distList"></div>
    </div>
    <div class="pnl">
      <div class="pnl-hd"><span class="pnl-title" id="vt-title">All Submissions</span><span class="pnl-badge" id="vt-badge">—</span></div>
      <div class="vtw">
        <table>
          <thead><tr><th>Date</th><th>Supervisor</th><th>Province</th><th>District</th><th>Sector</th><th>Village</th><th>Status</th><th>M15-24</th><th>F15-24</th><th>M25-35</th><th>F25-35</th><th>Total</th><th>vs Target</th></tr></thead>
          <tbody id="mainTbl"><tr><td colspan="13" style="padding:20px;color:var(--muted);font-size:12px">No submissions yet.</td></tr></tbody>
        </table>
      </div>
    </div>
  </div>

  <div class="three-col">
    <div class="pnl">
      <div class="pnl-hd"><span class="pnl-title">📅 Daily submissions (last 7 days)</span></div>
      <div style="padding:14px 0 4px"><div class="bar-chart" id="dailyChart"><div style="color:var(--muted);font-size:12px;align-self:center;padding:20px">No data yet</div></div></div>
      <div class="pnl-hd" style="border-top:1px solid var(--border);margin-top:8px"><span class="pnl-title">📊 District progress vs target</span></div>
      <div style="padding:12px 16px;max-height:240px;overflow-y:auto" id="distProg"></div>
    </div>
    <div class="pnl">
      <div class="pnl-hd"><span class="pnl-title">🌍 Province breakdown</span></div>
      <div style="padding:12px 16px" id="provProg"></div>
      <div class="pnl-hd" style="border-top:1px solid var(--border)"><span class="pnl-title">👥 Sex distribution</span></div>
      <div style="padding:12px 16px" id="sexChart"></div>
    </div>
    <div class="pnl">
      <div class="pnl-hd">
        <span class="pnl-title" id="vil-prog-title">🏘 Village progress — select district</span>
        <span class="pnl-badge" id="vil-prog-badge">—</span>
      </div>
      <div style="padding:10px 14px 6px;border-bottom:1px solid var(--border)">
        <select id="vil-dist-sel" onchange="onVilDistSel()" style="width:100%;background:var(--bg);border:1px solid var(--border);color:var(--text);padding:7px 10px;border-radius:4px;font-family:'DM Sans',sans-serif;font-size:12px;outline:none">
          <option value="">Choose a district to see village progress…</option>
        </select>
      </div>
      <div id="vil-prog-list" style="max-height:320px;overflow-y:auto;padding:8px 0">
        <div class="empty-msg">Select a district above.</div>
      </div>
    </div>
  </div>

  <div class="pnl mb20">
    <div class="pnl-hd"><span class="pnl-title">📋 Activity log</span></div>
    <div class="log-list" id="activityLog"><div class="empty-msg">No activity logged yet.</div></div>
  </div>
</div>

<!-- ═══ VILLAGES ═══ -->
<div class="panel" id="p-villages">
  <div class="pnl mb20">
    <div class="pnl-hd">
      <span class="pnl-title">&#127757; Village-level progress</span>
      <span class="pnl-badge" id="vill-badge">160 villages &middot; 3,200 target</span>
    </div>
    <div style="display:flex;gap:10px;padding:12px 16px;border-bottom:1px solid var(--border);align-items:flex-end;flex-wrap:wrap">
      <div style="display:flex;flex-direction:column;gap:4px;flex:1;min-width:150px">
        <label style="font-family:&#39;IBM Plex Mono&#39;,monospace;font-size:9px;letter-spacing:1.5px;color:var(--muted);text-transform:uppercase">&#127758; Province</label>
        <select id="vf-prov" onchange="onVfProv()" style="background:var(--bg);border:1px solid var(--border);color:var(--text);padding:7px 10px;border-radius:4px;font-family:&#39;DM Sans&#39;,sans-serif;font-size:12px;outline:none;transition:border-color .15s">
          <option value="">All provinces</option>
        </select>
      </div>
      <div style="display:flex;flex-direction:column;gap:4px;flex:1;min-width:150px">
        <label style="font-family:&#39;IBM Plex Mono&#39;,monospace;font-size:9px;letter-spacing:1.5px;color:var(--muted);text-transform:uppercase">&#127961; District</label>
        <select id="vf-dist" onchange="renderVillTbl()" style="background:var(--bg);border:1px solid var(--border);color:var(--text);padding:7px 10px;border-radius:4px;font-family:&#39;DM Sans&#39;,sans-serif;font-size:12px;outline:none">
          <option value="">All districts</option>
        </select>
      </div>
      <button onclick="clearVillFilters()" style="height:34px;padding:0 14px;background:transparent;border:1px solid var(--border);color:var(--muted);border-radius:4px;font-family:&#39;DM Sans&#39;,sans-serif;font-size:12px;cursor:pointer">Clear</button>
    </div>
    <div class="vtw" style="max-height:560px">
      <table>
        <thead><tr>
          <th>Village</th><th>Sector</th><th>Cell</th><th>District</th><th>Province</th>
          <th>M15-24</th><th>F15-24</th><th>M25-35</th><th>F25-35</th>
          <th>Total</th><th>Target</th><th>Rem.</th><th>Progress</th><th>Status</th>
        </tr></thead>
        <tbody id="villTbl"></tbody>
      </table>
    </div>
  </div>
</div>

<!-- ═══ COMPLETED ═══ -->
<div class="panel" id="p-completed">
  <div class="pnl mb20">
    <div class="pnl-hd"><span class="pnl-title">✅ Completed survey submissions</span><span class="pnl-badge" id="comp-badge">0 records</span></div>
    <div class="vtw" style="max-height:620px">
      <table>
        <thead><tr><th>#</th><th>Date</th><th>Supervisor</th><th>Province</th><th>District</th><th>Sector</th><th>Village</th><th>M15-24</th><th>F15-24</th><th>M25-35</th><th>F25-35</th><th>Total respondents</th></tr></thead>
        <tbody id="compTbl"><tr><td colspan="12" class="empty-msg">No completed submissions yet.</td></tr></tbody>
      </table>
    </div>
  </div>
</div>

<!-- ═══ INCOMPLETE ═══ -->
<div class="panel" id="p-incomplete">
  <div class="pnl mb20">
    <div class="pnl-hd"><span class="pnl-title">⏸ Incomplete survey submissions</span><span class="pnl-badge pnl-badge-y" id="inc-badge">0 records</span></div>
    <div class="vtw" style="max-height:620px">
      <table>
        <thead><tr><th>#</th><th>Date</th><th>Supervisor</th><th>Province</th><th>District</th><th>Village</th><th>Last section</th><th>Reason stopped</th><th>Started</th><th>Stopped</th><th>Collected</th></tr></thead>
        <tbody id="incTbl"><tr><td colspan="11" class="empty-msg">No incomplete records.</td></tr></tbody>
      </table>
    </div>
  </div>
</div>

<!-- ═══ REPLACEMENT ═══ -->
<div class="panel" id="p-replacement">
  <div class="pnl mb20">
    <div class="pnl-hd"><span class="pnl-title">🔄 Replacement survey submissions</span><span class="pnl-badge pnl-badge-r" id="rep-badge">0 records</span></div>
    <div class="vtw" style="max-height:620px">
      <table>
        <thead><tr><th>#</th><th>Date</th><th>Supervisor</th><th>Province</th><th>District</th><th>Village</th><th>Reason for replacement</th><th>Replacements done</th><th>Male</th><th>Female</th><th>Total</th></tr></thead>
        <tbody id="repTbl"><tr><td colspan="11" class="empty-msg">No replacement records.</td></tr></tbody>
      </table>
    </div>
  </div>
</div>

<!-- ═══ DATA ENTRY (both roles) ═══ -->
<div class="panel" id="p-entry">
  <div class="pnl mb20" style="max-width:860px">
    <div class="pnl-hd"><span class="pnl-title">✏️ Log daily survey progress</span></div>
    <div class="form-pad">
      <div class="sep-lbl">Supervisor & date</div>
      <div class="fg fg3">
        <div class="ff"><label>Supervisor name *</label>
          <select id="f-sn">
            <option value="">Select your name…</option>
            <option value="Jean Paul Bimenyimana">Jean Paul Bimenyimana</option>
            <option value="Tharcille Niyigena">Tharcille Niyigena</option>
            <option value="Consolateur Byishimo Turikumwe">Consolateur Byishimo Turikumwe</option>
            <option value="Elisa Ngabonziza">Elisa Ngabonziza</option>
            <option value="Emmanuel Nkundineza">Emmanuel Nkundineza</option>
            <option value="Didier Nkurunziza">Didier Nkurunziza</option>
            <option value="Aliane Ikuzwe">Aliane Ikuzwe</option>
            <option value="Jean D'Amour Hagabimana">Jean D'Amour Hagabimana</option>
          </select>
        </div>
        <div class="ff"><label>Date *</label><input type="date" id="f-dt" /></div>
        <div class="ff"><label>Survey status *</label>
          <select id="f-st" onchange="onSt()">
            <option value="completed">Completed</option>
            <option value="incomplete">Incomplete</option>
            <option value="replacement">Replacement</option>
          </select>
        </div>
      </div>
      <div class="sep-lbl">Location</div>
      <div class="fg fg4">
        <div class="ff"><label>Province *</label><select id="f-pv" onchange="onPv()"><option value="">Select province…</option></select></div>
        <div class="ff"><label>District *</label><select id="f-di" onchange="onDi()" disabled><option value="">Select province first</option></select></div>
        <div class="ff"><label>Sector *</label><select id="f-se" onchange="onSe()" disabled><option value="">Select district first</option></select></div>
        <div class="ff"><label>Village *</label><select id="f-vi" disabled><option value="">Select sector first</option></select></div>
      </div>
      <div class="sep-lbl">Respondent counts by sex &amp; age</div>
      <div class="fg fg4">
        <div class="ff"><label style="color:var(--my)">Male 15–24</label><input type="number" id="f-m1" min="0" value="0" /></div>
        <div class="ff"><label style="color:var(--fy)">Female 15–24</label><input type="number" id="f-f1" min="0" value="0" /></div>
        <div class="ff"><label style="color:var(--mo)">Male 25–35</label><input type="number" id="f-m2" min="0" value="0" /></div>
        <div class="ff"><label style="color:var(--fo)">Female 25–35</label><input type="number" id="f-f2" min="0" value="0" /></div>
      </div>
      <div id="inc-ext" style="display:none">
        <div class="sep-lbl">Incomplete details</div>
        <div class="fg fg3">
          <div class="ff"><label>Surveys started</label><input type="number" id="f-sta" min="0" value="0" /></div>
          <div class="ff"><label>Surveys not completed</label><input type="number" id="f-sto" min="0" value="0" /></div>
          <div class="ff"><label>Last section reached</label>
            <select id="f-ls">
              <option value="">Select…</option>
              <option>A – Household roster</option><option>B – Education</option><option>C – Employment</option>
              <option>D – Financial inclusion</option><option>E – Migration</option><option>F – Digital literacy</option>
              <option>G – Health</option><option>H – Nutrition</option><option>I – Mental health</option>
              <option>J – Governance</option><option>K – Relationships</option><option>L – Climate</option>
              <option>M – Mobility</option><option>O – Gender norms</option><option>P – Harassment</option>
              <option>Q – Aspirations</option><option>R – Non-cognitive</option><option>T – Time use</option>
              <option>U – Training</option>
            </select>
          </div>
        </div>
        <div class="fg fg2" style="margin-bottom:10px">
          <div class="ff" style="grid-column:span 2"><label>Reason not completed</label><input id="f-sr" placeholder="e.g. Respondents had to leave for the market" /></div>
        </div>
      </div>
      <div id="rep-ext" style="display:none">
        <div class="sep-lbl">Replacement details</div>
        <div class="fg fg3" style="margin-bottom:10px">
          <div class="ff"><label>No. of replacements done</label><input type="number" id="f-rc" min="0" value="0" /></div>
          <div class="ff" style="grid-column:span 2"><label>Reason for replacement</label><input id="f-rr" placeholder="e.g. Planned respondents were unavailable or relocated" /></div>
        </div>
      </div>
      <div class="ff" style="margin-bottom:4px"><label>Notes / field observations</label><textarea id="f-no" placeholder="Any field observations for today…"></textarea></div>
      <button class="submit-btn" onclick="saveRec()">Save record</button>
      <div class="f-err" id="f-err">Please fill in all required fields marked *.</div>
      <div class="f-ok" id="f-ok">Record saved successfully.</div>
    </div>
  </div>
</div>

<!-- ═══ MY LOG (supervisor) ═══ -->
<div class="panel" id="p-mylog">
  <div class="pnl mb20">
    <div class="pnl-hd"><span class="pnl-title">📋 My submitted records</span></div>
    <div class="vtw" style="max-height:620px">
      <table>
        <thead><tr><th>#</th><th>Date</th><th>District</th><th>Village</th><th>Status</th><th>M15-24</th><th>F15-24</th><th>M25-35</th><th>F25-35</th><th>Total</th></tr></thead>
        <tbody id="myTbl"><tr><td colspan="10" class="empty-msg">No records submitted yet.</td></tr></tbody>
      </table>
    </div>
  </div>
</div>

<!-- ═══ SHARE ═══ -->
<div class="panel" id="p-share">
  <div class="pnl mb20" style="max-width:700px">
    <div class="pnl-hd"><span class="pnl-title">🔗 Share portal with supervisors</span></div>
    <div class="form-pad">
      <div class="sep-lbl">Portal link</div>
      <div style="background:var(--bg);border:1px solid var(--border);border-radius:4px;padding:10px 14px;display:flex;align-items:center;gap:10px;margin-bottom:4px">
        <span style="font-family:'IBM Plex Mono',monospace;font-size:12px;color:var(--accent4);flex:1">https://ifpri-rw2025.vanguard-economics.org/portal</span>
        <button onclick="copyTxt(this,'https://ifpri-rw2025.vanguard-economics.org/portal')" style="font-family:'IBM Plex Mono',monospace;font-size:10px;background:transparent;border:1px solid var(--border);color:var(--muted);padding:4px 10px;border-radius:3px;cursor:pointer;letter-spacing:1px">COPY</button>
      </div>
      <div class="sep-lbl" style="margin-top:20px">Access levels</div>
      <table>
        <thead><tr><th>Role</th><th>Access level</th><th>Note</th></tr></thead>
        <tbody>
          <tr><td>Project admin</td><td><span class="sts s-done">FULL DASHBOARD</span></td><td style="font-size:11px;color:var(--muted)">Login details shared privately with admin only</td></tr>
          <tr><td>Field supervisors (shared)</td><td><span class="sts s-prog">DATA ENTRY ONLY</span></td><td style="font-size:11px;color:var(--muted)">Contact admin for login credentials</td></tr>
        </tbody>
      </table>
    </div>
  </div>
</div>

</div><!-- /content -->
</div><!-- /appWrap -->

<script>
// ══════════════════════════════════════════════════════════════════════
// CONFIGURATION — paste your Google Apps Script Web App URL here
// after deploying the script (see setup instructions)
// ══════════════════════════════════════════════════════════════════════
const SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbxkA9xsLJozONMsE61ZcJgsjdMPY1eq3meUPV7RsOvPkcPcz7DWDeXfopcLQpeswNu1Ig/exec';

const CREDS={admin:{pw:'ifpri2025',role:'admin'},supervisor:{pw:'super2025',role:'supervisor'}};
const PER_VIL=20, STRATA_TGT=800;

const VILLAGES=[{"id":1,"province":"Northern Province","district":"Rulindo","sector":"Bushoki","cell":"Kayenzi","village":"Murambo"},{"id":2,"province":"Northern Province","district":"Rulindo","sector":"Cyinzuzi","cell":"Migendezo","village":"Gitabage"},{"id":3,"province":"Northern Province","district":"Rulindo","sector":"Kisaro","cell":"Kamushenyi","village":"Gakenke"},{"id":4,"province":"Northern Province","district":"Rulindo","sector":"Masoro","cell":"Shengampuli","village":"Amataba"},{"id":5,"province":"Northern Province","district":"Rulindo","sector":"Ngoma","cell":"Karambo","village":"Butare"},{"id":6,"province":"Northern Province","district":"Rulindo","sector":"Rukozo","cell":"Mberuka","village":"Gakubo"},{"id":7,"province":"Northern Province","district":"Rulindo","sector":"Tumba","cell":"Gahabwa","village":"Kabuga"},{"id":8,"province":"Northern Province","district":"Gakenke","sector":"Coko","cell":"Mbirima","village":"Akanduga"},{"id":9,"province":"Northern Province","district":"Gakenke","sector":"Gakenke","cell":"Kagoma","village":"Rurambi"},{"id":10,"province":"Northern Province","district":"Gakenke","sector":"Janja","cell":"Gatwa","village":"Nyabushishiri"},{"id":11,"province":"Northern Province","district":"Gakenke","sector":"Karambo","cell":"Kirebe","village":"Kabuye"},{"id":12,"province":"Northern Province","district":"Gakenke","sector":"Minazi","cell":"Munyana","village":"Gitwa"},{"id":13,"province":"Northern Province","district":"Gakenke","sector":"Muhondo","cell":"Musenyi","village":"Buhinya"},{"id":14,"province":"Northern Province","district":"Gakenke","sector":"Nemba","cell":"Buranga","village":"Burego"},{"id":15,"province":"Northern Province","district":"Gakenke","sector":"Rusasa","cell":"Nyundo","village":"Nyundo"},{"id":16,"province":"Northern Province","district":"Musanze","sector":"Cyuve","cell":"Migeshi","village":"Buremu"},{"id":17,"province":"Northern Province","district":"Musanze","sector":"Gashaki","cell":"Muharuro","village":"Bugabo"},{"id":18,"province":"Northern Province","district":"Musanze","sector":"Kinigi","cell":"Nyabigoma","village":"Gasizi"},{"id":19,"province":"Northern Province","district":"Musanze","sector":"Musanze","cell":"Kabazungu","village":"Rucumu"},{"id":20,"province":"Northern Province","district":"Musanze","sector":"Remera","cell":"Gasongero","village":"Gitega"},{"id":21,"province":"Northern Province","district":"Musanze","sector":"Shingiro","cell":"Gakingo","village":"Mutuzo"},{"id":22,"province":"Northern Province","district":"Burera","sector":"Butaro","cell":"Gatsibo","village":"Murambi"},{"id":23,"province":"Northern Province","district":"Burera","sector":"Cyanika","cell":"Kagitega","village":"Gasebeya"},{"id":24,"province":"Northern Province","district":"Burera","sector":"Gahunga","cell":"Gisizi","village":"Gisizi"},{"id":25,"province":"Northern Province","district":"Burera","sector":"Gitovu","cell":"Musasa","village":"Kamusaba"},{"id":26,"province":"Northern Province","district":"Burera","sector":"Kinyababa","cell":"Bugamba","village":"Kabingo"},{"id":27,"province":"Northern Province","district":"Burera","sector":"Nemba","cell":"Kivumu","village":"Mugano"},{"id":28,"province":"Northern Province","district":"Burera","sector":"Rugarama","cell":"Karangara","village":"Sasa"},{"id":29,"province":"Northern Province","district":"Burera","sector":"Ruhunde","cell":"Gitovu","village":"Tetero"},{"id":30,"province":"Northern Province","district":"Burera","sector":"Rwerere","cell":"Ruconsho","village":"Ngoma"},{"id":31,"province":"Northern Province","district":"Gicumbi","sector":"Bwisige","cell":"Nyabushingitwa","village":"Ndayabana"},{"id":32,"province":"Northern Province","district":"Gicumbi","sector":"Cyumba","cell":"Rwankonjo","village":"Rukizi"},{"id":33,"province":"Northern Province","district":"Gicumbi","sector":"Kaniga","cell":"Nyarwambu","village":"Kabeza"},{"id":34,"province":"Northern Province","district":"Gicumbi","sector":"Miyove","cell":"Mubuga","village":"Kacyiru"},{"id":35,"province":"Northern Province","district":"Gicumbi","sector":"Muko","cell":"Rebero","village":"Kirara-Gasizi"},{"id":36,"province":"Northern Province","district":"Gicumbi","sector":"Nyamiyaga","cell":"Karambo","village":"Gaseke"},{"id":37,"province":"Northern Province","district":"Gicumbi","sector":"Rubaya","cell":"Muguramo","village":"Ngange"},{"id":38,"province":"Northern Province","district":"Gicumbi","sector":"Rushaki","cell":"Karurama","village":"Ngabira"},{"id":39,"province":"Northern Province","district":"Gicumbi","sector":"Ruvune","cell":"Kabare","village":"Taba"},{"id":40,"province":"Northern Province","district":"Gicumbi","sector":"Shangasha","cell":"Shangasha","village":"Ryamatebura"},{"id":41,"province":"Eastern Province","district":"Rwamagana","sector":"Gishali","cell":"Ruhimbi","village":"Abakina"},{"id":42,"province":"Eastern Province","district":"Rwamagana","sector":"Munyaga","cell":"Nkungu","village":"Mataba"},{"id":43,"province":"Eastern Province","district":"Rwamagana","sector":"Muyumbu","cell":"Murehe","village":"Ruvomo"},{"id":44,"province":"Eastern Province","district":"Rwamagana","sector":"Rubona","cell":"Byinza","village":"Kabayange Ii"},{"id":45,"province":"Eastern Province","district":"Nyagatare","sector":"Karama","cell":"Cyenkwanzi","village":"Cyenkwanzi Centre"},{"id":46,"province":"Eastern Province","district":"Nyagatare","sector":"Karangazi","cell":"Nyagashanga","village":"Ruhita"},{"id":47,"province":"Eastern Province","district":"Nyagatare","sector":"Katabagemu","cell":"Rugazi","village":"Rwagisangangabo"},{"id":48,"province":"Eastern Province","district":"Nyagatare","sector":"Mukama","cell":"Bufunda","village":"Nyakajeje"},{"id":49,"province":"Eastern Province","district":"Nyagatare","sector":"Nyagatare","cell":"Cyabayaga","village":"Akamonyi"},{"id":50,"province":"Eastern Province","district":"Nyagatare","sector":"Rwempasha","cell":"Gasinga","village":"Gasinga"},{"id":51,"province":"Eastern Province","district":"Nyagatare","sector":"Rwimiyaga","cell":"Rutungu","village":"Gakagati II"},{"id":52,"province":"Eastern Province","district":"Gatsibo","sector":"Gasange","cell":"Teme","village":"Giheta"},{"id":53,"province":"Eastern Province","district":"Gatsibo","sector":"Gitoki","cell":"Rubira","village":"Nyakagarama"},{"id":54,"province":"Eastern Province","district":"Gatsibo","sector":"Kageyo","cell":"Gituza","village":"Gisiza"},{"id":55,"province":"Eastern Province","district":"Gatsibo","sector":"Kiziguro","cell":"Ndatemwa","village":"Rubungo"},{"id":56,"province":"Eastern Province","district":"Gatsibo","sector":"Murambi","cell":"Rwankuba","village":"Umwiga"},{"id":57,"province":"Eastern Province","district":"Gatsibo","sector":"Nyagihanga","cell":"Nyagitabire","village":"Nyamikamba"},{"id":58,"province":"Eastern Province","district":"Gatsibo","sector":"Rugarama","cell":"Matare","village":"Rwankuba"},{"id":59,"province":"Eastern Province","district":"Kayonza","sector":"Gahini","cell":"Juru","village":"Kamudongo"},{"id":60,"province":"Eastern Province","district":"Kayonza","sector":"Kabare","cell":"Rubumba","village":"Bwatampama"},{"id":61,"province":"Eastern Province","district":"Kayonza","sector":"Murama","cell":"Nyakanazi","village":"Rugazi"},{"id":62,"province":"Eastern Province","district":"Kayonza","sector":"Mwiri","cell":"Kageyo","village":"Rugeyo"},{"id":63,"province":"Eastern Province","district":"Kayonza","sector":"Nyamirama","cell":"Musumba","village":"Karama"},{"id":64,"province":"Eastern Province","district":"Kayonza","sector":"Ruramira","cell":"Ruyonza","village":"Kabeza"},{"id":65,"province":"Eastern Province","district":"Kirehe","sector":"Gahara","cell":"Nyagasenyi","village":"Cyabihama I"},{"id":66,"province":"Eastern Province","district":"Kirehe","sector":"Kigarama","cell":"Kigarama","village":"Samuko"},{"id":67,"province":"Eastern Province","district":"Kirehe","sector":"Kirehe","cell":"Nyabikokora","village":"Kwirebero"},{"id":68,"province":"Eastern Province","district":"Kirehe","sector":"Mpanga","cell":"Rubaya","village":"Rubaya"},{"id":69,"province":"Eastern Province","district":"Kirehe","sector":"Nasho","cell":"Cyambwe","village":"Kagamba"},{"id":70,"province":"Eastern Province","district":"Kirehe","sector":"Nyarubuye","cell":"Mareba","village":"Kaziba II"},{"id":71,"province":"Eastern Province","district":"Ngoma","sector":"Jarama","cell":"Kigoma","village":"Vunga"},{"id":72,"province":"Eastern Province","district":"Ngoma","sector":"Mugesera","cell":"Mugatare","village":"Kampara"},{"id":73,"province":"Eastern Province","district":"Ngoma","sector":"Remera","cell":"Bugera","village":"Kabeza"},{"id":74,"province":"Eastern Province","district":"Ngoma","sector":"Rukumberi","cell":"Rubago","village":"Kavumve"},{"id":75,"province":"Eastern Province","district":"Ngoma","sector":"Sake","cell":"Rukoma","village":"Muminoga"},{"id":76,"province":"Eastern Province","district":"Bugesera","sector":"Juru","cell":"Mugorore","village":"Gatora"},{"id":77,"province":"Eastern Province","district":"Bugesera","sector":"Mayange","cell":"Kibenga","village":"Rwakaramira"},{"id":78,"province":"Eastern Province","district":"Bugesera","sector":"Ngeruka","cell":"Gihembe","village":"Kagasa"},{"id":79,"province":"Eastern Province","district":"Bugesera","sector":"Nyarugenge","cell":"Gihinga","village":"Nyagasozi"},{"id":80,"province":"Eastern Province","district":"Bugesera","sector":"Shyara","cell":"Rutare","village":"Rutare"},{"id":81,"province":"Southern Province","district":"Nyanza","sector":"Cyabakamyi","cell":"Kadaho","village":"Gataba"},{"id":82,"province":"Southern Province","district":"Nyanza","sector":"Kigoma","cell":"Butansinda","village":"Karama"},{"id":83,"province":"Southern Province","district":"Nyanza","sector":"Mukingo","cell":"Mpanga","village":"Remera"},{"id":84,"province":"Southern Province","district":"Nyanza","sector":"Ntyazo","cell":"Cyotamakara","village":"Kankima"},{"id":85,"province":"Southern Province","district":"Nyanza","sector":"Rwabicuma","cell":"Nyarusange","village":"Kamuvunyi A"},{"id":86,"province":"Southern Province","district":"Gisagara","sector":"Kansi","cell":"Akaboti","village":"Akabuga"},{"id":87,"province":"Southern Province","district":"Gisagara","sector":"Kigembe","cell":"Nyabikenke","village":"Shyombo"},{"id":88,"province":"Southern Province","district":"Gisagara","sector":"Muganza","cell":"Muganza","village":"Agasharu"},{"id":89,"province":"Southern Province","district":"Gisagara","sector":"Mukindo","cell":"Gitega","village":"Rebero"},{"id":90,"province":"Southern Province","district":"Gisagara","sector":"Ndora","cell":"Dahwe","village":"Gitwa"},{"id":91,"province":"Southern Province","district":"Nyaruguru","sector":"Busanze","cell":"Kirarangombe","village":"Kinyinya"},{"id":92,"province":"Southern Province","district":"Nyaruguru","sector":"Kibeho","cell":"Mubuga","village":"Nyarwumba"},{"id":93,"province":"Southern Province","district":"Nyaruguru","sector":"Muganza","cell":"Samiyonga","village":"Murambi"},{"id":94,"province":"Southern Province","district":"Nyaruguru","sector":"Ngoma","cell":"Mbuye","village":"Mugobe"},{"id":95,"province":"Southern Province","district":"Nyaruguru","sector":"Ruheru","cell":"Remera","village":"Kirwa"},{"id":96,"province":"Southern Province","district":"Huye","sector":"Gishamvu","cell":"Nyumba","village":"Busoro"},{"id":97,"province":"Southern Province","district":"Huye","sector":"Kigoma","cell":"Karambi","village":"Gitwa"},{"id":98,"province":"Southern Province","district":"Huye","sector":"Maraba","cell":"Shanga","village":"Mpinga"},{"id":99,"province":"Southern Province","district":"Huye","sector":"Ruhashya","cell":"Gatovu","village":"Kiyanza"},{"id":100,"province":"Southern Province","district":"Huye","sector":"Rwaniro","cell":"Nyaruhombo","village":"Murambi"},{"id":101,"province":"Southern Province","district":"Nyamagabe","sector":"Buruhukiro","cell":"Rambya","village":"Mpanga"},{"id":102,"province":"Southern Province","district":"Nyamagabe","sector":"Kaduha","cell":"Kavumu","village":"Karehe"},{"id":103,"province":"Southern Province","district":"Nyamagabe","sector":"Kibumbwe","cell":"Kibibi","village":"Kirwa"},{"id":104,"province":"Southern Province","district":"Nyamagabe","sector":"Mugano","cell":"Sovu","village":"Rugarama Ii"},{"id":105,"province":"Southern Province","district":"Nyamagabe","sector":"Mushubi","cell":"Gashwati","village":"Mushubi"},{"id":106,"province":"Southern Province","district":"Nyamagabe","sector":"Uwinkingi","cell":"Munyege","village":"Nyarurambi"},{"id":107,"province":"Southern Province","district":"Ruhango","sector":"Byimana","cell":"Nyakabuye","village":"Nyarubumbiro"},{"id":108,"province":"Southern Province","district":"Ruhango","sector":"Kinazi","cell":"Rutabo","village":"Gitwa"},{"id":109,"province":"Southern Province","district":"Ruhango","sector":"Mbuye","cell":"Mwendo","village":"Ipate"},{"id":110,"province":"Southern Province","district":"Ruhango","sector":"Ntongwe","cell":"Nyakabungo","village":"Kigabiro"},{"id":111,"province":"Southern Province","district":"Ruhango","sector":"Ruhango","cell":"Tambwe","village":"Ruduha I"},{"id":112,"province":"Southern Province","district":"Muhanga","sector":"Muhanga","cell":"Kibangu","village":"Gitega"},{"id":113,"province":"Southern Province","district":"Muhanga","sector":"Muhanga","cell":"Muhanga","village":"Tyazo"},{"id":114,"province":"Southern Province","district":"Muhanga","sector":"Muhanga","cell":"Nyarusange","village":"Musongati"},{"id":115,"province":"Southern Province","district":"Muhanga","sector":"Muhanga","cell":"Shyogwe","village":"Kinini"},{"id":116,"province":"Southern Province","district":"Kamonyi","sector":"Kayenzi","cell":"Bugarama","village":"Remera"},{"id":117,"province":"Southern Province","district":"Kamonyi","sector":"Mugina","cell":"Mugina","village":"Mugina"},{"id":118,"province":"Southern Province","district":"Kamonyi","sector":"Nyamiyaga","cell":"Kabashumba","village":"Bumbogo"},{"id":119,"province":"Southern Province","district":"Kamonyi","sector":"Rugarika","cell":"Bihembe","village":"Karama"},{"id":120,"province":"Southern Province","district":"Kamonyi","sector":"Runda","cell":"Kagina","village":"Rugarama"},{"id":121,"province":"Western Province","district":"Karongi","sector":"Gishyita","cell":"Munanira","village":"Nyakabuye"},{"id":122,"province":"Western Province","district":"Karongi","sector":"Mubuga","cell":"Nyagatovu","village":"Nyankira"},{"id":123,"province":"Western Province","district":"Karongi","sector":"Mutuntu","cell":"Byogo","village":"Musango"},{"id":124,"province":"Western Province","district":"Karongi","sector":"Rugabano","cell":"Gitovu","village":"Gatobo"},{"id":125,"province":"Western Province","district":"Karongi","sector":"Rwankuba","cell":"Munini","village":"Gakangaga"},{"id":126,"province":"Western Province","district":"Rutsiro","sector":"Boneza","cell":"Kabihogo","village":"Rugamba"},{"id":127,"province":"Western Province","district":"Rutsiro","sector":"Kigeyo","cell":"Nyagahinika","village":"Nyarusuku"},{"id":128,"province":"Western Province","district":"Rutsiro","sector":"Manihira","cell":"Tangabo","village":"Munini"},{"id":129,"province":"Western Province","district":"Rutsiro","sector":"Murunda","cell":"Mburamazi","village":"Rukingu"},{"id":130,"province":"Western Province","district":"Rutsiro","sector":"Mushubati","cell":"Bumba","village":"Bisyo"},{"id":131,"province":"Western Province","district":"Rutsiro","sector":"Nyabirasi","cell":"Ngoma","village":"Nkuna"},{"id":132,"province":"Western Province","district":"Rutsiro","sector":"Rusebeya","cell":"Remera","village":"Gahunga"},{"id":133,"province":"Western Province","district":"Rubavu","sector":"Busasamana","cell":"Gasiza","village":"Kiraro"},{"id":134,"province":"Western Province","district":"Rubavu","sector":"Cyanzarwe","cell":"Rwanzekuma","village":"Munaba"},{"id":135,"province":"Western Province","district":"Rubavu","sector":"Nyakiriba","cell":"Bisizi","village":"Bweza"},{"id":136,"province":"Western Province","district":"Rubavu","sector":"Nyundo","cell":"Kavomo","village":"Bahimba"},{"id":137,"province":"Western Province","district":"Nyabihu","sector":"Jenda","cell":"Gasizi","village":"Kanzenze"},{"id":138,"province":"Western Province","district":"Nyabihu","sector":"Kabatwa","cell":"Gihorwe","village":"Rushubi"},{"id":139,"province":"Western Province","district":"Nyabihu","sector":"Kintobo","cell":"Rukondo","village":"Kimpundu"},{"id":140,"province":"Western Province","district":"Nyabihu","sector":"Rambura","cell":"Mutaho","village":"Kiraza"},{"id":141,"province":"Western Province","district":"Nyabihu","sector":"Rurembo","cell":"Murambi","village":"Muremure"},{"id":142,"province":"Western Province","district":"Ngororero","sector":"Gatumba","cell":"Gatsibo","village":"Kimirama"},{"id":143,"province":"Western Province","district":"Ngororero","sector":"Kabaya","cell":"Mwendo","village":"Karambi"},{"id":144,"province":"Western Province","district":"Ngororero","sector":"Kavumu","cell":"Nyamugeyo","village":"Kabere"},{"id":145,"province":"Western Province","district":"Ngororero","sector":"Muhanda","cell":"Gasiza","village":"Nyenyeri"},{"id":146,"province":"Western Province","district":"Ngororero","sector":"Ndaro","cell":"Bitabage","village":"Nyamugari"},{"id":147,"province":"Western Province","district":"Ngororero","sector":"Nyange","cell":"Nsibo","village":"Nyarusange"},{"id":148,"province":"Western Province","district":"Rusizi","sector":"Butare","cell":"Gatereri","village":"Rwibutso"},{"id":149,"province":"Western Province","district":"Rusizi","sector":"Giheke","cell":"Giheke","village":"Karambo"},{"id":150,"province":"Western Province","district":"Rusizi","sector":"Gikundamvura","cell":"Mpinga","village":"Rebero"},{"id":151,"province":"Western Province","district":"Rusizi","sector":"Nkanka","cell":"Kamanyenga","village":"Hepfo"},{"id":152,"province":"Western Province","district":"Rusizi","sector":"Nyakabuye","cell":"Gaseke","village":"Muyange"},{"id":153,"province":"Western Province","district":"Rusizi","sector":"Nzahaha","cell":"Rwinzuki","village":"Kiranga"},{"id":154,"province":"Western Province","district":"Nyamasheke","sector":"Cyato","cell":"Bisumo","village":"Hangari"},{"id":155,"province":"Western Province","district":"Nyamasheke","sector":"Kagano","cell":"Gako","village":"Gasharu"},{"id":156,"province":"Western Province","district":"Nyamasheke","sector":"Karambi","cell":"Gasovu","village":"Nyarugenge"},{"id":157,"province":"Western Province","district":"Nyamasheke","sector":"Kirimbi","cell":"Cyimpindu","village":"Gitwa"},{"id":158,"province":"Western Province","district":"Nyamasheke","sector":"Macuba","cell":"Vugangoma","village":"Nyagahinga"},{"id":159,"province":"Western Province","district":"Nyamasheke","sector":"Rangiro","cell":"Jurwe","village":"Gasebeya-Kibavu"},{"id":160,"province":"Western Province","district":"Nyamasheke","sector":"Shangi","cell":"Shangi","village":"Taba"}];

// village totals keyed by id
let VT={};
VILLAGES.forEach(v=>{VT[v.id]={m1:0,f1:0,m2:0,f2:0}});

let records=[];
let role=null;
let activeDist='ALL';

// ── Google Sheets API helpers ─────────────────────────────────────────────────
function showLoader(msg){
  let el=document.getElementById('loader-bar');
  if(!el){
    el=document.createElement('div');
    el.id='loader-bar';
    el.style.cssText='position:fixed;top:0;left:0;right:0;height:3px;background:linear-gradient(90deg,var(--accent),var(--accent4));z-index:9999;animation:loader-anim 1.2s ease infinite';
    document.head.insertAdjacentHTML('beforeend','<style>@keyframes loader-anim{0%{transform:scaleX(0);transform-origin:left}50%{transform:scaleX(1);transform-origin:left}51%{transform:scaleX(1);transform-origin:right}100%{transform:scaleX(0);transform-origin:right}}</style>');
    document.body.appendChild(el);
  }
  el.style.display='block';
  if(msg) showStatus(msg,'info');
}
function hideLoader(){
  const el=document.getElementById('loader-bar');
  if(el) el.style.display='none';
}
function showStatus(msg,type='info'){
  let el=document.getElementById('status-toast');
  if(!el){
    el=document.createElement('div');
    el.id='status-toast';
    el.style.cssText='position:fixed;bottom:20px;right:20px;padding:10px 16px;border-radius:6px;font-family:\'IBM Plex Mono\',monospace;font-size:11px;z-index:9999;transition:opacity .3s;letter-spacing:.5px;max-width:320px';
    document.body.appendChild(el);
  }
  const colors={info:'background:var(--surface);border:1px solid var(--border);color:var(--muted)',
    ok:'background:rgba(0,212,168,.12);border:1px solid rgba(0,212,168,.3);color:var(--accent)',
    err:'background:rgba(255,107,107,.12);border:1px solid rgba(255,107,107,.3);color:var(--accent2)'};
  el.style.cssText+=';'+colors[type];
  el.textContent=msg;el.style.opacity='1';
  clearTimeout(el._t);
  el._t=setTimeout(()=>{el.style.opacity='0';},3500);
}

async function apiGet(){
  if(SCRIPT_URL==='YOUR_GOOGLE_APPS_SCRIPT_URL_HERE'){
    showStatus('⚠ No script URL configured — running in offline mode','err');
    return null;
  }
  try{
    showLoader('Fetching data…');
    const res=await fetch(SCRIPT_URL+'?action=getAll',{method:'GET'});
    const json=await res.json();
    hideLoader();
    return json.ok?json.records:null;
  }catch(e){hideLoader();showStatus('⚠ Could not connect to database: '+e.message,'err');return null;}
}

async function apiPost(payload){
  if(SCRIPT_URL==='YOUR_GOOGLE_APPS_SCRIPT_URL_HERE') return {ok:false,offline:true};
  try{
    const res=await fetch(SCRIPT_URL,{
      method:'POST',
      body:JSON.stringify(payload)
    });
    return await res.json();
  }catch(e){showStatus('⚠ Save failed: '+e.message,'err');return {ok:false};}
}

function applyRecords(rawRows){
  // Convert Google Sheets rows to our record format
  records=rawRows.map(r=>({
    id:r['ID'],
    supervisor:r['Supervisor'],
    date:r['Date'],
    province:r['Province'],
    district:r['District'],
    sector:r['Sector'],
    village:r['Village'],
    vid:parseInt(r['VillageID'])||0,
    status:r['Status'],
    m1:parseInt(r['M15-24'])||0,
    f1:parseInt(r['F15-24'])||0,
    m2:parseInt(r['M25-35'])||0,
    f2:parseInt(r['F25-35'])||0,
    total:parseInt(r['Total'])||0,
    started:parseInt(r['Started'])||0,
    stopped:parseInt(r['Stopped'])||0,
    lastSection:r['LastSection']||'',
    stopReason:r['StopReason']||'',
    repCount:parseInt(r['ReplacementCount'])||0,
    repReason:r['ReplacementReason']||'',
    notes:r['Notes']||'',
  }));
  rebuildVT();
}

async function loadRecordsFromSheet(){
  const rows=await apiGet();
  if(rows!==null){applyRecords(rows);showStatus('✓ Data loaded — '+records.length+' records','ok');}
  refreshAdmin();
}

function rebuildVT(){
  VILLAGES.forEach(v=>{VT[v.id]={m1:0,f1:0,m2:0,f2:0}});
  records.forEach(r=>{if(r.vid&&VT[r.vid]){VT[r.vid].m1+=r.m1;VT[r.vid].f1+=r.f1;VT[r.vid].m2+=r.m2;VT[r.vid].f2+=r.f2;}});
}

// Keep localStorage as offline fallback
function saveLocalFallback(){
  try{localStorage.setItem('ifpri_rw2025_backup',JSON.stringify(records));}catch(e){}
}
function loadLocalFallback(){
  try{
    const s=localStorage.getItem('ifpri_rw2025_backup');
    if(s){const p=JSON.parse(s);applyRecords(p.map(r=>({
      'ID':r.id,'Supervisor':r.supervisor,'Date':r.date,
      'Province':r.province,'District':r.district,'Sector':r.sector,
      'Village':r.village,'VillageID':r.vid,'Status':r.status,
      'M15-24':r.m1,'F15-24':r.f1,'M25-35':r.m2,'F25-35':r.f2,'Total':r.total,
      'Started':r.started,'Stopped':r.stopped,'LastSection':r.lastSection,
      'StopReason':r.stopReason,'ReplacementCount':r.repCount,
      'ReplacementReason':r.repReason,'Notes':r.notes
    })));}
  }catch(e){}
}

// No seed data — fresh start for live deployment

// ── Login ──
document.getElementById('lp').addEventListener('keydown',e=>{if(e.key==='Enter')doLogin();});
document.getElementById('lu').addEventListener('keydown',e=>{if(e.key==='Enter')doLogin();});

function doLogin(){
  const u=document.getElementById('lu').value.trim();
  const p=document.getElementById('lp').value;
  const e=document.getElementById('lerr');
  if(CREDS[u]&&CREDS[u].pw===p){
    e.style.display='none'; role=CREDS[u].role;
    document.getElementById('loginWrap').style.display='none';
    document.getElementById('appWrap').style.display='block';
    document.getElementById('rolePill').textContent=role.toUpperCase();
    document.getElementById('rolePill').className='role-pill '+(role==='admin'?'rp-admin':'rp-sup');
    document.getElementById('hdrTitle').textContent=role==='admin'?'Youth Survey — Field Progress Dashboard':'Youth Survey — Data Entry';
    document.getElementById('hdrDate').textContent=new Date().toLocaleDateString('en-GB',{weekday:'short',day:'2-digit',month:'short',year:'numeric'});
    if(role==='admin'){
      document.getElementById('adminTabs').style.display='flex';
      document.getElementById('refreshBtn').style.display='block';
      showPanel('overview');
      loadRecordsFromSheet();   // fetch live from Google Sheets
    } else {
      document.getElementById('supTabs').style.display='flex';
      showPanel('entry'); initForm();
      loadRecordsFromSheet();   // load for "My submissions" tab
    }
  } else { e.style.display='block'; }
}

function doLogout(){
  role=null;
  document.getElementById('loginWrap').style.display='flex';
  document.getElementById('appWrap').style.display='none';
  document.getElementById('adminTabs').style.display='none';
  document.getElementById('supTabs').style.display='none';
  document.getElementById('lu').value='';document.getElementById('lp').value='';
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('on'));
}

function showPanel(id){
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('on'));
  document.getElementById('p-'+id).classList.add('on');
}

function swTab(el){
  const tabs=el.closest('.tabs');
  tabs.querySelectorAll('.tab').forEach(t=>t.classList.remove('on','on-b','on-y','on-r'));
  const pid=el.dataset.panel;
  el.classList.add('on');
  showPanel(pid);
  if(['overview','villages','completed','incomplete','replacement'].includes(pid)) refreshAdmin();
  if(pid==='mylog') refreshMyLog();
}

// ── Form cascading ──
function initForm(){
  const psel=document.getElementById('f-pv');
  psel.innerHTML='<option value="">Select province…</option>';
  const provs=[...new Set(VILLAGES.map(v=>v.province))].sort();
  provs.forEach(p=>{const o=document.createElement('option');o.value=p;o.textContent=p;psel.appendChild(o);});
  document.getElementById('f-dt').value=new Date().toISOString().slice(0,10);
}
function onPv(){
  const p=document.getElementById('f-pv').value;
  const dd=document.getElementById('f-di'),sd=document.getElementById('f-se'),vd=document.getElementById('f-vi');
  dd.innerHTML='<option value="">Select district…</option>';
  sd.innerHTML='<option value="">Select district first</option>';
  vd.innerHTML='<option value="">Select sector first</option>';
  sd.disabled=true;vd.disabled=true;
  if(p){
    const dists=[...new Set(VILLAGES.filter(v=>v.province===p).map(v=>v.district))].sort();
    dists.forEach(d=>{const o=document.createElement('option');o.value=d;o.textContent=d;dd.appendChild(o);});
    dd.disabled=false;
  } else dd.disabled=true;
}
function onDi(){
  const p=document.getElementById('f-pv').value,d=document.getElementById('f-di').value;
  const sd=document.getElementById('f-se'),vd=document.getElementById('f-vi');
  sd.innerHTML='<option value="">Select sector…</option>';
  vd.innerHTML='<option value="">Select sector first</option>';
  vd.disabled=true;
  if(d){
    const secs=[...new Set(VILLAGES.filter(v=>v.province===p&&v.district===d).map(v=>v.sector))].sort();
    secs.forEach(s=>{const o=document.createElement('option');o.value=s;o.textContent=s;sd.appendChild(o);});
    sd.disabled=false;
  } else sd.disabled=true;
}
function onSe(){
  const p=document.getElementById('f-pv').value,d=document.getElementById('f-di').value,s=document.getElementById('f-se').value;
  const vd=document.getElementById('f-vi');
  vd.innerHTML='<option value="">Select village…</option>';
  if(s){
    VILLAGES.filter(v=>v.province===p&&v.district===d&&v.sector===s).forEach(v=>{
      const o=document.createElement('option');o.value=v.id;o.textContent=v.village;vd.appendChild(o);
    });
    vd.disabled=false;
  } else vd.disabled=true;
}
function onSt(){
  const s=document.getElementById('f-st').value;
  document.getElementById('inc-ext').style.display=s==='incomplete'?'block':'none';
  document.getElementById('rep-ext').style.display=s==='replacement'?'block':'none';
}

function saveRec(){
  const sn=document.getElementById('f-sn').value.trim();
  const dt=document.getElementById('f-dt').value;
  const pv=document.getElementById('f-pv').value;
  const di=document.getElementById('f-di').value;
  const se=document.getElementById('f-se').value;
  const vi=document.getElementById('f-vi').value;
  const err=document.getElementById('f-err'),ok=document.getElementById('f-ok');
  if(!sn||!dt||!pv||!di||!se||!vi){err.style.display='block';ok.style.display='none';return;}
  err.style.display='none';
  const vid=parseInt(vi);
  const vobj=VILLAGES.find(v=>v.id===vid);
  const st=document.getElementById('f-st').value;
  const m1=+document.getElementById('f-m1').value||0,f1=+document.getElementById('f-f1').value||0;
  const m2=+document.getElementById('f-m2').value||0,f2=+document.getElementById('f-f2').value||0;
  const total=m1+f1+m2+f2;
  const rec={
    id:records.length+1, supervisor:sn, date:dt,
    province:pv, district:di, sector:se, village:vobj?vobj.village:'', vid,
    status:st, m1,f1,m2,f2,total,
    started:+document.getElementById('f-sta').value||0,
    stopped:+document.getElementById('f-sto').value||0,
    lastSection:document.getElementById('f-ls').value,
    stopReason:document.getElementById('f-sr').value,
    repCount:+document.getElementById('f-rc').value||0,
    repReason:document.getElementById('f-rr').value,
    notes:document.getElementById('f-no').value,
  };
  // Optimistic UI — show locally immediately
  const tempId='tmp_'+Date.now();
  rec.id=tempId;
  records.push(rec);
  if(VT[vid]){VT[vid].m1+=m1;VT[vid].f1+=f1;VT[vid].m2+=m2;VT[vid].f2+=f2;}
  ok.style.display='block';
  setTimeout(()=>{ok.style.display='none';},3000);
  clearForm();
  refreshAdmin();
  document.getElementById('tp-my').textContent=records.length;
  saveLocalFallback();
  // Save to Google Sheets in background
  showStatus('⏳ Saving to database…','info');
  apiPost({action:'add',record:rec}).then(res=>{
    if(res.ok){
      // Replace temp id with real id from server
      const idx=records.findIndex(r=>r.id===tempId);
      if(idx>=0)records[idx].id=res.id;
      saveLocalFallback();
      showStatus('✅ Saved to Google Sheets','ok');
    } else if(!res.offline){
      showStatus('⚠ Saved locally only — will retry on next reload','err');
    }
  });
}

function clearForm(){
  ['f-sn','f-sr','f-rr','f-no'].forEach(id=>{document.getElementById(id).value='';});
  ['f-m1','f-f1','f-m2','f-f2','f-sta','f-sto','f-rc'].forEach(id=>{document.getElementById(id).value=0;});
  document.getElementById('f-st').value='completed';
  document.getElementById('f-ls').selectedIndex=0;
  document.getElementById('f-pv').value='';
  document.getElementById('f-di').innerHTML='<option value="">Select province first</option>';
  document.getElementById('f-di').disabled=true;
  document.getElementById('f-se').innerHTML='<option value="">Select district first</option>';
  document.getElementById('f-se').disabled=true;
  document.getElementById('f-vi').innerHTML='<option value="">Select sector first</option>';
  document.getElementById('f-vi').disabled=true;
  document.getElementById('f-dt').value=new Date().toISOString().slice(0,10);
  document.getElementById('inc-ext').style.display='none';
  document.getElementById('rep-ext').style.display='none';
  document.getElementById('f-err').style.display='none';
}

function refreshMyLog(){
  const mine=[...records].reverse();
  document.getElementById('tp-my').textContent=records.length;
  document.getElementById('myTbl').innerHTML=mine.length?mine.map(r=>`<tr>
    <td class="td-m">${r.id}</td>
    <td class="td-m">${r.date}</td>
    <td>${r.district}</td><td>${r.village}</td>
    <td><span class="sts s-${r.status==='completed'?'comp':r.status==='incomplete'?'inc':'rep'}">${r.status.toUpperCase()}</span></td>
    <td class="td-r" style="color:var(--my)">${r.m1}</td>
    <td class="td-r" style="color:var(--fy)">${r.f1}</td>
    <td class="td-r" style="color:var(--mo)">${r.m2}</td>
    <td class="td-r" style="color:var(--fo)">${r.f2}</td>
    <td class="td-r" style="font-weight:600">${r.total}</td>
  </tr>`).join(''):'<tr><td colspan="10" class="empty-msg">No records yet.</td></tr>';
}

// ── Admin refresh ──
function refreshAdmin(){
  const comp=records.filter(r=>r.status==='completed');
  const inc=records.filter(r=>r.status==='incomplete');
  const rep=records.filter(r=>r.status==='replacement');
  const totRes=records.reduce((a,r)=>a+r.total,0);
  const totM1=records.reduce((a,r)=>a+r.m1,0),totF1=records.reduce((a,r)=>a+r.f1,0);
  const totM2=records.reduce((a,r)=>a+r.m2,0),totF2=records.reduce((a,r)=>a+r.f2,0);
  const totRepCount=rep.reduce((a,r)=>a+r.repCount,0);
  const vilActive=new Set(records.map(r=>r.vid));
  const vilDone=VILLAGES.filter(v=>(VT[v.id].m1+VT[v.id].f1+VT[v.id].m2+VT[v.id].f2)>=PER_VIL);
  const pct=Math.round(totRes/3200*100);

  // pills
  document.getElementById('tp-c').textContent=comp.length;
  document.getElementById('tp-i').textContent=inc.length;
  document.getElementById('tp-r').textContent=rep.length;

  // stat cards
  set('s-tot',totRes.toLocaleString()); set('s-tot-sub',`of 3,200 target · ${pct}%`); sw('sp-tot',pct);
  set('s-act',vilActive.size); sw('sp-act',Math.round(vilActive.size/160*100));
  set('s-don',vilDone.length); sw('sp-don',Math.round(vilDone.length/160*100));
  set('s-inc',inc.length); set('s-inc-sub',`${inc.length} logged submissions`); sw('sp-inc',Math.min(100,inc.length*5));
  set('s-rep',totRepCount); set('s-rep-sub',`across ${rep.length} submissions`); sw('sp-rep',Math.min(100,totRepCount*2));
  set('s-pct',pct+'%'); set('s-rem',`${(3200-totRes).toLocaleString()} remaining`); sw('sp-pct',pct);

  // strata
  const t=STRATA_TGT;
  [['st1',totM1],['st2',totF1],['st3',totM2],['st4',totF2]].forEach(([id,v])=>{
    const p=Math.round(v/t*100);
    set(`${id}-c`,`${v}/${t}`); sw(`${id}-b`,p); set(`${id}-p`,p+'%');
  });

  // district list
  buildDistList();

  // main overview table
  document.getElementById('vt-title').textContent=activeDist==='ALL'?'All Submissions':activeDist+' Submissions';
  const shown=activeDist==='ALL'?records:[...records].filter(r=>r.district===activeDist);
  document.getElementById('vt-badge').textContent=shown.length+' records';
  const tgt=PER_VIL;
  const isAdmin=role==='admin';
  if(isAdmin){
    document.getElementById('admin-actions-th').style.display='';
    document.getElementById('clearAllBtn').style.display='';
  }
  document.getElementById('mainTbl').innerHTML=shown.length?[...shown].reverse().map(r=>`<tr>
    <td class="td-m" style="font-family:'IBM Plex Mono',monospace">${r.id}</td>
    <td class="td-m">${r.date}</td><td>${r.supervisor}</td>
    <td class="td-m">${r.province.replace(' Province','')}</td><td>${r.district}</td>
    <td style="font-weight:500">${r.village}</td>
    <td><span class="sts s-${r.status==='completed'?'comp':r.status==='incomplete'?'inc':'rep'}">${r.status==='completed'?'✅':r.status==='incomplete'?'⏸':'🔄'} ${r.status.toUpperCase()}</span></td>
    <td class="td-r" style="color:var(--my)">${r.m1}</td>
    <td class="td-r" style="color:var(--fy)">${r.f1}</td>
    <td class="td-r" style="color:var(--mo)">${r.m2}</td>
    <td class="td-r" style="color:var(--fo)">${r.f2}</td>
    <td class="td-r" style="font-weight:600">${r.total}</td>
    <td><div style="display:flex;align-items:center;gap:4px;min-width:70px"><div style="flex:1;height:3px;background:var(--border);border-radius:2px;overflow:hidden"><div style="height:100%;width:${Math.min(100,Math.round(r.total/tgt*100))}%;background:${r.total>=tgt?'var(--accent)':'var(--accent3)'}"></div></div><span style="font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--muted)">${Math.min(100,Math.round(r.total/tgt*100))}%</span></div></td>
    ${isAdmin?`<td><div style="display:flex;gap:5px"><button onclick="openEdit(${r.id})" style="height:22px;padding:0 8px;background:rgba(116,185,255,.1);border:1px solid rgba(116,185,255,.25);color:var(--accent4);border-radius:3px;font-size:10px;cursor:pointer;font-family:'IBM Plex Mono',monospace">✏</button><button onclick="deleteRec(${r.id})" style="height:22px;padding:0 8px;background:rgba(255,107,107,.1);border:1px solid rgba(255,107,107,.25);color:var(--accent2);border-radius:3px;font-size:10px;cursor:pointer;font-family:'IBM Plex Mono',monospace">🗑</button></div></td>`:'<td></td>'}
  </tr>`).join(''):'<tr><td colspan="14" class="empty-msg">No submissions yet. Supervisors can log data from the portal link.</td></tr>';

  // village table — deferred to renderVillTbl()
  renderVillTbl();

  // completed tab
  document.getElementById('comp-badge').textContent=comp.length+' records';
  document.getElementById('compTbl').innerHTML=comp.length?comp.map((r,i)=>`<tr>
    <td class="td-m">${i+1}</td><td class="td-m">${r.date}</td><td>${r.supervisor}</td>
    <td class="td-m">${r.province.replace(' Province','')}</td><td>${r.district}</td>
    <td class="td-m">${r.sector}</td><td style="font-weight:500">${r.village}</td>
    <td class="td-r" style="color:var(--my)">${r.m1}</td><td class="td-r" style="color:var(--fy)">${r.f1}</td>
    <td class="td-r" style="color:var(--mo)">${r.m2}</td><td class="td-r" style="color:var(--fo)">${r.f2}</td>
    <td class="td-r" style="font-weight:600">${r.total}</td>
  </tr>`).join(''):'<tr><td colspan="12" class="empty-msg">No completed records.</td></tr>';

  // incomplete tab
  document.getElementById('inc-badge').textContent=inc.length+' records';
  document.getElementById('incTbl').innerHTML=inc.length?inc.map((r,i)=>`<tr>
    <td class="td-m">${i+1}</td><td class="td-m">${r.date}</td><td>${r.supervisor}</td>
    <td class="td-m">${r.province.replace(' Province','')}</td><td>${r.district}</td>
    <td style="font-weight:500">${r.village}</td>
    <td class="td-m">${r.lastSection||'—'}</td>
    <td style="color:var(--accent3)">${r.stopReason||'—'}</td>
    <td class="td-r">${r.started}</td><td class="td-r">${r.stopped}</td>
    <td class="td-r" style="font-weight:600">${r.total}</td>
  </tr>`).join(''):'<tr><td colspan="11" class="empty-msg">No incomplete records.</td></tr>';

  // replacement tab
  document.getElementById('rep-badge').textContent=rep.length+' records';
  document.getElementById('repTbl').innerHTML=rep.length?rep.map((r,i)=>`<tr>
    <td class="td-m">${i+1}</td><td class="td-m">${r.date}</td><td>${r.supervisor}</td>
    <td class="td-m">${r.province.replace(' Province','')}</td><td>${r.district}</td>
    <td style="font-weight:500">${r.village}</td>
    <td style="color:var(--accent2)">${r.repReason||'—'}</td>
    <td class="td-r" style="font-weight:600">${r.repCount}</td>
    <td class="td-r" style="color:var(--my)">${r.m1}</td>
    <td class="td-r" style="color:var(--fy)">${r.f1}</td>
    <td class="td-r" style="font-weight:600">${r.total}</td>
  </tr>`).join(''):'<tr><td colspan="11" class="empty-msg">No replacement records.</td></tr>';

  // daily chart
  const dayMap={};
  records.forEach(r=>{dayMap[r.date]=(dayMap[r.date]||0)+r.total;});
  const days=Object.keys(dayMap).sort().slice(-7);
  const maxD=Math.max(1,...days.map(d=>dayMap[d]));
  const dc=document.getElementById('dailyChart');
  dc.innerHTML=days.length?days.map(d=>`
    <div class="bar-col">
      <div class="bar-val">${dayMap[d]}</div>
      <div class="bar-stack"><div class="bar-seg" style="height:${Math.round(dayMap[d]/maxD*75)}px;background:var(--accent);opacity:.85"></div></div>
      <div class="bar-lbl">${d.slice(5)}</div>
    </div>`).join(''):'<div style="color:var(--muted);font-size:12px;align-self:center;padding:16px">No submissions yet</div>';

  // district progress (left column)
  const distMap={};
  const dcols={'Northern Province':'var(--my)','Eastern Province':'var(--mo)','Southern Province':'var(--accent2)','Western Province':'var(--fo)'};
  VILLAGES.forEach(v=>{
    if(!distMap[v.district])distMap[v.district]={prov:v.province,tgt:0,tot:0};
    distMap[v.district].tgt+=PER_VIL;
    const e=VT[v.id];distMap[v.district].tot+=e.m1+e.f1+e.m2+e.f2;
  });
  document.getElementById('distProg').innerHTML=Object.entries(distMap).map(([d,v])=>{
    const p=Math.round(v.tot/v.tgt*100);
    const col=dcols[v.prov]||'var(--accent)';
    return`<div class="dist-prog-row">
      <div class="dist-prog-hd"><span class="dist-prog-name">${d}</span><span class="dist-prog-nums">${v.tot}/${v.tgt} · ${p}%</span></div>
      <div class="dp-bar"><div class="dp-fill" style="width:${p}%;background:${col}"></div></div>
    </div>`;
  }).join('');
  
  // populate village district selector
  initVilDistSel(distMap);

  // province progress
  const provMap={};
  VILLAGES.forEach(v=>{
    if(!provMap[v.province])provMap[v.province]={tgt:0,tot:0};
    provMap[v.province].tgt+=PER_VIL;
    const e=VT[v.id];provMap[v.province].tot+=e.m1+e.f1+e.m2+e.f2;
  });
  document.getElementById('provProg').innerHTML=Object.entries(provMap).map(([pv,v])=>{
    const p=Math.round(v.tot/v.tgt*100);
    const col=dcols[pv]||'var(--accent)';
    return`<div class="dist-prog-row">
      <div class="dist-prog-hd"><span class="dist-prog-name">${pv.replace(' Province','')}</span><span class="dist-prog-nums">${v.tot}/${v.tgt} · ${p}%</span></div>
      <div class="dp-bar"><div class="dp-fill" style="width:${p}%;background:${col}"></div></div>
    </div>`;
  }).join('');

  // sex chart
  const totM=totM1+totM2,totF=totF1+totF2,totAll=Math.max(1,totM+totF);
  document.getElementById('sexChart').innerHTML=`
    <div class="dist-prog-row"><div class="dist-prog-hd"><span class="dist-prog-name" style="color:var(--my)">Male</span><span class="dist-prog-nums">${totM} (${Math.round(totM/totAll*100)}%)</span></div><div class="dp-bar"><div class="dp-fill" style="width:${Math.round(totM/totAll*100)}%;background:var(--my)"></div></div></div>
    <div class="dist-prog-row"><div class="dist-prog-hd"><span class="dist-prog-name" style="color:var(--fy)">Female</span><span class="dist-prog-nums">${totF} (${Math.round(totF/totAll*100)}%)</span></div><div class="dp-bar"><div class="dp-fill" style="width:${Math.round(totF/totAll*100)}%;background:var(--fy)"></div></div></div>`;

  // activity log
  const logEl=document.getElementById('activityLog');
  logEl.innerHTML=records.length?[...records].reverse().slice(0,20).map(r=>`
    <div class="log-item">
      <div class="log-dot" style="background:${r.status==='completed'?'var(--accent)':r.status==='incomplete'?'var(--accent3)':'var(--accent2)'}"></div>
      <div class="log-time">${r.date}</div>
      <div class="log-txt"><b style="color:var(--accent4)">${r.village}</b> (${r.district}) — ${r.supervisor} — <span style="color:${r.status==='completed'?'var(--accent)':r.status==='incomplete'?'var(--accent3)':'var(--accent2)'}">${r.status}</span> — <b>M:${r.m1+r.m2} F:${r.f1+r.f2} Total:${r.total}</b></div>
    </div>`).join(''):'<div class="empty-msg">No activity yet.</div>';
}

function buildDistList(){
  const distMap={};
  VILLAGES.forEach(v=>{
    if(!distMap[v.district])distMap[v.district]={prov:v.province,tgt:0,tot:0};
    distMap[v.district].tgt+=PER_VIL;
    const e=VT[v.id];distMap[v.district].tot+=e.m1+e.f1+e.m2+e.f2;
  });
  const el=document.getElementById('distList');
  el.innerHTML='';
  // ALL
  const totTgt=160*PER_VIL,totTot=VILLAGES.reduce((a,v)=>{const e=VT[v.id];return a+e.m1+e.f1+e.m2+e.f2;},0);
  const allPct=Math.round(totTot/totTgt*100);
  const allDiv=document.createElement('div');
  allDiv.className='dist-item'+(activeDist==='ALL'?' act':'');
  allDiv.onclick=()=>{activeDist='ALL';buildDistList();refreshAdmin();};
  allDiv.innerHTML=`<div class="dist-prov">All provinces</div><div class="dist-name">All Districts <span style="color:var(--muted);font-weight:400;font-size:10px">(27 districts)</span></div><div class="dist-pr-row"><div class="dist-bar"><div class="dist-fill" style="width:${allPct}%"></div></div><div class="dist-pct">${allPct}%</div></div>`;
  el.appendChild(allDiv);
  const dcols={'Northern Province':'var(--my)','Eastern Province':'var(--mo)','Southern Province':'var(--accent2)','Western Province':'var(--fo)'};
  Object.entries(distMap).forEach(([d,v])=>{
    const p=Math.round(v.tot/v.tgt*100);
    const col=dcols[v.prov]||'var(--accent)';
    const div=document.createElement('div');
    div.className='dist-item'+(activeDist===d?' act':'');
    div.onclick=()=>{activeDist=d;buildDistList();refreshAdmin();};
    div.innerHTML=`<div class="dist-prov">${v.prov.replace(' Province','')}</div><div class="dist-name">${d}</div><div class="dist-pr-row"><div class="dist-bar"><div class="dist-fill" style="width:${p}%;background:${col}"></div></div><div class="dist-pct">${p}%</div></div>`;
    el.appendChild(div);
  });
}

function set(id,v){const e=document.getElementById(id);if(e)e.textContent=v;}
function sw(id,p){const e=document.getElementById(id);if(e)e.style.width=Math.min(100,Math.max(0,p))+'%';}
function copyTxt(btn,txt){navigator.clipboard.writeText(txt).then(()=>{btn.textContent='COPIED';setTimeout(()=>{btn.textContent='COPY';},2000);});}

// ── Village filter helpers ────────────────────────────────────────────────────
function initVilDistSel(distMap){
  const sel=document.getElementById('vil-dist-sel');
  if(!sel) return;
  const cur=sel.value;
  sel.innerHTML='<option value="">Choose a district to see village progress…</option>';
  Object.keys(distMap).sort().forEach(d=>{
    const o=document.createElement('option');o.value=d;o.textContent=d;sel.appendChild(o);
  });
  if(cur) sel.value=cur;
  if(sel.value) onVilDistSel();
}

function onVilDistSel(){
  const dist=document.getElementById('vil-dist-sel').value;
  const title=document.getElementById('vil-prog-title');
  const badge=document.getElementById('vil-prog-badge');
  const list=document.getElementById('vil-prog-list');
  if(!dist){
    title.textContent='🏘 Village progress — select district';
    badge.textContent='—';
    list.innerHTML='<div class="empty-msg">Select a district above.</div>';
    return;
  }
  const vils=VILLAGES.filter(v=>v.district===dist);
  title.textContent='🏘 '+dist;
  badge.textContent=vils.length+' villages';
  const dcols={'Northern Province':'var(--my)','Eastern Province':'var(--mo)','Southern Province':'var(--accent2)','Western Province':'var(--fo)'};
  list.innerHTML=vils.map(v=>{
    const e=VT[v.id],tot=e.m1+e.f1+e.m2+e.f2,pct=Math.round(tot/PER_VIL*100);
    const col=dcols[v.province]||'var(--accent)';
    const icon=tot>=PER_VIL?'✅':tot>0?'🔄':'⏳';
    return`<div style="padding:9px 16px;border-bottom:1px solid rgba(30,45,61,.4)">
      <div style="display:flex;justify-content:space-between;margin-bottom:4px">
        <span style="font-family:'Syne',sans-serif;font-size:12px;font-weight:600">${icon} ${v.village}</span>
        <span style="font-family:'IBM Plex Mono',monospace;font-size:10px;color:var(--muted)">${tot}/${PER_VIL} (${pct}%)</span>
      </div>
      <div style="display:flex;gap:8px;align-items:center">
        <div style="flex:1;height:4px;background:var(--border);border-radius:2px;overflow:hidden">
          <div style="height:100%;width:${pct}%;background:${col};border-radius:2px;transition:width .5s ease"></div>
        </div>
        <span style="font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--muted);width:28px;text-align:right">${pct}%</span>
      </div>
      <div style="display:flex;gap:10px;margin-top:4px;font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--muted)">
        <span style="color:var(--my)">M15: ${e.m1}</span>
        <span style="color:var(--fy)">F15: ${e.f1}</span>
        <span style="color:var(--mo)">M25: ${e.m2}</span>
        <span style="color:var(--fo)">F25: ${e.f2}</span>
      </div>
    </div>`;
  }).join('');
}

function initVillFilters(){
  const ps=document.getElementById('vf-prov');
  if(!ps||ps.children.length>1) return;
  const provs=[...new Set(VILLAGES.map(v=>v.province))].sort();
  provs.forEach(p=>{const o=document.createElement('option');o.value=p;o.textContent=p;ps.appendChild(o);});
}

function onVfProv(){
  const p=document.getElementById('vf-prov').value;
  const dd=document.getElementById('vf-dist');
  dd.innerHTML='<option value="">All districts</option>';
  if(p){
    const dists=[...new Set(VILLAGES.filter(v=>v.province===p).map(v=>v.district))].sort();
    dists.forEach(d=>{const o=document.createElement('option');o.value=d;o.textContent=d;dd.appendChild(o);});
  }
  renderVillTbl();
}

function clearVillFilters(){
  document.getElementById('vf-prov').value='';
  const dd=document.getElementById('vf-dist');
  dd.innerHTML='<option value="">All districts</option>';
  renderVillTbl();
}

function renderVillTbl(){
  initVillFilters();
  const pv=document.getElementById('vf-prov')?document.getElementById('vf-prov').value:'';
  const di=document.getElementById('vf-dist')?document.getElementById('vf-dist').value:'';
  let vils=VILLAGES;
  if(pv) vils=vils.filter(v=>v.province===pv);
  if(di) vils=vils.filter(v=>v.district===di);
  const badge=document.getElementById('vill-badge');
  if(badge) badge.textContent=vils.length+' villages · '+(vils.length*PER_VIL)+' target';
  const dcols={'Northern Province':'var(--my)','Eastern Province':'var(--mo)','Southern Province':'var(--accent2)','Western Province':'var(--fo)'};
  const provIcons={'Northern Province':'🔵','Eastern Province':'🟢','Southern Province':'🔴','Western Province':'🟡'};
  document.getElementById('villTbl').innerHTML=vils.map(v=>{
    const e=VT[v.id],tot=e.m1+e.f1+e.m2+e.f2,rem=Math.max(0,PER_VIL-tot);
    const pct=Math.round(tot/PER_VIL*100);
    const col=dcols[v.province]||'var(--accent)';
    const icon=tot>=PER_VIL?'✅':tot>0?'🔄':'⏳';
    return`<tr>
      <td style="font-weight:500">${icon} ${v.village}</td>
      <td class="td-m">${v.sector}</td><td class="td-m">${v.cell}</td>
      <td>${v.district}</td>
      <td class="td-m">${provIcons[v.province]||''} ${v.province.replace(' Province','')}</td>
      <td class="td-r" style="color:var(--my)">${e.m1}</td>
      <td class="td-r" style="color:var(--fy)">${e.f1}</td>
      <td class="td-r" style="color:var(--mo)">${e.m2}</td>
      <td class="td-r" style="color:var(--fo)">${e.f2}</td>
      <td class="td-r" style="font-weight:600">${tot}</td>
      <td class="td-r td-m">${PER_VIL}</td>
      <td class="td-r" style="color:${rem===0?'var(--accent)':'var(--accent3)'}">${rem}</td>
      <td>
        <div style="display:flex;align-items:center;gap:5px;min-width:80px">
          <div style="flex:1;height:4px;background:var(--border);border-radius:2px;overflow:hidden">
            <div style="height:100%;width:${pct}%;background:${col};border-radius:2px"></div>
          </div>
          <span style="font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--muted);width:26px">${pct}%</span>
        </div>
      </td>
      <td><span class="sts ${tot>=PER_VIL?'s-done':tot>0?'s-prog':'s-pend'}">${tot>=PER_VIL?'✅ DONE':tot>0?'🔄 PROGRESS':'⏳ PENDING'}</span></td>
    </tr>`;
  }).join('');
}

// ── Admin edit / delete / clear ───────────────────────────────────────────────
function openEdit(recId){
  const r=records.find(x=>x.id===recId);
  if(!r)return;
  document.getElementById('edit-id').value=recId;
  document.getElementById('edit-sn').value=r.supervisor;
  document.getElementById('edit-dt').value=r.date;
  document.getElementById('edit-st').value=r.status;
  document.getElementById('edit-vil').value=r.village+' ('+r.district+')';
  document.getElementById('edit-m1').value=r.m1;
  document.getElementById('edit-f1').value=r.f1;
  document.getElementById('edit-m2').value=r.m2;
  document.getElementById('edit-f2').value=r.f2;
  document.getElementById('edit-no').value=r.notes||'';
  document.getElementById('editModal').style.display='flex';
}
function closeEdit(){document.getElementById('editModal').style.display='none';}
function saveEdit(){
  const id=document.getElementById('edit-id').value;
  const idx=records.findIndex(x=>String(x.id)===String(id));
  if(idx<0)return;
  const m1=+document.getElementById('edit-m1').value||0;
  const f1=+document.getElementById('edit-f1').value||0;
  const m2=+document.getElementById('edit-m2').value||0;
  const f2=+document.getElementById('edit-f2').value||0;
  const updated={...records[idx],
    supervisor:document.getElementById('edit-sn').value,
    date:document.getElementById('edit-dt').value,
    status:document.getElementById('edit-st').value,
    m1,f1,m2,f2,total:m1+f1+m2+f2,
    notes:document.getElementById('edit-no').value
  };
  records[idx]=updated;
  rebuildVT();saveLocalFallback();closeEdit();refreshAdmin();
  apiPost({action:'update',record:{'ID':id,...updated}}).then(res=>{
    if(res.ok) showStatus('✅ Record updated in Google Sheets','ok');
    else showStatus('⚠ Updated locally — may not have reached server','err');
  });
}
function deleteRec(recId){
  if(!confirm('Delete this record permanently? This cannot be undone.'))return;
  records=records.filter(x=>x.id!==recId);
  rebuildVT();saveLocalFallback();refreshAdmin();
  apiPost({action:'delete',id:recId}).then(res=>{
    if(res.ok) showStatus('🗑 Record deleted','ok');
    else showStatus('⚠ Delete may not have reached the server','err');
  });
}
function confirmClearAll(){
  if(!confirm('Clear ALL submitted records?\nThis will permanently delete all data from Google Sheets. This cannot be undone.'))return;
  records=[];rebuildVT();saveLocalFallback();refreshAdmin();
  apiPost({action:'clearAll'}).then(res=>{
    if(res.ok) showStatus('🗑 All records cleared','ok');
  });
}
</script>

<!-- Edit modal -->
<div id="editModal" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,.75);z-index:999;align-items:center;justify-content:center">
  <div style="background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:1.5rem;width:520px;max-width:95vw;max-height:90vh;overflow-y:auto">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:1.2rem">
      <div style="font-family:'Syne',sans-serif;font-weight:700;font-size:15px">✏️ Edit Record</div>
      <button onclick="closeEdit()" style="background:transparent;border:1px solid var(--border);color:var(--muted);width:28px;height:28px;border-radius:4px;cursor:pointer;font-size:16px">×</button>
    </div>
    <input type="hidden" id="edit-id" />
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:10px">
      <div style="display:flex;flex-direction:column;gap:4px">
        <label style="font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--muted);text-transform:uppercase;letter-spacing:1.5px">Supervisor</label>
        <select id="edit-sn" style="background:var(--bg);border:1px solid var(--border);color:var(--text);padding:7px 10px;border-radius:4px;font-size:12px;outline:none">
          <option value="Jean Paul Bimenyimana">Jean Paul Bimenyimana</option>
          <option value="Tharcille Niyigena">Tharcille Niyigena</option>
          <option value="Consolateur Byishimo Turikumwe">Consolateur Byishimo Turikumwe</option>
          <option value="Elisa Ngabonziza">Elisa Ngabonziza</option>
          <option value="Emmanuel Nkundineza">Emmanuel Nkundineza</option>
          <option value="Didier Nkurunziza">Didier Nkurunziza</option>
          <option value="Aliane Ikuzwe">Aliane Ikuzwe</option>
          <option value="Jean D'Amour Hagabimana">Jean D'Amour Hagabimana</option>
        </select>
      </div>
      <div style="display:flex;flex-direction:column;gap:4px">
        <label style="font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--muted);text-transform:uppercase;letter-spacing:1.5px">Date</label>
        <input type="date" id="edit-dt" style="background:var(--bg);border:1px solid var(--border);color:var(--text);padding:7px 10px;border-radius:4px;font-size:12px;outline:none;width:100%" />
      </div>
      <div style="display:flex;flex-direction:column;gap:4px">
        <label style="font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--muted);text-transform:uppercase;letter-spacing:1.5px">Status</label>
        <select id="edit-st" style="background:var(--bg);border:1px solid var(--border);color:var(--text);padding:7px 10px;border-radius:4px;font-size:12px;outline:none">
          <option value="completed">Completed</option>
          <option value="incomplete">Incomplete</option>
          <option value="replacement">Replacement</option>
        </select>
      </div>
      <div style="display:flex;flex-direction:column;gap:4px">
        <label style="font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--muted);text-transform:uppercase;letter-spacing:1.5px">Village</label>
        <input id="edit-vil" readonly style="background:var(--surface2);border:1px solid var(--border);color:var(--muted);padding:7px 10px;border-radius:4px;font-size:12px;outline:none;width:100%" />
      </div>
    </div>
    <div style="display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:8px;margin-bottom:10px">
      <div style="display:flex;flex-direction:column;gap:4px"><label style="font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--my);text-transform:uppercase;letter-spacing:1.5px">M 15–24</label><input type="number" id="edit-m1" min="0" style="background:var(--bg);border:1px solid var(--border);color:var(--text);padding:7px 10px;border-radius:4px;font-size:12px;outline:none;width:100%" /></div>
      <div style="display:flex;flex-direction:column;gap:4px"><label style="font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--fy);text-transform:uppercase;letter-spacing:1.5px">F 15–24</label><input type="number" id="edit-f1" min="0" style="background:var(--bg);border:1px solid var(--border);color:var(--text);padding:7px 10px;border-radius:4px;font-size:12px;outline:none;width:100%" /></div>
      <div style="display:flex;flex-direction:column;gap:4px"><label style="font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--mo);text-transform:uppercase;letter-spacing:1.5px">M 25–35</label><input type="number" id="edit-m2" min="0" style="background:var(--bg);border:1px solid var(--border);color:var(--text);padding:7px 10px;border-radius:4px;font-size:12px;outline:none;width:100%" /></div>
      <div style="display:flex;flex-direction:column;gap:4px"><label style="font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--fo);text-transform:uppercase;letter-spacing:1.5px">F 25–35</label><input type="number" id="edit-f2" min="0" style="background:var(--bg);border:1px solid var(--border);color:var(--text);padding:7px 10px;border-radius:4px;font-size:12px;outline:none;width:100%" /></div>
    </div>
    <div style="display:flex;flex-direction:column;gap:4px;margin-bottom:14px">
      <label style="font-family:'IBM Plex Mono',monospace;font-size:9px;color:var(--muted);text-transform:uppercase;letter-spacing:1.5px">Notes</label>
      <textarea id="edit-no" style="background:var(--bg);border:1px solid var(--border);color:var(--text);padding:8px 10px;border-radius:4px;font-size:12px;outline:none;width:100%;height:60px;resize:vertical;font-family:'DM Sans',sans-serif"></textarea>
    </div>
    <div style="display:flex;gap:8px">
      <button onclick="saveEdit()" style="flex:1;height:36px;background:var(--accent);color:#0a0e14;border:none;border-radius:4px;font-family:'Syne',sans-serif;font-weight:700;font-size:11px;letter-spacing:1.5px;cursor:pointer;text-transform:uppercase">Save changes</button>
      <button onclick="closeEdit()" style="height:36px;padding:0 16px;background:transparent;border:1px solid var(--border);color:var(--muted);border-radius:4px;font-family:'DM Sans',sans-serif;font-size:12px;cursor:pointer">Cancel</button>
    </div>
  </div>
</div>

<!-- Setup Instructions Modal -->
<div id="setupModal" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,.85);z-index:9998;align-items:flex-start;justify-content:center;padding:24px;overflow-y:auto">
  <div style="background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:2rem;width:100%;max-width:700px;margin:auto">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:1.5rem">
      <div>
        <div style="font-family:'Syne',sans-serif;font-weight:800;font-size:16px;color:var(--accent)">⚙ Setup Guide — Connect to Google Sheets</div>
        <div style="font-size:12px;color:var(--muted);margin-top:3px">Follow these steps once to make the portal live for all supervisors</div>
      </div>
      <button onclick="document.getElementById('setupModal').style.display='none'" style="background:transparent;border:1px solid var(--border);color:var(--muted);width:28px;height:28px;border-radius:4px;cursor:pointer;font-size:16px">×</button>
    </div>

    <div style="counter-reset:step">

      <div style="margin-bottom:1.25rem;padding:14px 16px;background:var(--bg);border:1px solid var(--border);border-radius:6px;border-left:3px solid var(--accent)">
        <div style="font-family:'Syne',sans-serif;font-weight:700;font-size:13px;color:var(--accent);margin-bottom:6px">Step 1 — Create a Google Sheet</div>
        <div style="font-size:12px;color:var(--text);line-height:1.7">
          Go to <b style="color:var(--accent4)">sheets.google.com</b> and create a new blank spreadsheet.<br>
          Name it: <b>IFPRI Rwanda Youth Survey 2025</b>
        </div>
      </div>

      <div style="margin-bottom:1.25rem;padding:14px 16px;background:var(--bg);border:1px solid var(--border);border-radius:6px;border-left:3px solid var(--accent4)">
        <div style="font-family:'Syne',sans-serif;font-weight:700;font-size:13px;color:var(--accent4);margin-bottom:6px">Step 2 — Open Apps Script</div>
        <div style="font-size:12px;color:var(--text);line-height:1.7">
          In the Google Sheet, click <b>Extensions → Apps Script</b><br>
          Delete all the default code in the editor.
        </div>
      </div>

      <div style="margin-bottom:1.25rem;padding:14px 16px;background:var(--bg);border:1px solid var(--border);border-radius:6px;border-left:3px solid var(--accent3)">
        <div style="font-family:'Syne',sans-serif;font-weight:700;font-size:13px;color:var(--accent3);margin-bottom:6px">Step 3 — Paste the backend script</div>
        <div style="font-size:12px;color:var(--text);line-height:1.7">
          Open the file <b>GoogleAppsScript.js</b> (provided alongside this portal file).<br>
          Copy all of its contents and paste into the Apps Script editor.<br>
          Click the 💾 <b>Save</b> icon (or Ctrl+S).
        </div>
      </div>

      <div style="margin-bottom:1.25rem;padding:14px 16px;background:var(--bg);border:1px solid var(--border);border-radius:6px;border-left:3px solid var(--fy)">
        <div style="font-family:'Syne',sans-serif;font-weight:700;font-size:13px;color:var(--fy);margin-bottom:6px">Step 4 — Deploy as Web App</div>
        <div style="font-size:12px;color:var(--text);line-height:1.7">
          Click <b>Deploy → New deployment</b><br>
          · Type: <b>Web app</b><br>
          · Description: <b>IFPRI Portal Backend</b><br>
          · Execute as: <b>Me (your Google account)</b><br>
          · Who has access: <b>Anyone</b><br>
          Click <b>Deploy</b> → Authorize when prompted → Copy the <b>Web app URL</b>
        </div>
      </div>

      <div style="margin-bottom:1.25rem;padding:14px 16px;background:var(--bg);border:1px solid var(--border);border-radius:6px;border-left:3px solid var(--accent2)">
        <div style="font-family:'Syne',sans-serif;font-weight:700;font-size:13px;color:var(--accent2);margin-bottom:6px">Step 5 — Paste URL into the portal HTML</div>
        <div style="font-size:12px;color:var(--text);line-height:1.7">
          Open <b>IFPRI_Survey_Portal.html</b> in a text editor (Notepad, VS Code, etc.)<br>
          Find this line near the top of the JavaScript section:<br>
          <div style="background:var(--surface2);border:1px solid var(--border);border-radius:4px;padding:8px 12px;margin:6px 0;font-family:'IBM Plex Mono',monospace;font-size:11px;color:var(--accent3)">const SCRIPT_URL = 'YOUR_GOOGLE_APPS_SCRIPT_URL_HERE';</div>
          Replace <b>YOUR_GOOGLE_APPS_SCRIPT_URL_HERE</b> with the URL you copied.<br>
          Save the HTML file.
        </div>
      </div>

      <div style="padding:14px 16px;background:var(--bg);border:1px solid var(--border);border-radius:6px;border-left:3px solid var(--mo)">
        <div style="font-family:'Syne',sans-serif;font-weight:700;font-size:13px;color:var(--mo);margin-bottom:6px">Step 6 — Host and share</div>
        <div style="font-size:12px;color:var(--text);line-height:1.7">
          Go to <b style="color:var(--accent4)">netlify.com/drop</b><br>
          Drag and drop the updated <b>IFPRI_Survey_Portal.html</b> file onto the page.<br>
          You get a live URL instantly — share it with all supervisors.<br>
          <b style="color:var(--accent)">All submissions go directly into your Google Sheet. Admin sees everything in real time.</b>
        </div>
      </div>

    </div>

    <div style="margin-top:1.5rem;padding:12px 16px;background:rgba(0,212,168,.06);border:1px solid rgba(0,212,168,.15);border-radius:6px">
      <div style="font-size:12px;color:var(--muted);line-height:1.7">
        <b style="color:var(--accent)">Total setup time: ~20 minutes.</b> Once done, the portal works for the full duration of data collection.
        The Google Sheet acts as your live database — you can view, filter, and export data to Excel/CSV at any time.
        No monthly fees. No account needed beyond a Google account.
      </div>
    </div>

    <button onclick="document.getElementById('setupModal').style.display='none'" style="width:100%;height:38px;background:var(--accent);color:#0a0e14;border:none;border-radius:5px;font-family:'Syne',sans-serif;font-weight:700;font-size:12px;letter-spacing:1.5px;cursor:pointer;text-transform:uppercase;margin-top:1.25rem">Got it — Close</button>
  </div>
</div>
</body>
</html>
