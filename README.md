<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>README — WP E-Commerce Automation Stack</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;900&family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet">
<style>
:root {
  --bg:       #030712;
  --surface:  #0a0f1e;
  --panel:    #0d1424;
  --border:   rgba(0,255,180,0.12);
  --border2:  rgba(0,255,180,0.25);
  --green:    #00ffb4;
  --cyan:     #00d4ff;
  --red:      #ff3e6c;
  --gold:     #ffd166;
  --dim:      rgba(0,255,180,0.5);
  --muted:    rgba(200,220,255,0.35);
  --text:     rgba(200,220,255,0.85);
  --font-mono: 'Share Tech Mono', monospace;
  --font-ar:   'Cairo', sans-serif;
  --font-head: 'Orbitron', sans-serif;
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--font-ar);
  overflow-x: hidden;
  min-height: 100vh;
}

/* ── SCANLINES ── */
body::after {
  content: '';
  position: fixed; inset: 0; pointer-events: none; z-index: 1000;
  background: repeating-linear-gradient(
    0deg,
    rgba(0,255,180,0.015) 0px, rgba(0,255,180,0.015) 1px,
    transparent 1px, transparent 3px
  );
  animation: scan 8s linear infinite;
}
@keyframes scan {
  0%   { background-position: 0 0; }
  100% { background-position: 0 100vh; }
}

/* ── GRID BG ── */
body::before {
  content: '';
  position: fixed; inset: 0; pointer-events: none;
  background-image:
    linear-gradient(rgba(0,255,180,0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,255,180,0.03) 1px, transparent 1px);
  background-size: 40px 40px;
}

/* ════════════════════════════════
   TOP BAR
════════════════════════════════ */
.topbar {
  position: fixed; top: 0; left: 0; right: 0; z-index: 500;
  height: 44px;
  background: rgba(3,7,18,0.92);
  backdrop-filter: blur(16px);
  border-bottom: 1px solid var(--border);
  display: flex; align-items: center; padding: 0 32px; gap: 24px;
}

.topbar-dots { display: flex; gap: 7px; }
.td { width: 11px; height: 11px; border-radius: 50%; }
.td1 { background: var(--red); box-shadow: 0 0 8px var(--red); }
.td2 { background: var(--gold); box-shadow: 0 0 8px var(--gold); }
.td3 { background: var(--green); box-shadow: 0 0 8px var(--green); }

.topbar-title {
  font-family: var(--font-mono);
  font-size: 12px; color: var(--green); letter-spacing: 2px;
  flex: 1; text-align: center;
}

.topbar-status {
  display: flex; align-items: center; gap: 8px;
  font-family: var(--font-mono); font-size: 11px; color: var(--green);
}
.pulse-dot {
  width: 7px; height: 7px; border-radius: 50%;
  background: var(--green);
  box-shadow: 0 0 10px var(--green);
  animation: pulse 2s ease-in-out infinite;
}
@keyframes pulse {
  0%,100% { opacity: 1; transform: scale(1); }
  50%      { opacity: 0.4; transform: scale(0.7); }
}

/* ════════════════════════════════
   MAIN WRAPPER
════════════════════════════════ */
.wrapper {
  max-width: 960px;
  margin: 0 auto;
  padding: 72px 24px 80px;
}

/* ════════════════════════════════
   HERO HEADER
════════════════════════════════ */
.hero-header {
  text-align: center;
  padding: 60px 0 40px;
  position: relative;
}

.glitch-title {
  font-family: var(--font-head);
  font-size: clamp(28px, 6vw, 58px);
  font-weight: 900;
  color: var(--green);
  letter-spacing: 4px;
  text-transform: uppercase;
  position: relative;
  display: inline-block;
  animation: titleIn 1s ease both;
  text-shadow:
    0 0 20px rgba(0,255,180,0.5),
    0 0 60px rgba(0,255,180,0.2);
}

.glitch-title::before,
.glitch-title::after {
  content: attr(data-text);
  position: absolute; inset: 0;
  font-family: var(--font-head);
}
.glitch-title::before {
  color: var(--red); clip-path: polygon(0 0, 100% 0, 100% 45%, 0 45%);
  animation: glitch1 4s infinite;
}
.glitch-title::after {
  color: var(--cyan); clip-path: polygon(0 55%, 100% 55%, 100% 100%, 0 100%);
  animation: glitch2 4s infinite;
}
@keyframes glitch1 {
  0%,90%,100% { transform: translate(0); }
  92% { transform: translate(-3px, 1px); }
  94% { transform: translate(3px, -1px); }
  96% { transform: translate(-2px); }
}
@keyframes glitch2 {
  0%,90%,100% { transform: translate(0); }
  92% { transform: translate(3px, -1px); }
  94% { transform: translate(-3px, 1px); }
  96% { transform: translate(2px); }
}
@keyframes titleIn {
  from { opacity: 0; transform: translateY(-30px) scale(0.95); }
  to   { opacity: 1; transform: translateY(0) scale(1); }
}

.hero-sub {
  font-family: var(--font-ar);
  font-size: 15px; color: var(--muted);
  margin-top: 14px; line-height: 1.9;
  animation: fadeIn 1s 0.4s ease both;
}

/* Badges row */
.badges {
  display: flex; flex-wrap: wrap; justify-content: center;
  gap: 10px; margin: 24px 0;
  animation: fadeIn 1s 0.6s ease both;
}
.badge {
  font-family: var(--font-mono);
  font-size: 10px; letter-spacing: 1.5px; text-transform: uppercase;
  padding: 5px 14px; border-radius: 2px;
  border: 1px solid;
  position: relative; overflow: hidden;
  transition: all 0.3s;
}
.badge::before {
  content: ''; position: absolute; inset: 0;
  background: currentColor; opacity: 0.08;
}
.badge:hover { transform: translateY(-2px); }
.badge-g { color: var(--green); border-color: rgba(0,255,180,0.4); }
.badge-c { color: var(--cyan);  border-color: rgba(0,212,255,0.4); }
.badge-r { color: var(--red);   border-color: rgba(255,62,108,0.4); }
.badge-y { color: var(--gold);  border-color: rgba(255,209,102,0.4); }

/* ════════════════════════════════
   SECTION BLOCKS
════════════════════════════════ */
.section {
  margin-top: 48px;
  opacity: 0; transform: translateY(30px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}
.section.visible { opacity: 1; transform: translateY(0); }

.section-header {
  display: flex; align-items: center; gap: 14px;
  margin-bottom: 20px;
}
.section-num {
  font-family: var(--font-mono);
  font-size: 11px; color: var(--green); letter-spacing: 2px;
}
.section-line {
  flex: 1; height: 1px;
  background: linear-gradient(to left, transparent, var(--border2));
}
.section-title {
  font-family: var(--font-head);
  font-size: clamp(14px, 3vw, 20px);
  font-weight: 700; color: var(--green);
  letter-spacing: 3px; text-transform: uppercase;
}

/* ════════════════════════════════
   TERMINAL BLOCK
════════════════════════════════ */
.terminal {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 4px;
  overflow: hidden;
  box-shadow: 0 0 40px rgba(0,255,180,0.05), inset 0 0 40px rgba(0,0,0,0.3);
}
.terminal-bar {
  background: var(--panel);
  padding: 10px 16px;
  border-bottom: 1px solid var(--border);
  display: flex; align-items: center; gap: 10px;
}
.terminal-dots { display: flex; gap: 6px; }
.terminal-dots span { width: 9px; height: 9px; border-radius: 50%; }
.td-r { background: var(--red); }
.td-y { background: var(--gold); }
.td-g { background: var(--green); }
.term-filename {
  font-family: var(--font-mono);
  font-size: 11px; color: var(--muted); margin-right: auto;
}
.terminal-body { padding: 20px 24px; }

.tl {
  font-family: var(--font-mono);
  font-size: 12.5px; line-height: 1.8;
  opacity: 0; transform: translateX(8px);
  transition: opacity 0.4s, transform 0.4s;
  white-space: pre;
}
.tl.show { opacity: 1; transform: translateX(0); }
.tl-prompt { color: var(--green); }
.tl-cmd    { color: var(--cyan); }
.tl-str    { color: var(--gold); }
.tl-comment{ color: rgba(200,220,255,0.25); }
.tl-ok     { color: var(--green); }
.tl-err    { color: var(--red); }
.tl-val    { color: #c792ea; }

/* ════════════════════════════════
   PIPELINE FLOW
════════════════════════════════ */
.pipeline {
  display: flex; align-items: stretch;
  gap: 0; overflow-x: auto;
  padding-bottom: 8px;
}
.pipe-node {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 18px 16px;
  text-align: center;
  min-width: 110px; flex-shrink: 0;
  position: relative;
  transition: all 0.3s;
  opacity: 0;
  animation: nodeIn 0.5s ease forwards;
}
.pipe-node:hover {
  border-color: var(--green);
  box-shadow: 0 0 24px rgba(0,255,180,0.15);
  transform: translateY(-3px);
}
.pipe-icon { font-size: 26px; display: block; margin-bottom: 8px; }
.pipe-name {
  font-family: var(--font-mono);
  font-size: 10px; color: var(--green);
  letter-spacing: 1px; text-transform: uppercase;
}
.pipe-sub { font-size: 10px; color: var(--muted); margin-top: 3px; }

.pipe-arrow {
  display: flex; align-items: center; padding: 0 4px;
  color: var(--green); font-size: 18px;
  opacity: 0;
  animation: arrowIn 0.3s ease forwards;
  flex-shrink: 0;
}
@keyframes nodeIn {
  from { opacity: 0; transform: scale(0.85); }
  to   { opacity: 1; transform: scale(1); }
}
@keyframes arrowIn {
  from { opacity: 0; } to { opacity: 0.4; }
}

/* ════════════════════════════════
   PLUGIN TABLE
════════════════════════════════ */
.ptable {
  width: 100%; border-collapse: collapse;
  font-family: var(--font-mono); font-size: 12px;
  border: 1px solid var(--border); border-radius: 4px; overflow: hidden;
}
.ptable thead { background: var(--panel); }
.ptable th {
  padding: 12px 16px; text-align: right;
  color: var(--green); letter-spacing: 2px; font-size: 10px;
  text-transform: uppercase; border-bottom: 1px solid var(--border);
}
.ptable td {
  padding: 11px 16px; border-bottom: 1px solid rgba(0,255,180,0.05);
  color: var(--text); font-size: 12px;
  transition: background 0.2s;
}
.ptable tr:hover td { background: rgba(0,255,180,0.03); }
.ptable tr:last-child td { border-bottom: none; }

.tag {
  display: inline-block;
  font-size: 9px; letter-spacing: 1px; text-transform: uppercase;
  padding: 2px 8px; border-radius: 2px; border: 1px solid;
  font-family: var(--font-mono);
}
.tag-free { color: var(--green); border-color: rgba(0,255,180,0.3); background: rgba(0,255,180,0.05); }
.tag-paid { color: var(--gold);  border-color: rgba(255,209,102,0.3); background: rgba(255,209,102,0.05); }
.tag-core { color: var(--cyan);  border-color: rgba(0,212,255,0.3); background: rgba(0,212,255,0.05); }

/* ════════════════════════════════
   PAYMENT CARDS
════════════════════════════════ */
.pay-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
}
.pay-country {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 4px; overflow: hidden;
}
.pay-head {
  background: var(--panel);
  padding: 12px 18px;
  border-bottom: 1px solid var(--border);
  font-family: var(--font-head);
  font-size: 12px; letter-spacing: 2px;
  color: var(--cyan);
  display: flex; align-items: center; gap: 10px;
}
.pay-item {
  padding: 12px 18px;
  border-bottom: 1px solid rgba(0,255,180,0.04);
  display: flex; align-items: center; gap: 12px;
  font-family: var(--font-mono); font-size: 12px;
  transition: background 0.2s;
}
.pay-item:hover { background: rgba(0,255,180,0.03); }
.pay-item:last-child { border-bottom: none; }
.pay-dot {
  width: 6px; height: 6px; border-radius: 50%;
  flex-shrink: 0; animation: pulse 2s infinite;
}
.dot-g { background: var(--green); box-shadow: 0 0 6px var(--green); }
.dot-y { background: var(--gold);  box-shadow: 0 0 6px var(--gold); animation-delay: 1s; }
.pay-nm { color: var(--text); flex: 1; }
.pay-note { font-size: 10px; color: var(--muted); }

/* ════════════════════════════════
   COST BLOCK
════════════════════════════════ */
.cost-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 12px;
}
.cost-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 18px 16px;
  position: relative; overflow: hidden;
  transition: all 0.3s;
}
.cost-card::before {
  content: '';
  position: absolute; top: 0; left: 0; right: 0; height: 2px;
  background: var(--green);
  transform: scaleX(0); transform-origin: right;
  transition: transform 0.4s ease;
}
.cost-card:hover::before { transform: scaleX(1); transform-origin: left; }
.cost-card:hover {
  border-color: var(--border2);
  box-shadow: 0 0 20px rgba(0,255,180,0.08);
}
.cost-name {
  font-family: var(--font-mono);
  font-size: 11px; color: var(--muted);
  letter-spacing: 1px; text-transform: uppercase; margin-bottom: 6px;
}
.cost-price {
  font-family: var(--font-head);
  font-size: 20px; font-weight: 700;
}
.cost-period { font-size: 10px; color: var(--muted); margin-top: 2px; }
.price-green { color: var(--green); }
.price-gold  { color: var(--gold); }
.price-free  { color: var(--cyan); }

/* ════════════════════════════════
   RTL CHECKLIST
════════════════════════════════ */
.checklist { list-style: none; }
.checklist li {
  display: flex; align-items: flex-start; gap: 12px;
  padding: 10px 0;
  border-bottom: 1px solid rgba(0,255,180,0.05);
  font-size: 13px; line-height: 1.7;
  opacity: 0; transform: translateX(-10px);
  transition: opacity 0.5s, transform 0.5s;
}
.checklist li.show { opacity: 1; transform: translateX(0); }
.checklist li:last-child { border-bottom: none; }
.check-icon {
  font-family: var(--font-mono);
  font-size: 12px; color: var(--green);
  margin-top: 2px; flex-shrink: 0;
}
.check-key { color: var(--gold); font-weight: 700; margin-left: 4px; }

/* ════════════════════════════════
   LIVE COUNTER STRIP
════════════════════════════════ */
.counter-strip {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1px;
  background: var(--border);
  border: 1px solid var(--border);
  border-radius: 4px;
  overflow: hidden;
  margin: 32px 0;
}
.counter-item {
  background: var(--surface);
  padding: 20px 16px;
  text-align: center;
}
.counter-num {
  font-family: var(--font-head);
  font-size: 28px; font-weight: 900;
  color: var(--green);
  text-shadow: 0 0 16px rgba(0,255,180,0.4);
}
.counter-label {
  font-family: var(--font-mono);
  font-size: 9px; letter-spacing: 2px; color: var(--muted);
  text-transform: uppercase; margin-top: 4px;
}

/* ════════════════════════════════
   SCROLLING TICKER
════════════════════════════════ */
.ticker-wrap {
  overflow: hidden;
  background: var(--panel);
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  padding: 8px 0;
  margin: 40px 0;
}
.ticker-track {
  display: flex; gap: 48px;
  width: max-content;
  animation: ticker 25s linear infinite;
}
.ticker-item {
  font-family: var(--font-mono);
  font-size: 11px; letter-spacing: 2px;
  color: var(--green); text-transform: uppercase;
  white-space: nowrap; display: flex; align-items: center; gap: 8px;
}
.ticker-sep { color: var(--border2); }
@keyframes ticker {
  from { transform: translateX(0); }
  to   { transform: translateX(-50%); }
}

/* ════════════════════════════════
   FOOTER
════════════════════════════════ */
.readme-footer {
  margin-top: 60px;
  padding-top: 32px;
  border-top: 1px solid var(--border);
  text-align: center;
}
.footer-logo {
  font-family: var(--font-head);
  font-size: 18px; letter-spacing: 4px;
  color: var(--green);
  text-shadow: 0 0 20px rgba(0,255,180,0.4);
}
.footer-meta {
  font-family: var(--font-mono);
  font-size: 11px; color: var(--muted);
  margin-top: 12px; line-height: 2;
}
.footer-line {
  height: 1px; margin: 20px auto 0;
  max-width: 200px;
  background: linear-gradient(to right, transparent, var(--green), transparent);
}

/* ════════════════════════════════
   MATRIX RAIN (Canvas)
════════════════════════════════ */
#matrix-canvas {
  position: fixed; top: 0; left: 0;
  width: 100%; height: 100%;
  pointer-events: none; z-index: 0;
  opacity: 0.03;
}

/* ════════════════════════════════
   ANIMATIONS
════════════════════════════════ */
@keyframes fadeIn {
  from { opacity: 0; } to { opacity: 1; }
}

/* Mobile */
@media(max-width: 640px) {
  .pay-grid { grid-template-columns: 1fr; }
  .counter-strip { grid-template-columns: repeat(2,1fr); }
  .pipeline { gap: 2px; }
  .pipe-node { min-width: 80px; padding: 12px 8px; }
  .pipe-icon { font-size: 20px; }
  .glitch-title { letter-spacing: 2px; }
}
</style>
</head>
<body>

<canvas id="matrix-canvas"></canvas>

<!-- TOP BAR -->
<div class="topbar">
  <div class="topbar-dots">
    <div class="td td1"></div>
    <div class="td td2"></div>
    <div class="td td3"></div>
  </div>
  <div class="topbar-title">README.md — WP E-COMMERCE AUTOMATION STACK</div>
  <div class="topbar-status">
    <div class="pulse-dot"></div>
    SYSTEM ONLINE
  </div>
</div>

<div class="wrapper">

  <!-- ══ HERO ══ -->
  <div class="hero-header">
    <div class="glitch-title" data-text="WP AUTOMATION">WP AUTOMATION</div>
    <div class="glitch-title" data-text="STACK" style="color:var(--cyan);text-shadow:0 0 20px rgba(0,212,255,0.5);font-size:clamp(18px,4vw,38px);margin-top:4px;animation-delay:0.2s">STACK</div>

    <div class="hero-sub">
      دليل احترافي شامل لبناء متجر WordPress e-commerce ثنائي اللغة<br>
      عربي / إنجليزي · مصر · الخليج · بعقلية الـ CTO + قوة الـ Automation
    </div>

    <div class="badges">
      <span class="badge badge-g">▸ WordPress</span>
      <span class="badge badge-c">▸ WooCommerce</span>
      <span class="badge badge-r">▸ ERPNext</span>
      <span class="badge badge-y">▸ Full Automation</span>
      <span class="badge badge-g">▸ RTL Support</span>
      <span class="badge badge-c">▸ Multi-Currency</span>
      <span class="badge badge-r">▸ AI-Powered</span>
      <span class="badge badge-y">▸ CTO Mindset</span>
    </div>
  </div>

  <!-- COUNTERS -->
  <div class="counter-strip section">
    <div class="counter-item">
      <div class="counter-num" id="cnt1">0</div>
      <div class="counter-label">Plugins</div>
    </div>
    <div class="counter-item">
      <div class="counter-num" id="cnt2">0</div>
      <div class="counter-label">Gateways</div>
    </div>
    <div class="counter-item">
      <div class="counter-num" id="cnt3">0</div>
      <div class="counter-label">Languages</div>
    </div>
    <div class="counter-item">
      <div class="counter-num" id="cnt4">0</div>
      <div class="counter-label">Auto Steps</div>
    </div>
  </div>

  <!-- TICKER -->
  <div class="ticker-wrap">
    <div class="ticker-track">
      <span class="ticker-item">🟢 WooCommerce <span class="ticker-sep">///</span></span>
      <span class="ticker-item">⚡ Elementor Pro <span class="ticker-sep">///</span></span>
      <span class="ticker-item">🌐 WPML <span class="ticker-sep">///</span></span>
      <span class="ticker-item">🚀 WP Rocket <span class="ticker-sep">///</span></span>
      <span class="ticker-item">💳 Paymob <span class="ticker-sep">///</span></span>
      <span class="ticker-item">🏗️ Flatsome <span class="ticker-sep">///</span></span>
      <span class="ticker-item">⚙️ n8n Automation <span class="ticker-sep">///</span></span>
      <span class="ticker-item">📊 ERPNext <span class="ticker-sep">///</span></span>
      <span class="ticker-item">☁️ Cloudflare CDN <span class="ticker-sep">///</span></span>
      <span class="ticker-item">🔒 Wordfence <span class="ticker-sep">///</span></span>
      <!-- duplicate for seamless loop -->
      <span class="ticker-item">🟢 WooCommerce <span class="ticker-sep">///</span></span>
      <span class="ticker-item">⚡ Elementor Pro <span class="ticker-sep">///</span></span>
      <span class="ticker-item">🌐 WPML <span class="ticker-sep">///</span></span>
      <span class="ticker-item">🚀 WP Rocket <span class="ticker-sep">///</span></span>
      <span class="ticker-item">💳 Paymob <span class="ticker-sep">///</span></span>
      <span class="ticker-item">🏗️ Flatsome <span class="ticker-sep">///</span></span>
      <span class="ticker-item">⚙️ n8n Automation <span class="ticker-sep">///</span></span>
      <span class="ticker-item">📊 ERPNext <span class="ticker-sep">///</span></span>
      <span class="ticker-item">☁️ Cloudflare CDN <span class="ticker-sep">///</span></span>
      <span class="ticker-item">🔒 Wordfence <span class="ticker-sep">///</span></span>
    </div>
  </div>

  <!-- ══ 01 OVERVIEW TERMINAL ══ -->
  <div class="section" id="s1">
    <div class="section-header">
      <span class="section-num">01</span>
      <div class="section-line"></div>
      <h2 class="section-title">Project Overview</h2>
    </div>

    <div class="terminal">
      <div class="terminal-bar">
        <div class="terminal-dots">
          <span class="td-r"></span><span class="td-y"></span><span class="td-g"></span>
        </div>
        <span class="term-filename">~/wp-ecommerce-stack/README.md</span>
      </div>
      <div class="terminal-body" id="term1">
        <div class="tl tl-comment"># ── WordPress E-Commerce Automation Stack ──────────────────────</div>
        <div class="tl"><span class="tl-prompt">$</span> <span class="tl-cmd">cat</span> <span class="tl-str">project.config</span></div>
        <div class="tl tl-comment"></div>
        <div class="tl"><span class="tl-val">PROJECT</span>   : WordPress E-Commerce (AR/EN)</div>
        <div class="tl"><span class="tl-val">MARKETS</span>   : Egypt 🇪🇬 · Saudi Arabia 🇸🇦 · Gulf 🌍</div>
        <div class="tl"><span class="tl-val">STACK</span>     : WordPress + WooCommerce + ERPNext</div>
        <div class="tl"><span class="tl-val">LANGUAGES</span> : Arabic (RTL) + English (LTR)</div>
        <div class="tl"><span class="tl-val">AUTOMATION</span>: n8n + Make + WooCommerce REST API</div>
        <div class="tl"><span class="tl-val">MINDSET</span>   : CTO-Grade Architecture</div>
        <div class="tl tl-comment"></div>
        <div class="tl"><span class="tl-prompt">$</span> <span class="tl-cmd">echo</span> <span class="tl-str">"Stack initialized successfully ✓"</span></div>
        <div class="tl tl-ok">  Stack initialized successfully ✓</div>
        <div class="tl tl-comment"># Ready to deploy ─────────────────────────────────────────────</div>
      </div>
    </div>
  </div>

  <!-- ══ 02 AUTOMATION PIPELINE ══ -->
  <div class="section" id="s2">
    <div class="section-header">
      <span class="section-num">02</span>
      <div class="section-line"></div>
      <h2 class="section-title">Automation Pipeline</h2>
    </div>

    <div class="pipeline" id="pipeline">
      <div class="pipe-node" style="animation-delay:.1s">
        <span class="pipe-icon">🛒</span>
        <div class="pipe-name">WooCommerce</div>
        <div class="pipe-sub">Order Event</div>
      </div>
      <div class="pipe-arrow" style="animation-delay:.2s">→</div>
      <div class="pipe-node" style="animation-delay:.3s">
        <span class="pipe-icon">⚙️</span>
        <div class="pipe-name">n8n / Make</div>
        <div class="pipe-sub">Trigger</div>
      </div>
      <div class="pipe-arrow" style="animation-delay:.4s">→</div>
      <div class="pipe-node" style="animation-delay:.5s">
        <span class="pipe-icon">📊</span>
        <div class="pipe-name">ERPNext</div>
        <div class="pipe-sub">Sync Data</div>
      </div>
      <div class="pipe-arrow" style="animation-delay:.6s">→</div>
      <div class="pipe-node" style="animation-delay:.7s">
        <span class="pipe-icon">📦</span>
        <div class="pipe-name">Inventory</div>
        <div class="pipe-sub">Auto Update</div>
      </div>
      <div class="pipe-arrow" style="animation-delay:.8s">→</div>
      <div class="pipe-node" style="animation-delay:.9s">
        <span class="pipe-icon">💰</span>
        <div class="pipe-name">Accounting</div>
        <div class="pipe-sub">Journal Entry</div>
      </div>
      <div class="pipe-arrow" style="animation-delay:1s">→</div>
      <div class="pipe-node" style="animation-delay:1.1s">
        <span class="pipe-icon">📧</span>
        <div class="pipe-name">Notify</div>
        <div class="pipe-sub">Email / SMS</div>
      </div>
      <div class="pipe-arrow" style="animation-delay:1.2s">→</div>
      <div class="pipe-node" style="animation-delay:1.3s">
        <span class="pipe-icon">📈</span>
        <div class="pipe-name">Analytics</div>
        <div class="pipe-sub">Dashboard</div>
      </div>
    </div>

    <!-- Automation terminal -->
    <div class="terminal" style="margin-top:16px;">
      <div class="terminal-bar">
        <div class="terminal-dots">
          <span class="td-r"></span><span class="td-y"></span><span class="td-g"></span>
        </div>
        <span class="term-filename">~/automation/flows/order-flow.js</span>
      </div>
      <div class="terminal-body" id="term2">
        <div class="tl tl-comment">// WooCommerce → ERPNext Automation Flow</div>
        <div class="tl"><span class="tl-val">const</span> flow = {</div>
        <div class="tl">  trigger  : <span class="tl-str">'woocommerce.order.created'</span>,</div>
        <div class="tl">  steps    : [</div>
        <div class="tl">    <span class="tl-str">'validate_order'</span>,</div>
        <div class="tl">    <span class="tl-str">'sync_erpnext_salesorder'</span>,</div>
        <div class="tl">    <span class="tl-str">'deduct_inventory'</span>,</div>
        <div class="tl">    <span class="tl-str">'create_accounting_entry'</span>,</div>
        <div class="tl">    <span class="tl-str">'send_ar_en_confirmation'</span>,</div>
        <div class="tl">  ],</div>
        <div class="tl">  payment  : <span class="tl-str">'paymob | moyasar | tap'</span>,</div>
        <div class="tl">  currency : <span class="tl-str">'EGP | SAR | AED | USD'</span>,</div>
        <div class="tl">};</div>
        <div class="tl tl-comment"></div>
        <div class="tl"><span class="tl-prompt">▶</span> <span class="tl-ok">Flow registered. Listening for events...</span></div>
      </div>
    </div>
  </div>

  <!-- ══ 03 PLUGINS TABLE ══ -->
  <div class="section" id="s3">
    <div class="section-header">
      <span class="section-num">03</span>
      <div class="section-line"></div>
      <h2 class="section-title">Essential Plugins</h2>
    </div>

    <table class="ptable">
      <thead>
        <tr>
          <th>#</th>
          <th>Plugin</th>
          <th>الوظيفة</th>
          <th>النوع</th>
          <th>السعر</th>
        </tr>
      </thead>
      <tbody>
        <tr><td>01</td><td>WooCommerce</td><td>المتجر الأساسي</td><td><span class="tag tag-core">CORE</span></td><td style="color:var(--cyan)">Free</td></tr>
        <tr><td>02</td><td>Flatsome Theme</td><td>قالب متجر احترافي</td><td><span class="tag tag-paid">PAID</span></td><td style="color:var(--gold)">$59 once</td></tr>
        <tr><td>03</td><td>Elementor Pro</td><td>Page Builder متقدم</td><td><span class="tag tag-paid">PAID</span></td><td style="color:var(--gold)">$59/yr</td></tr>
        <tr><td>04</td><td>WPML</td><td>ثنائية اللغة AR/EN</td><td><span class="tag tag-paid">PAID</span></td><td style="color:var(--gold)">$99/yr</td></tr>
        <tr><td>05</td><td>WP Rocket</td><td>Cache & Performance</td><td><span class="tag tag-paid">PAID</span></td><td style="color:var(--gold)">$59/yr</td></tr>
        <tr><td>06</td><td>Yoast SEO</td><td>تحسين محركات البحث</td><td><span class="tag tag-free">FREE</span></td><td style="color:var(--green)">Free</td></tr>
        <tr><td>07</td><td>Wordfence</td><td>الحماية والأمان</td><td><span class="tag tag-free">FREE</span></td><td style="color:var(--green)">Free</td></tr>
        <tr><td>08</td><td>ShortPixel</td><td>ضغط وتحسين الصور</td><td><span class="tag tag-paid">PAID</span></td><td style="color:var(--gold)">$4.99/mo</td></tr>
        <tr><td>09</td><td>Dokan Multivendor</td><td>Multi-Vendor Marketplace</td><td><span class="tag tag-free">FREE</span></td><td style="color:var(--green)">Free</td></tr>
        <tr><td>10</td><td>MailPoet</td><td>Email Marketing</td><td><span class="tag tag-free">FREE</span></td><td style="color:var(--green)">Free</td></tr>
        <tr><td>11</td><td>UpdraftPlus Pro</td><td>نسخ احتياطي تلقائي</td><td><span class="tag tag-paid">PAID</span></td><td style="color:var(--gold)">$70/yr</td></tr>
        <tr><td>12</td><td>Currency Switcher Pro</td><td>عملات متعددة EGP/SAR</td><td><span class="tag tag-paid">PAID</span></td><td style="color:var(--gold)">$29/yr</td></tr>
      </tbody>
    </table>
  </div>

  <!-- ══ 04 PAYMENT GATEWAYS ══ -->
  <div class="section" id="s4">
    <div class="section-header">
      <span class="section-num">04</span>
      <div class="section-line"></div>
      <h2 class="section-title">Payment Gateways</h2>
    </div>

    <div class="pay-grid">
      <div class="pay-country">
        <div class="pay-head">🇪🇬 السوق المصري</div>
        <div class="pay-item"><span class="pay-dot dot-g"></span><div><div class="pay-nm">Paymob (Accept)</div><div class="pay-note">بطاقات + محافظ + فاتورة</div></div><span class="tag tag-free">FREE</span></div>
        <div class="pay-item"><span class="pay-dot dot-g"></span><div><div class="pay-nm">Fawry</div><div class="pay-note">الأكثر انتشاراً في مصر</div></div><span class="tag tag-free">FREE</span></div>
        <div class="pay-item"><span class="pay-dot dot-y"></span><div><div class="pay-nm">Kashier</div><div class="pay-note">واجهة عربية + 3DS</div></div><span class="tag tag-paid">COM%</span></div>
        <div class="pay-item"><span class="pay-dot dot-y"></span><div><div class="pay-nm">PayTabs</div><div class="pay-note">مصر + الخليج معاً</div></div><span class="tag tag-paid">COM%</span></div>
      </div>
      <div class="pay-country">
        <div class="pay-head">🇸🇦 السوق الخليجي</div>
        <div class="pay-item"><span class="pay-dot dot-g"></span><div><div class="pay-nm">Moyasar</div><div class="pay-note">الأفضل في السعودية + Mada</div></div><span class="tag tag-free">FREE</span></div>
        <div class="pay-item"><span class="pay-dot dot-g"></span><div><div class="pay-nm">Tap Payments</div><div class="pay-note">STC Pay + Visa + كل الخليج</div></div><span class="tag tag-free">FREE</span></div>
        <div class="pay-item"><span class="pay-dot dot-y"></span><div><div class="pay-nm">HyperPay</div><div class="pay-note">Enterprise · مشاريع كبيرة</div></div><span class="tag tag-paid">ENT</span></div>
        <div class="pay-item"><span class="pay-dot dot-y"></span><div><div class="pay-nm">Stripe (via agent)</div><div class="pay-note">بطاقات دولية عبر وسيط</div></div><span class="tag tag-paid">2.9%</span></div>
      </div>
    </div>
  </div>

  <!-- ══ 05 RTL CHECKLIST ══ -->
  <div class="section" id="s5">
    <div class="section-header">
      <span class="section-num">05</span>
      <div class="section-line"></div>
      <h2 class="section-title">RTL & Arabic Support</h2>
    </div>

    <ul class="checklist" id="checklist">
      <li><span class="check-icon">[✓]</span><div>استخدم خطوط<span class="check-key">Cairo / Tajawal</span>من Google Fonts — دعم RTL نيتف وتبدو احترافية</div></li>
      <li><span class="check-icon">[✓]</span><div>فعّل<span class="check-key">WPML + WooCommerce Multilingual</span>لترجمة المنتجات، الكاتيجوريز، والإيميلات</div></li>
      <li><span class="check-icon">[✓]</span><div>اختبر الـ Checkout كاملاً بـ<span class="check-key">RTL Tester Plugin</span>— Cart, Checkout, My Account</div></li>
      <li><span class="check-icon">[✓]</span><div>استخدم<span class="check-key">Currency Switcher Pro</span>لعرض EGP/SAR/AED تلقائياً حسب موقع الزائر</div></li>
      <li><span class="check-icon">[✓]</span><div>خصص قوالب الإيميل بـ<span class="check-key">Email Customizer for WooCommerce</span>عربي + إنجليزي</div></li>
      <li><span class="check-icon">[✓]</span><div>تأكد أن الـ Theme يدعم<span class="check-key">RTL بشكل نيتف</span>— Flatsome وAstra Pro الأفضل</div></li>
    </ul>
  </div>

  <!-- ══ 06 COST BREAKDOWN ══ -->
  <div class="section" id="s6">
    <div class="section-header">
      <span class="section-num">06</span>
      <div class="section-line"></div>
      <h2 class="section-title">Stack Cost Breakdown</h2>
    </div>

    <div class="cost-grid">
      <div class="cost-card"><div class="cost-name">Hosting (Cloudways)</div><div class="cost-price price-gold">$14<span style="font-size:12px">/mo</span></div><div class="cost-period">DigitalOcean · مستحسن</div></div>
      <div class="cost-card"><div class="cost-name">Flatsome Theme</div><div class="cost-price price-gold">$59<span style="font-size:12px"> once</span></div><div class="cost-period">مرة واحدة · Updates مجاناً</div></div>
      <div class="cost-card"><div class="cost-name">Elementor Pro</div><div class="cost-price price-gold">$59<span style="font-size:12px">/yr</span></div><div class="cost-period">Page Builder متكامل</div></div>
      <div class="cost-card"><div class="cost-name">WPML</div><div class="cost-price price-gold">$99<span style="font-size:12px">/yr</span></div><div class="cost-period">ثنائية اللغة الكاملة</div></div>
      <div class="cost-card"><div class="cost-name">WP Rocket</div><div class="cost-price price-gold">$59<span style="font-size:12px">/yr</span></div><div class="cost-period">أسرع Cache Plugin</div></div>
      <div class="cost-card"><div class="cost-name">ShortPixel</div><div class="cost-price price-gold">$4.99<span style="font-size:12px">/mo</span></div><div class="cost-period">ضغط صور تلقائي</div></div>
      <div class="cost-card"><div class="cost-name">WooCommerce</div><div class="cost-price price-free">FREE</div><div class="cost-period">Core E-Commerce</div></div>
      <div class="cost-card"><div class="cost-name">Cloudflare CDN</div><div class="cost-price price-free">FREE</div><div class="cost-period">CDN + DDoS Protection</div></div>
      <div class="cost-card"><div class="cost-name">Wordfence + Yoast</div><div class="cost-price price-free">FREE</div><div class="cost-period">Security + SEO</div></div>
      <div class="cost-card"><div class="cost-name">Payment Gateways</div><div class="cost-price price-free">FREE</div><div class="cost-period">Paymob · Moyasar · Tap</div></div>
    </div>

    <!-- Cost terminal -->
    <div class="terminal" style="margin-top:20px;">
      <div class="terminal-bar">
        <div class="terminal-dots"><span class="td-r"></span><span class="td-y"></span><span class="td-g"></span></div>
        <span class="term-filename">~/scripts/calculate-cost.sh</span>
      </div>
      <div class="terminal-body" id="term3">
        <div class="tl tl-comment">#!/bin/bash  # Stack Cost Calculator</div>
        <div class="tl"><span class="tl-prompt">$</span> ./calculate_stack_cost.sh</div>
        <div class="tl tl-comment"></div>
        <div class="tl">  Year 1 (one-time)  : <span class="tl-val">$59</span>   (Flatsome)</div>
        <div class="tl">  Annual plugins     : <span class="tl-val">$217</span>  (Elementor + WPML + Rocket)</div>
        <div class="tl">  Hosting (12mo)     : <span class="tl-val">$168</span>  ($14/mo × 12)</div>
        <div class="tl">  Images (12mo)      : <span class="tl-val">$60</span>   ($4.99/mo × 12)</div>
        <div class="tl">                       ───────</div>
        <div class="tl">  YEAR 1 TOTAL       : <span class="tl-ok">~$504</span></div>
        <div class="tl">  YEAR 2+ (annual)   : <span class="tl-ok">~$445</span>  (no Flatsome)</div>
        <div class="tl tl-comment"></div>
        <div class="tl"><span class="tl-ok">✓ Cost-efficient for production-grade bilingual e-commerce</span></div>
      </div>
    </div>
  </div>

  <!-- ══ 07 QUICK START ══ -->
  <div class="section" id="s7">
    <div class="section-header">
      <span class="section-num">07</span>
      <div class="section-line"></div>
      <h2 class="section-title">Quick Start</h2>
    </div>

    <div class="terminal">
      <div class="terminal-bar">
        <div class="terminal-dots"><span class="td-r"></span><span class="td-y"></span><span class="td-g"></span></div>
        <span class="term-filename">~/setup/quick-start.sh</span>
      </div>
      <div class="terminal-body" id="term4">
        <div class="tl tl-comment">#!/bin/bash</div>
        <div class="tl tl-comment"># Step 1: Provision server on Cloudways (DigitalOcean)</div>
        <div class="tl"><span class="tl-prompt">$</span> <span class="tl-cmd">cloudways</span> server:create --app wordpress --size 2GB</div>
        <div class="tl tl-ok">  ✓ Server provisioned at 165.xxx.xxx.xxx</div>
        <div class="tl tl-comment"></div>
        <div class="tl tl-comment"># Step 2: Install WooCommerce + Flatsome</div>
        <div class="tl"><span class="tl-prompt">$</span> <span class="tl-cmd">wp</span> plugin install woocommerce --activate</div>
        <div class="tl tl-ok">  ✓ WooCommerce installed & activated</div>
        <div class="tl"><span class="tl-prompt">$</span> <span class="tl-cmd">wp</span> theme install flatsome --activate</div>
        <div class="tl tl-ok">  ✓ Flatsome theme active</div>
        <div class="tl tl-comment"></div>
        <div class="tl tl-comment"># Step 3: Enable RTL + Arabic</div>
        <div class="tl"><span class="tl-prompt">$</span> <span class="tl-cmd">wp</span> language core install ar --activate</div>
        <div class="tl tl-ok">  ✓ Arabic language enabled (RTL)</div>
        <div class="tl tl-comment"></div>
        <div class="tl tl-comment"># Step 4: Connect ERPNext via REST API</div>
        <div class="tl"><span class="tl-prompt">$</span> <span class="tl-cmd">curl</span> -X POST <span class="tl-str">https://erp.yourdomain.com/api/resource/Sales Order</span> \</div>
        <div class="tl">       -H <span class="tl-str">"Authorization: token key:secret"</span> \</div>
        <div class="tl">       -d <span class="tl-str">'{"doctype":"Sales Order","customer":"WC-001"}'</span></div>
        <div class="tl tl-ok">  ✓ ERPNext sync established</div>
        <div class="tl tl-comment"></div>
        <div class="tl"><span class="tl-prompt">▶</span> <span class="tl-ok">All systems GO. Store is live 🚀</span></div>
      </div>
    </div>
  </div>

  <!-- FOOTER -->
  <div class="readme-footer section">
    <div class="footer-logo">WP · AUTOMATION · STACK</div>
    <div class="footer-meta">
      Crafted with CTO Mindset · Full Stack Developer · ERPNext Expert<br>
      Egypt 🇪🇬 · Saudi Arabia 🇸🇦 · Gulf Region 🌍<br>
      <span style="color:var(--green)">WordPress + WooCommerce + ERPNext + n8n + Cloudflare</span>
    </div>
    <div class="footer-line"></div>
    <div style="font-family:var(--font-mono);font-size:10px;color:var(--muted);margin-top:14px;letter-spacing:2px;">
      README v2.0 · 2025 · MIT LICENSE
    </div>
  </div>

</div><!-- /wrapper -->

<script>
/* ── Matrix Rain ── */
const canvas = document.getElementById('matrix-canvas');
const ctx = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
const cols = Math.floor(canvas.width / 18);
const drops = Array(cols).fill(1);
const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@#$%ﺍﺏﺕﺙﺝﺡﺥﺩﺫﺭﺯﺱﺵﺹﺽﻁﻅﻉﻏ';

function drawMatrix() {
  ctx.fillStyle = 'rgba(3,7,18,0.05)';
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  ctx.fillStyle = '#00ffb4';
  ctx.font = '13px Share Tech Mono';
  drops.forEach((y, i) => {
    const ch = chars[Math.floor(Math.random() * chars.length)];
    ctx.fillText(ch, i * 18, y * 18);
    if (y * 18 > canvas.height && Math.random() > 0.975) drops[i] = 0;
    drops[i]++;
  });
}
setInterval(drawMatrix, 60);
window.addEventListener('resize', () => {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
});

/* ── Scroll Reveal ── */
const sections = document.querySelectorAll('.section');
const revealObs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
      revealObs.unobserve(e.target);
    }
  });
}, { threshold: 0.1 });
sections.forEach(s => revealObs.observe(s));

/* ── Terminal Typewriter ── */
function animateTerm(id, delay = 0) {
  const lines = document.querySelectorAll(`#${id} .tl`);
  lines.forEach((line, i) => {
    setTimeout(() => line.classList.add('show'), delay + i * 70);
  });
}

const termObs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      const id = e.target.id;
      if (id === 'term1') animateTerm('term1');
      if (id === 'term2') animateTerm('term2');
      if (id === 'term3') animateTerm('term3');
      if (id === 'term4') animateTerm('term4');
      termObs.unobserve(e.target);
    }
  });
}, { threshold: 0.2 });
['term1','term2','term3','term4'].forEach(id => {
  const el = document.getElementById(id);
  if (el) termObs.observe(el);
});

/* ── Checklist animation ── */
const clObs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      const items = e.target.querySelectorAll('li');
      items.forEach((li, i) => setTimeout(() => li.classList.add('show'), i * 120));
      clObs.unobserve(e.target);
    }
  });
}, { threshold: 0.2 });
const cl = document.getElementById('checklist');
if (cl) clObs.observe(cl);

/* ── Counters ── */
function animateCounter(el, target, duration = 1800) {
  let start = 0;
  const step = Math.ceil(target / (duration / 30));
  const interval = setInterval(() => {
    start = Math.min(start + step, target);
    el.textContent = start;
    if (start >= target) clearInterval(interval);
  }, 30);
}

const cntObs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      animateCounter(document.getElementById('cnt1'), 12);
      animateCounter(document.getElementById('cnt2'), 8);
      animateCounter(document.getElementById('cnt3'), 2);
      animateCounter(document.getElementById('cnt4'), 7);
      cntObs.unobserve(e.target);
    }
  });
}, { threshold: 0.5 });
const strip = document.querySelector('.counter-strip');
if (strip) cntObs.observe(strip);

/* ── Pipeline nodes ── */
const pipeObs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.querySelectorAll('.pipe-node, .pipe-arrow').forEach(el => {
        const delay = parseFloat(el.style.animationDelay || '0') * 1000;
        setTimeout(() => el.style.animationPlayState = 'running', delay);
      });
      pipeObs.unobserve(e.target);
    }
  });
}, { threshold: 0.3 });
const pipe = document.getElementById('pipeline');
if (pipe) pipeObs.observe(pipe);

/* ── Glitch hover on title ── */
document.querySelectorAll('.glitch-title').forEach(el => {
  el.addEventListener('mouseenter', () => {
    el.style.animation = 'glitch1 0.3s infinite';
  });
  el.addEventListener('mouseleave', () => {
    el.style.animation = '';
  });
});
</script>
</body>
</html>

