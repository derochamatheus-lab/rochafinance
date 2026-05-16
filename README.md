[rocha-finance.html](https://github.com/user-attachments/files/27839090/rocha-finance.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rocha Finance</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;0,9..40,600;1,9..40,300&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<link rel="stylesheet" href="https://unpkg.com/@phosphor-icons/web@2.0.3/src/regular/style.css">
<link rel="stylesheet" href="https://unpkg.com/@phosphor-icons/web@2.0.3/src/fill/style.css">

<style>
  :root {
    --bg: #0f0f0e;
    --surface: #181817;
    --surface2: #212120;
    --border: #2a2a28;
    --border2: #323230;
    --text: #f0ede8;
    --text-muted: #7a7870;
    --text-soft: #a8a49e;
    --accent: #c8f55a;
    --accent-dark: #9dc43a;
    --accent-muted: #c8f55a22;
    --red: #ff5a5a;
    --red-muted: #ff5a5a18;
    --green: #5af5a0;
    --green-muted: #5af5a018;
    --gold: #f5c842;
    --radius: 16px;
    --radius-sm: 10px;
    --shadow: 0 4px 24px rgba(0,0,0,0.4);
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ---- LAYOUT ---- */
  .app-shell {
    display: flex;
    height: 100vh;
    overflow: hidden;
  }

  /* ---- SIDEBAR ---- */
  .sidebar {
    width: 240px;
    min-width: 240px;
    background: var(--surface);
    border-right: 1px solid var(--border);
    display: flex;
    flex-direction: column;
    padding: 28px 0 20px;
    gap: 4px;
    transition: width 0.3s ease;
  }

  .sidebar-logo {
    padding: 0 20px 24px;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .logo-mark {
    width: 36px;
    height: 36px;
    background: var(--accent);
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
  }

  .logo-mark span {
    font-family: 'DM Serif Display', serif;
    font-size: 18px;
    color: #0f0f0e;
    font-weight: 400;
    line-height: 1;
  }

  .logo-text {
    font-family: 'DM Serif Display', serif;
    font-size: 17px;
    color: var(--text);
    letter-spacing: -0.3px;
  }

  .logo-text span {
    color: var(--accent);
  }

  .nav-section-label {
    padding: 8px 20px 4px;
    font-size: 10px;
    font-weight: 600;
    letter-spacing: 1.2px;
    text-transform: uppercase;
    color: var(--text-muted);
  }

  .nav-btn {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px 20px;
    cursor: pointer;
    border: none;
    background: none;
    color: var(--text-soft);
    font-size: 14px;
    font-family: 'DM Sans', sans-serif;
    font-weight: 400;
    width: 100%;
    text-align: left;
    border-radius: 0;
    transition: all 0.15s ease;
    position: relative;
  }

  .nav-btn i { font-size: 17px; flex-shrink: 0; }

  .nav-btn:hover {
    color: var(--text);
    background: var(--surface2);
  }

  .nav-btn.active {
    color: var(--accent);
    background: var(--accent-muted);
    font-weight: 500;
  }

  .nav-btn.active::before {
    content: '';
    position: absolute;
    left: 0;
    top: 50%;
    transform: translateY(-50%);
    width: 3px;
    height: 60%;
    background: var(--accent);
    border-radius: 0 3px 3px 0;
  }

  .sidebar-footer {
    margin-top: auto;
    padding: 12px 20px 0;
    border-top: 1px solid var(--border);
  }

  .month-nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 8px 12px;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
  }

  .month-nav button {
    background: none;
    border: none;
    color: var(--text-soft);
    cursor: pointer;
    padding: 4px;
    font-size: 16px;
    display: flex;
    align-items: center;
    transition: color 0.15s;
  }

  .month-nav button:hover { color: var(--accent); }

  #current-month-display {
    font-size: 13px;
    font-weight: 500;
    color: var(--text);
  }

  /* ---- MAIN CONTENT ---- */
  .main {
    flex: 1;
    overflow-y: auto;
    overflow-x: hidden;
    display: flex;
    flex-direction: column;
  }

  .topbar {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 20px 28px;
    border-bottom: 1px solid var(--border);
    background: var(--surface);
    position: sticky;
    top: 0;
    z-index: 10;
    backdrop-filter: blur(12px);
  }

  .topbar-title {
    font-family: 'DM Serif Display', serif;
    font-size: 22px;
    color: var(--text);
    letter-spacing: -0.4px;
  }

  .topbar-actions {
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .btn {
    display: inline-flex;
    align-items: center;
    gap: 7px;
    padding: 9px 16px;
    border-radius: var(--radius-sm);
    font-family: 'DM Sans', sans-serif;
    font-size: 13px;
    font-weight: 500;
    cursor: pointer;
    border: none;
    transition: all 0.15s ease;
  }

  .btn-primary {
    background: var(--accent);
    color: #0f0f0e;
  }

  .btn-primary:hover {
    background: var(--accent-dark);
    transform: translateY(-1px);
  }

  .btn-ghost {
    background: var(--surface2);
    color: var(--text-soft);
    border: 1px solid var(--border);
  }

  .btn-ghost:hover {
    color: var(--text);
    border-color: var(--border2);
  }

  .btn-danger {
    background: var(--red-muted);
    color: var(--red);
    border: 1px solid transparent;
  }

  .btn-danger:hover {
    border-color: var(--red);
  }

  .page-content {
    padding: 28px;
    flex: 1;
  }

  /* ---- TAB CONTENT ---- */
  .tab-content { display: none; }
  .tab-content.active { display: block; }

  /* ---- GRID ---- */
  .grid-3 {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
    margin-bottom: 24px;
  }

  .grid-2 {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
  }

  /* ---- CARDS ---- */
  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 22px;
  }

  .card-label {
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.8px;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 10px;
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .card-value {
    font-family: 'DM Serif Display', serif;
    font-size: 28px;
    color: var(--text);
    letter-spacing: -0.5px;
    line-height: 1.1;
  }

  .card-value.income { color: var(--green); }
  .card-value.expense { color: var(--red); }
  .card-value.negative { color: var(--red); }

  .balance-hero {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 28px 28px 24px;
    margin-bottom: 24px;
    position: relative;
    overflow: hidden;
  }

  .balance-hero::before {
    content: '';
    position: absolute;
    top: -40px;
    right: -40px;
    width: 160px;
    height: 160px;
    background: radial-gradient(circle, var(--accent-muted) 0%, transparent 70%);
    pointer-events: none;
  }

  .balance-hero-label {
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 1px;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 10px;
  }

  .balance-hero-value {
    font-family: 'DM Serif Display', serif;
    font-size: 48px;
    color: var(--text);
    letter-spacing: -1.5px;
    line-height: 1;
  }

  .balance-hero-sub {
    margin-top: 14px;
    display: flex;
    gap: 20px;
  }

  .balance-hero-sub span {
    font-size: 12px;
    color: var(--text-muted);
    display: flex;
    align-items: center;
    gap: 5px;
  }

  .balance-hero-sub i { font-size: 14px; }

  /* ---- CHART ---- */
  .chart-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 22px;
  }

  .chart-title {
    font-size: 13px;
    font-weight: 600;
    color: var(--text-soft);
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .chart-wrapper {
    position: relative;
    height: 220px;
  }

  /* ---- TRANSACTIONS TABLE ---- */
  .tx-table-wrap {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    overflow: hidden;
  }

  .tx-table {
    width: 100%;
    border-collapse: collapse;
  }

  .tx-table thead th {
    padding: 12px 16px;
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.8px;
    text-transform: uppercase;
    color: var(--text-muted);
    text-align: left;
    border-bottom: 1px solid var(--border);
  }

  .tx-table thead th:last-child { text-align: center; }

  .tx-table tbody tr {
    border-bottom: 1px solid var(--border);
    transition: background 0.15s;
  }

  .tx-table tbody tr:last-child { border-bottom: none; }

  .tx-table tbody tr:hover { background: var(--surface2); }

  .tx-table td {
    padding: 13px 16px;
    font-size: 13px;
  }

  .tx-date { color: var(--text-muted); }
  .tx-desc { color: var(--text); font-weight: 500; }

  .cat-badge {
    display: inline-flex;
    align-items: center;
    gap: 5px;
    padding: 3px 9px;
    border-radius: 6px;
    font-size: 11px;
    font-weight: 500;
  }

  .tx-amount {
    text-align: right;
    font-weight: 600;
    font-size: 13px;
    font-variant-numeric: tabular-nums;
  }

  .tx-amount.income { color: var(--green); }
  .tx-amount.expense { color: var(--text); }

  .tx-actions { text-align: center; }

  .icon-btn {
    background: none;
    border: none;
    cursor: pointer;
    color: var(--text-muted);
    padding: 5px;
    border-radius: 6px;
    transition: all 0.15s;
    font-size: 15px;
    display: inline-flex;
    align-items: center;
  }

  .icon-btn:hover { color: var(--red); background: var(--red-muted); }

  /* ---- EMPTY STATE ---- */
  .empty-state {
    padding: 48px;
    text-align: center;
    color: var(--text-muted);
  }

  .empty-state i { font-size: 36px; margin-bottom: 12px; display: block; }
  .empty-state p { font-size: 14px; }

  /* ---- CHAT ---- */
  .chat-wrap {
    display: flex;
    flex-direction: column;
    height: calc(100vh - 130px);
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    overflow: hidden;
  }

  .chat-header {
    padding: 16px 20px;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    gap: 12px;
    background: var(--surface2);
  }

  .chat-avatar {
    width: 36px;
    height: 36px;
    background: var(--accent-muted);
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--accent);
    font-size: 18px;
  }

  .chat-header-text h3 {
    font-size: 14px;
    font-weight: 600;
    color: var(--text);
  }

  .chat-header-text p {
    font-size: 11px;
    color: var(--text-muted);
  }

  .online-dot {
    width: 6px;
    height: 6px;
    background: var(--green);
    border-radius: 50%;
    display: inline-block;
    margin-right: 4px;
    animation: pulse 2s infinite;
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.4; }
  }

  #chat-messages {
    flex: 1;
    overflow-y: auto;
    padding: 20px;
    display: flex;
    flex-direction: column;
    gap: 8px;
    background: var(--bg);
  }

  .msg-user {
    align-self: flex-end;
    max-width: 72%;
  }

  .msg-bot {
    align-self: flex-start;
    max-width: 72%;
  }

  .msg-bubble {
    padding: 10px 14px;
    border-radius: 14px;
    font-size: 13px;
    line-height: 1.5;
    box-shadow: 0 1px 4px rgba(0,0,0,0.3);
  }

  .msg-user .msg-bubble {
    background: var(--accent);
    color: #0f0f0e;
    border-bottom-right-radius: 4px;
    font-weight: 500;
  }

  .msg-bot .msg-bubble {
    background: var(--surface);
    color: var(--text);
    border: 1px solid var(--border);
    border-bottom-left-radius: 4px;
  }

  .msg-time {
    font-size: 10px;
    color: var(--text-muted);
    text-align: right;
    margin-top: 3px;
    padding: 0 4px;
  }

  .msg-user .msg-time { text-align: right; }
  .msg-bot .msg-time { text-align: left; }

  .chat-input-wrap {
    padding: 14px 16px;
    border-top: 1px solid var(--border);
    display: flex;
    gap: 10px;
    align-items: center;
    background: var(--surface2);
  }

  .chat-input {
    flex: 1;
    background: var(--bg);
    border: 1px solid var(--border);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-size: 13px;
    padding: 10px 14px;
    border-radius: 10px;
    outline: none;
    transition: border-color 0.15s;
  }

  .chat-input::placeholder { color: var(--text-muted); }
  .chat-input:focus { border-color: var(--accent); }

  .chat-send-btn {
    width: 38px;
    height: 38px;
    background: var(--accent);
    border: none;
    border-radius: 10px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #0f0f0e;
    font-size: 17px;
    flex-shrink: 0;
    transition: all 0.15s;
  }

  .chat-send-btn:hover {
    background: var(--accent-dark);
    transform: scale(1.05);
  }

  .chat-hint {
    padding: 10px 16px;
    font-size: 11px;
    color: var(--text-muted);
    background: var(--surface2);
    border-top: 1px solid var(--border);
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
  }

  .chat-hint span {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 3px 8px;
    border-radius: 6px;
    cursor: pointer;
    transition: all 0.15s;
    color: var(--text-soft);
  }

  .chat-hint span:hover {
    border-color: var(--accent);
    color: var(--accent);
  }

  /* ---- RECURRING ---- */
  .rec-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 16px 20px;
    border-bottom: 1px solid var(--border);
    transition: background 0.15s;
  }

  .rec-item:last-child { border-bottom: none; }
  .rec-item:hover { background: var(--surface2); }

  .rec-info h4 { font-size: 14px; font-weight: 500; color: var(--text); }
  .rec-info p { font-size: 11px; color: var(--text-muted); margin-top: 3px; }

  .rec-amount {
    font-family: 'DM Serif Display', serif;
    font-size: 18px;
    color: var(--text);
  }

  .rec-amount.income { color: var(--green); }
  .rec-amount.expense { color: var(--red); }

  /* ---- REPORT CARDS ---- */
  .report-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 20px;
  }

  .report-card-title {
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.8px;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 10px;
  }

  .report-card-value {
    font-family: 'DM Serif Display', serif;
    font-size: 26px;
    color: var(--text);
  }

  .report-card-sub {
    font-size: 12px;
    color: var(--text-muted);
    margin-top: 4px;
  }

  /* ---- BUDGET ---- */
  .budget-item {
    display: flex;
    align-items: center;
    gap: 14px;
    padding: 14px 20px;
    border-bottom: 1px solid var(--border);
  }

  .budget-item:last-child { border-bottom: none; }

  .budget-cat-icon {
    width: 34px;
    height: 34px;
    border-radius: 9px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 15px;
    flex-shrink: 0;
  }

  .budget-cat-name {
    font-size: 13px;
    font-weight: 500;
    color: var(--text);
    flex: 1;
  }

  .budget-input-wrap {
    display: flex;
    align-items: center;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 0 12px;
    height: 36px;
    gap: 6px;
  }

  .budget-input-wrap span {
    font-size: 12px;
    color: var(--text-muted);
  }

  .budget-input {
    background: none;
    border: none;
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-size: 13px;
    font-weight: 500;
    width: 80px;
    text-align: right;
    outline: none;
  }

  /* ---- CATEGORIES GRID ---- */
  #categories-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 12px;
  }

  .cat-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 16px;
    display: flex;
    align-items: center;
    gap: 12px;
    transition: border-color 0.15s;
  }

  .cat-card:hover { border-color: var(--border2); }

  .cat-card-icon {
    width: 38px;
    height: 38px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 18px;
    flex-shrink: 0;
  }

  .cat-card-name {
    font-size: 13px;
    font-weight: 500;
    color: var(--text);
  }

  .cat-card-type {
    font-size: 11px;
    color: var(--text-muted);
    margin-top: 1px;
  }

  /* ---- MODALS ---- */
  .modal-overlay {
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.7);
    backdrop-filter: blur(4px);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 100;
  }

  .modal-overlay.hidden { display: none; }

  .modal-box {
    background: var(--surface);
    border: 1px solid var(--border2);
    border-radius: 20px;
    width: 420px;
    max-width: 95vw;
    max-height: 90vh;
    overflow-y: auto;
    box-shadow: var(--shadow);
    animation: modal-in 0.2s ease;
  }

  @keyframes modal-in {
    from { opacity: 0; transform: translateY(12px) scale(0.97); }
    to { opacity: 1; transform: none; }
  }

  .modal-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 22px 24px 16px;
    border-bottom: 1px solid var(--border);
  }

  .modal-title {
    font-family: 'DM Serif Display', serif;
    font-size: 20px;
    color: var(--text);
  }

  .modal-close {
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--text-soft);
    width: 30px;
    height: 30px;
    border-radius: 8px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
    transition: all 0.15s;
  }

  .modal-close:hover { color: var(--text); border-color: var(--border2); }

  .modal-body { padding: 20px 24px 24px; }

  .form-group { margin-bottom: 16px; }

  .form-label {
    display: block;
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.7px;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 7px;
  }

  .form-input, .form-select {
    width: 100%;
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-size: 13px;
    padding: 10px 12px;
    border-radius: 10px;
    outline: none;
    transition: border-color 0.15s;
    -webkit-appearance: none;
  }

  .form-input:focus, .form-select:focus {
    border-color: var(--accent);
  }

  .form-input::placeholder { color: var(--text-muted); }

  .type-toggle {
    display: flex;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 4px;
    gap: 4px;
  }

  .type-toggle button {
    flex: 1;
    padding: 8px;
    border: none;
    border-radius: 7px;
    font-family: 'DM Sans', sans-serif;
    font-size: 12px;
    font-weight: 500;
    cursor: pointer;
    background: none;
    color: var(--text-soft);
    transition: all 0.15s;
  }

  .type-toggle button.active-expense {
    background: var(--red-muted);
    color: var(--red);
  }

  .type-toggle button.active-income {
    background: var(--green-muted);
    color: var(--green);
  }

  .modal-footer {
    display: flex;
    gap: 10px;
    justify-content: flex-end;
    padding: 0 24px 24px;
  }

  /* ---- TOAST ---- */
  #message-box {
    position: fixed;
    bottom: 24px;
    right: 24px;
    background: var(--surface);
    border: 1px solid var(--border2);
    border-radius: var(--radius);
    padding: 14px 18px;
    display: flex;
    align-items: center;
    gap: 12px;
    box-shadow: var(--shadow);
    z-index: 200;
    animation: slide-in 0.3s ease;
    min-width: 260px;
  }

  #message-box.hidden { display: none; }

  @keyframes slide-in {
    from { opacity: 0; transform: translateX(20px); }
    to { opacity: 1; transform: none; }
  }

  .toast-icon {
    width: 32px;
    height: 32px;
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
    flex-shrink: 0;
  }

  .toast-content h4 { font-size: 13px; font-weight: 600; color: var(--text); }
  .toast-content p { font-size: 12px; color: var(--text-muted); margin-top: 1px; }

  /* ---- SCROLLBAR ---- */
  ::-webkit-scrollbar { width: 6px; height: 6px; }
  ::-webkit-scrollbar-track { background: transparent; }
  ::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 3px; }
  ::-webkit-scrollbar-thumb:hover { background: var(--text-muted); }

  /* ---- DIVIDER ---- */
  .section-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 14px;
  }

  .section-title {
    font-size: 13px;
    font-weight: 600;
    color: var(--text-soft);
    display: flex;
    align-items: center;
    gap: 6px;
  }

  /* ---- MOBILE ---- */
  @media (max-width: 768px) {
    .sidebar { display: none; }
    .grid-3 { grid-template-columns: 1fr; }
    .grid-2 { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<div class="app-shell">

  <!-- SIDEBAR -->
  <aside class="sidebar">
    <div class="sidebar-logo">
      <div class="logo-mark"><span>R</span></div>
      <div class="logo-text">Rocha <span>Finance</span></div>
    </div>

    <div class="nav-section-label">Principal</div>
    <button class="nav-btn active" id="nav-dashboard" onclick="appModules.navigation.switchTab('dashboard')">
      <i class="ph ph-squares-four"></i> Visão Geral
    </button>
    <button class="nav-btn" id="nav-transactions" onclick="appModules.navigation.switchTab('transactions')">
      <i class="ph ph-arrows-left-right"></i> Histórico
    </button>
    <button class="nav-btn" id="nav-chat" onclick="appModules.navigation.switchTab('chat')">
      <i class="ph ph-robot"></i> Assistente IA
    </button>

    <div class="nav-section-label" style="margin-top:8px">Gestão</div>
    <button class="nav-btn" id="nav-recurring" onclick="appModules.navigation.switchTab('recurring')">
      <i class="ph ph-repeat"></i> Recorrentes
    </button>
    <button class="nav-btn" id="nav-reports" onclick="appModules.navigation.switchTab('reports')">
      <i class="ph ph-chart-bar"></i> Relatórios
    </button>
    <button class="nav-btn" id="nav-budgets" onclick="appModules.navigation.switchTab('budgets')">
      <i class="ph ph-target"></i> Limites
    </button>
    <button class="nav-btn" id="nav-categories" onclick="appModules.navigation.switchTab('categories')">
      <i class="ph ph-tag"></i> Categorias
    </button>

    <div class="sidebar-footer">
      <div class="month-nav">
        <button onclick="appModules.navigation.changeMonth(-1)"><i class="ph ph-caret-left"></i></button>
        <span id="current-month-display">Maio 2026</span>
        <button onclick="appModules.navigation.changeMonth(1)"><i class="ph ph-caret-right"></i></button>
      </div>
      <button class="nav-btn" style="margin-top:8px;padding-left:0;color:var(--text-muted)" onclick="appModules.auth.logout()">
        <i class="ph ph-sign-out"></i> Sair
      </button>
    </div>
  </aside>

  <!-- MAIN -->
  <main class="main">
    <div class="topbar">
      <h1 class="topbar-title" id="current-view-title">Visão Geral</h1>
      <div class="topbar-actions">
        <button class="btn btn-ghost" onclick="ExportImportModule.exportToCSV(appModules.state.getState().transactions, appModules.state.getState().categories)">
          <i class="ph ph-download-simple"></i> Exportar
        </button>
        <button class="btn btn-primary" onclick="appModules.transactions.openModal()">
          <i class="ph ph-plus"></i> Nova Transação
        </button>
      </div>
    </div>

    <div class="page-content">

      <!-- DASHBOARD -->
      <div id="tab-dashboard" class="tab-content active">
        <div class="balance-hero">
          <div class="balance-hero-label">Saldo do Mês</div>
          <div class="balance-hero-value" id="card-balance">R$ 0,00</div>
          <div class="balance-hero-sub">
            <span style="color:var(--green)"><i class="ph ph-arrow-up-right"></i> <span id="card-income">R$ 0,00</span></span>
            <span style="color:var(--red)"><i class="ph ph-arrow-down-right"></i> <span id="card-expense">R$ 0,00</span></span>
          </div>
        </div>

        <div class="grid-2">
          <div class="chart-card">
            <div class="chart-title"><i class="ph ph-chart-donut"></i> Gastos por Categoria</div>
            <div class="chart-wrapper">
              <canvas id="expensesChart"></canvas>
              <div id="no-chart-data" class="empty-state hidden" style="padding:30px">
                <i class="ph ph-chart-donut" style="font-size:28px"></i>
                <p>Sem gastos no período</p>
              </div>
            </div>
          </div>

          <div class="card" style="display:flex;flex-direction:column;gap:14px">
            <div class="section-title"><i class="ph ph-lightning"></i> Ações Rápidas</div>
            <button class="btn btn-primary" style="width:100%;justify-content:center;padding:12px" onclick="appModules.transactions.openModal()">
              <i class="ph ph-plus-circle"></i> Lançar Transação
            </button>
            <button class="btn btn-ghost" style="width:100%;justify-content:center;padding:12px" onclick="appModules.navigation.switchTab('chat')">
              <i class="ph ph-robot"></i> Usar Assistente IA
            </button>
            <button class="btn btn-ghost" style="width:100%;justify-content:center;padding:12px" onclick="appModules.navigation.switchTab('recurring')">
              <i class="ph ph-repeat"></i> Gerenciar Recorrentes
            </button>
            <button class="btn btn-ghost" style="width:100%;justify-content:center;padding:12px" onclick="appModules.navigation.switchTab('reports')">
              <i class="ph ph-chart-bar"></i> Ver Relatórios
            </button>
          </div>
        </div>
      </div>

      <!-- TRANSACTIONS -->
      <div id="tab-transactions" class="tab-content">
        <div class="tx-table-wrap">
          <table class="tx-table">
            <thead>
              <tr>
                <th>Data</th>
                <th>Descrição</th>
                <th>Categoria</th>
                <th style="text-align:right">Valor</th>
                <th>Ações</th>
              </tr>
            </thead>
            <tbody id="transactions-list"></tbody>
          </table>
          <div id="empty-transactions" class="empty-state hidden">
            <i class="ph ph-receipt"></i>
            <p>Nenhuma transação neste período.</p>
          </div>
        </div>
      </div>

      <!-- CHAT -->
      <div id="tab-chat" class="tab-content">
        <div class="chat-wrap">
          <div class="chat-header">
            <div class="chat-avatar"><i class="ph ph-robot"></i></div>
            <div class="chat-header-text">
              <h3>Assistente Financeiro</h3>
              <p><span class="online-dot"></span>Diga o gasto, eu registro</p>
            </div>
          </div>

          <div id="chat-messages">
            <div class="msg-bot">
              <div class="msg-bubble">
                Olá! Pode me dizer seus gastos em linguagem natural.<br><br>
                Exemplos:<br>
                <em>"Mercado 150"</em><br>
                <em>"Gasolina 80,50"</em><br>
                <em>"Recebi salário 3000"</em>
              </div>
              <div class="msg-time">Agora</div>
            </div>
          </div>

          <div class="chat-hint">
            <span onclick="fillChat('Mercado 150')">Mercado 150</span>
            <span onclick="fillChat('Gasolina 80')">Gasolina 80</span>
            <span onclick="fillChat('Uber 25')">Uber 25</span>
            <span onclick="fillChat('iFood 45')">iFood 45</span>
            <span onclick="fillChat('Recebi salário 5000')">Salário 5000</span>
          </div>

          <div class="chat-input-wrap">
            <input id="chat-input" class="chat-input" placeholder="Ex: Almoço no restaurante 35,00" onkeypress="appModules.chat.handleKeyPress(event)">
            <button class="chat-send-btn" onclick="appModules.chat.sendMessage()">
              <i class="ph ph-paper-plane-tilt"></i>
            </button>
          </div>
        </div>
      </div>

      <!-- RECURRING -->
      <div id="tab-recurring" class="tab-content">
        <div style="display:flex;justify-content:flex-end;margin-bottom:16px">
          <button class="btn btn-primary" onclick="appModules.recurring.openModal()">
            <i class="ph ph-plus"></i> Adicionar Recorrente
          </button>
        </div>
        <div class="tx-table-wrap">
          <div id="recurring-list"></div>
        </div>
      </div>

      <!-- REPORTS -->
      <div id="tab-reports" class="tab-content">
        <div class="grid-3" style="margin-bottom:20px">
          <div class="report-card">
            <div class="report-card-title"><i class="ph ph-trend-down"></i> Total Despesas</div>
            <div class="report-card-value" id="report-avg-expense">R$ 0,00</div>
            <div class="report-card-sub">No mês atual</div>
          </div>
          <div class="report-card">
            <div class="report-card-title"><i class="ph ph-scales"></i> Saldo</div>
            <div class="report-card-value" id="report-forecast">R$ 0,00</div>
            <div class="report-card-sub" id="report-confidence">Entradas - Saídas</div>
          </div>
          <div class="report-card">
            <div class="report-card-title"><i class="ph ph-chart-line-up"></i> Tendência</div>
            <div class="report-card-value" id="report-trend" style="font-size:22px">—</div>
            <div class="report-card-sub">Comparado ao mês anterior</div>
          </div>
        </div>
        <div class="card">
          <div class="section-title" style="margin-bottom:10px"><i class="ph ph-info"></i> Dica</div>
          <p style="font-size:13px;color:var(--text-soft);line-height:1.6">
            Para análises mais detalhadas, exporte seus dados em CSV e use ferramentas como Excel ou Google Sheets para criar seus próprios gráficos e relatórios personalizados.
          </p>
          <button class="btn btn-ghost" style="margin-top:14px" onclick="ExportImportModule.exportToCSV(appModules.state.getState().transactions, appModules.state.getState().categories)">
            <i class="ph ph-download-simple"></i> Exportar CSV
          </button>
        </div>
      </div>

      <!-- BUDGETS -->
      <div id="tab-budgets" class="tab-content">
        <div class="tx-table-wrap" style="margin-bottom:16px">
          <div id="budget-list"></div>
        </div>
        <div style="display:flex;justify-content:flex-end">
          <button class="btn btn-primary" onclick="appModules.budgets.save()">
            <i class="ph ph-floppy-disk"></i> Salvar Limites
          </button>
        </div>
      </div>

      <!-- CATEGORIES -->
      <div id="tab-categories" class="tab-content">
        <div style="display:flex;justify-content:flex-end;margin-bottom:16px">
          <button class="btn btn-primary" onclick="appModules.categories.openModal()">
            <i class="ph ph-plus"></i> Nova Categoria
          </button>
        </div>
        <div id="categories-grid"></div>
      </div>

    </div><!-- /page-content -->
  </main>
</div>

<!-- ============================================================
     MODALS
============================================================ -->

<!-- MODAL: Nova Transação -->
<div id="modal-transaction" class="modal-overlay hidden">
  <div class="modal-box">
    <div class="modal-header">
      <h2 class="modal-title" id="modal-tx-title">Nova Transação</h2>
      <button class="modal-close" onclick="appModules.modals.close('modal-transaction')"><i class="ph ph-x"></i></button>
    </div>
    <div class="modal-body">
      <input type="hidden" id="tx-id">
      <input type="hidden" id="tx-type" value="expense">
      <input type="hidden" id="tx-source" value="manual">

      <div class="form-group">
        <label class="form-label">Tipo</label>
        <div class="type-toggle">
          <button id="btn-type-expense" class="active-expense" onclick="appModules.transactions.setType('expense')">
            <i class="ph ph-arrow-down-right"></i> Saída
          </button>
          <button id="btn-type-income" onclick="appModules.transactions.setType('income')">
            <i class="ph ph-arrow-up-right"></i> Entrada
          </button>
        </div>
      </div>

      <div class="form-group">
        <label class="form-label">Descrição</label>
        <input id="tx-desc" class="form-input" placeholder="Ex: Almoço no trabalho" type="text">
      </div>

      <div style="display:grid;grid-template-columns:1fr 1fr;gap:12px">
        <div class="form-group">
          <label class="form-label">Valor (R$)</label>
          <input id="tx-amount" class="form-input" placeholder="0,00" type="number" min="0.01" step="0.01">
        </div>
        <div class="form-group">
          <label class="form-label">Data</label>
          <input id="tx-date" class="form-input" type="date">
        </div>
      </div>

      <div class="form-group">
        <label class="form-label">Categoria</label>
        <select id="tx-category" class="form-select"></select>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-ghost" onclick="appModules.modals.close('modal-transaction')">Cancelar</button>
      <button class="btn btn-primary" onclick="appModules.transactions.save()">
        <i class="ph ph-check"></i> Salvar
      </button>
    </div>
  </div>
</div>

<!-- MODAL: Recorrente -->
<div id="modal-recurring" class="modal-overlay hidden">
  <div class="modal-box">
    <div class="modal-header">
      <h2 class="modal-title">Nova Recorrente</h2>
      <button class="modal-close" onclick="appModules.modals.close('modal-recurring')"><i class="ph ph-x"></i></button>
    </div>
    <div class="modal-body">
      <div class="form-group">
        <label class="form-label">Descrição</label>
        <input id="rec-desc" class="form-input" placeholder="Ex: Netflix, Aluguel...">
      </div>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:12px">
        <div class="form-group">
          <label class="form-label">Valor</label>
          <input id="rec-amount" class="form-input" placeholder="0,00" type="number" step="0.01">
        </div>
        <div class="form-group">
          <label class="form-label">Frequência</label>
          <select id="rec-freq" class="form-select">
            <option value="weekly">Semanal</option>
            <option value="biweekly">Quinzenal</option>
            <option value="monthly" selected>Mensal</option>
            <option value="quarterly">Trimestral</option>
            <option value="yearly">Anual</option>
          </select>
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Categoria</label>
        <select id="rec-category" class="form-select"></select>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-ghost" onclick="appModules.modals.close('modal-recurring')">Cancelar</button>
      <button class="btn btn-primary" onclick="saveRecurring()">
        <i class="ph ph-check"></i> Salvar
      </button>
    </div>
  </div>
</div>

<!-- MODAL: Categoria -->
<div id="modal-category" class="modal-overlay hidden">
  <div class="modal-box">
    <div class="modal-header">
      <h2 class="modal-title">Nova Categoria</h2>
      <button class="modal-close" onclick="appModules.modals.close('modal-category')"><i class="ph ph-x"></i></button>
    </div>
    <div class="modal-body">
      <div class="form-group">
        <label class="form-label">Nome</label>
        <input id="cat-name" class="form-input" placeholder="Ex: Educação">
      </div>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:12px">
        <div class="form-group">
          <label class="form-label">Tipo</label>
          <select id="cat-type" class="form-select">
            <option value="expense">Saída</option>
            <option value="income">Entrada</option>
          </select>
        </div>
        <div class="form-group">
          <label class="form-label">Cor</label>
          <input id="cat-color" class="form-input" type="color" value="#6366f1" style="padding:4px;height:40px">
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-ghost" onclick="appModules.modals.close('modal-category')">Cancelar</button>
      <button class="btn btn-primary" onclick="saveCategory()">
        <i class="ph ph-check"></i> Salvar
      </button>
    </div>
  </div>
</div>

<!-- TOAST -->
<div id="message-box" class="hidden">
  <div id="toast-icon" class="toast-icon"></div>
  <div class="toast-content">
    <h4 id="msg-title"></h4>
    <p id="msg-text"></p>
  </div>
  <button onclick="appModules.ui.closeMessage()" style="background:none;border:none;color:var(--text-muted);cursor:pointer;margin-left:auto;font-size:16px;display:flex;align-items:center">
    <i class="ph ph-x"></i>
  </button>
</div>

<!-- SCRIPTS -->
<script>
// ============================================================
// 1. STATE MANAGER
// ============================================================
class StateManager {
  constructor() {
    this.state = {
      currentDate: new Date(2026, 4, 15),
      user: null,
      transactions: [],
      recurringTransactions: [],
      categories: [
        { id: 'cat_1', name: 'Alimentação', type: 'expense', color: '#f59e0b', icon: 'ph-hamburger' },
        { id: 'cat_2', name: 'Transporte', type: 'expense', color: '#3b82f6', icon: 'ph-car' },
        { id: 'cat_3', name: 'Moradia', type: 'expense', color: '#8b5cf6', icon: 'ph-house' },
        { id: 'cat_4', name: 'Saúde', type: 'expense', color: '#ef4444', icon: 'ph-first-aid' },
        { id: 'cat_5', name: 'Lazer', type: 'expense', color: '#ec4899', icon: 'ph-popcorn' },
        { id: 'cat_6', name: 'Salário', type: 'income', color: '#10b981', icon: 'ph-money' },
        { id: 'cat_7', name: 'Outros', type: 'expense', color: '#6b7280', icon: 'ph-dots-three' }
      ],
      budgets: {},
      keywordDict: {
        'gasolina': 'cat_2', 'uber': 'cat_2', 'ônibus': 'cat_2', 'combustível': 'cat_2',
        'ifood': 'cat_1', 'mercado': 'cat_1', 'padaria': 'cat_1', 'restaurante': 'cat_1', 'supermercado': 'cat_1',
        'luz': 'cat_3', 'agua': 'cat_3', 'água': 'cat_3', 'aluguel': 'cat_3', 'internet': 'cat_3',
        'farmacia': 'cat_4', 'farmácia': 'cat_4', 'médico': 'cat_4', 'hospital': 'cat_4',
        'cinema': 'cat_5', 'show': 'cat_5', 'bar': 'cat_5', 'viagem': 'cat_5',
        'salario': 'cat_6', 'salário': 'cat_6', 'freela': 'cat_6', 'bônus': 'cat_6'
      }
    };
    this.listeners = [];
  }

  subscribe(cb) { this.listeners.push(cb); }
  setState(updates) {
    this.state = { ...this.state, ...updates };
    this.listeners.forEach(l => l(this.state));
    this.saveToStorage();
  }
  getState() { return this.state; }

  saveToStorage() {
    try {
      const s = { ...this.state, currentDate: this.state.currentDate.toISOString() };
      localStorage.setItem('rocha_finance_v2', JSON.stringify(s));
    } catch(e) {}
  }

  loadFromStorage() {
    try {
      const saved = localStorage.getItem('rocha_finance_v2');
      if (saved) {
        const data = JSON.parse(saved);
        if (data.currentDate) data.currentDate = new Date(data.currentDate);
        this.state = { ...this.state, ...data };
      }
    } catch(e) {}
  }
}

// ============================================================
// 2. UTILITIES
// ============================================================
const Utils = {
  generateId: () => '_' + Math.random().toString(36).substr(2, 9),
  formatCurrency: v => new Intl.NumberFormat('pt-BR', { style: 'currency', currency: 'BRL' }).format(v),
  getMonthYearStr: d => `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}`,
  formatDate: s => { const [y,m,d] = s.split('-'); return `${d}/${m}/${y}`; },
  getCategory: (id, cats) => cats.find(c => c.id === id) || cats[cats.length-1],
};

// ============================================================
// 3. NLP MODULE
// ============================================================
const NLPModule = {
  process(message, state) {
    const lower = message.toLowerCase();
    const valueMatch = lower.match(/(\d+(?:[.,]\d{2})?)/);
    if (!valueMatch) return { success: false, error: "Não consegui identificar o valor. Tente: 'Mercado 150'" };

    let amount = parseFloat(valueMatch[1].replace(',', '.'));
    if (amount <= 0) return { success: false, error: "O valor precisa ser maior que zero." };

    let desc = message.replace(valueMatch[0], '').trim() || "Lançamento via IA";

    let categoryId = null;
    const keywords = Object.keys(state.keywordDict).sort((a,b) => b.length - a.length);
    for (let kw of keywords) {
      if (lower.includes(kw)) { categoryId = state.keywordDict[kw]; break; }
    }

    const isIncome = lower.includes('recebi') || lower.includes('salario') || lower.includes('salário') || lower.includes('venda');
    let type = isIncome ? 'income' : 'expense';

    if (!categoryId) categoryId = isIncome ? state.categories.find(c => c.type === 'income')?.id : 'cat_7';
    else type = Utils.getCategory(categoryId, state.categories).type;

    return { success: true, description: desc.charAt(0).toUpperCase() + desc.slice(1), amount, categoryId, type };
  }
};

// ============================================================
// 4. EXPORT MODULE
// ============================================================
const ExportImportModule = {
  exportToCSV(transactions, categories) {
    let csv = 'Data,Descrição,Categoria,Tipo,Valor\n';
    transactions.forEach(tx => {
      const cat = Utils.getCategory(tx.categoryId, categories);
      const date = Utils.formatDate(tx.date);
      const value = tx.type === 'income' ? tx.amount : -tx.amount;
      csv += `${date},"${tx.description}","${cat.name}","${tx.type}","${value.toFixed(2)}"\n`;
    });
    const a = document.createElement('a');
    a.href = `data:text/csv;charset=utf-8,${encodeURIComponent(csv)}`;
    a.download = 'financeiro.csv';
    a.click();
  }
};

// ============================================================
// 5. RECURRING MODULE
// ============================================================
const RecurringModule = {
  FREQUENCY: { WEEKLY:'weekly', BIWEEKLY:'biweekly', MONTHLY:'monthly', QUARTERLY:'quarterly', YEARLY:'yearly' }
};

// ============================================================
// 6. REPORTS MODULE
// ============================================================
const ReportsModule = {
  generateSummary(transactions, categories, dateStr) {
    const d = dateStr ? new Date(dateStr) : new Date();
    const prefix = Utils.getMonthYearStr(d);
    const txs = transactions.filter(t => t.date.startsWith(prefix));
    let income = 0, expense = 0;
    txs.forEach(tx => { if (tx.type === 'income') income += tx.amount; else expense += tx.amount; });
    return { income, expense, balance: income - expense, transactionCount: txs.length };
  }
};

// ============================================================
// 7. APP MODULES
// ============================================================
const appModules = {
  state: new StateManager(),

  navigation: {
    switchTab(tabId) {
      document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
      const tabEl = document.getElementById(`tab-${tabId}`);
      if (tabEl) tabEl.classList.add('active');

      document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.remove('active'));
      const activeBtn = document.getElementById(`nav-${tabId}`);
      if (activeBtn) activeBtn.classList.add('active');

      const titles = {
        'dashboard':'Visão Geral','transactions':'Histórico','chat':'Assistente IA',
        'recurring':'Recorrentes','reports':'Relatórios','budgets':'Limites','categories':'Categorias'
      };
      const titleEl = document.getElementById('current-view-title');
      if (titleEl) titleEl.innerText = titles[tabId] || 'Rocha Finance';

      if (tabId === 'dashboard') this.renderDashboard();
      if (tabId === 'transactions') this.renderTransactions();
      if (tabId === 'recurring') this.renderRecurring();
      if (tabId === 'reports') this.renderReports();
      if (tabId === 'budgets') this.renderBudgets();
      if (tabId === 'categories') this.renderCategories();
    },

    changeMonth(delta) {
      const state = appModules.state.getState();
      const d = new Date(state.currentDate);
      d.setMonth(d.getMonth() + delta);
      appModules.state.setState({ currentDate: d });
      this.updateMonthDisplay();
      this.renderDashboard();
      this.renderTransactions();
    },

    updateMonthDisplay() {
      const state = appModules.state.getState();
      const months = ['Janeiro','Fevereiro','Março','Abril','Maio','Junho','Julho','Agosto','Setembro','Outubro','Novembro','Dezembro'];
      const el = document.getElementById('current-month-display');
      if (el) el.innerText = `${months[state.currentDate.getMonth()]} ${state.currentDate.getFullYear()}`;
    },

    renderDashboard() {
      const state = appModules.state.getState();
      const prefix = Utils.getMonthYearStr(state.currentDate);
      const txs = state.transactions.filter(t => t.date.startsWith(prefix));

      let income = 0, expense = 0;
      txs.forEach(t => { if (t.type === 'income') income += t.amount; else expense += t.amount; });
      const balance = income - expense;

      const cb = document.getElementById('card-balance');
      if (cb) {
        cb.innerText = Utils.formatCurrency(balance);
        cb.className = 'balance-hero-value' + (balance < 0 ? ' negative' : '');
      }
      const ci = document.getElementById('card-income');
      const ce = document.getElementById('card-expense');
      if (ci) ci.innerText = Utils.formatCurrency(income);
      if (ce) ce.innerText = Utils.formatCurrency(expense);

      const expenses = txs.filter(t => t.type === 'expense');
      const catTotals = {};
      expenses.forEach(tx => { catTotals[tx.categoryId] = (catTotals[tx.categoryId] || 0) + tx.amount; });

      const labels = [], data = [], bgColors = [];
      Object.keys(catTotals).forEach(catId => {
        const cat = Utils.getCategory(catId, state.categories);
        labels.push(cat.name);
        data.push(catTotals[catId]);
        bgColors.push(cat.color);
      });
      this.renderChart(labels, data, bgColors);
    },

    renderChart(labels, data, bgColors) {
      const canvas = document.getElementById('expensesChart');
      const noData = document.getElementById('no-chart-data');
      if (!canvas) return;

      if (data.length === 0) {
        canvas.style.display = 'none';
        if (noData) noData.classList.remove('hidden');
        return;
      }

      canvas.style.display = 'block';
      if (noData) noData.classList.add('hidden');

      if (window.expensesChartInstance) window.expensesChartInstance.destroy();

      const ctx = canvas.getContext('2d');
      window.expensesChartInstance = new Chart(ctx, {
        type: 'doughnut',
        data: { labels, datasets: [{ data, backgroundColor: bgColors, borderWidth: 2, borderColor: '#181817' }] },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          plugins: {
            legend: {
              position: 'right',
              labels: {
                usePointStyle: true,
                font: { family: 'DM Sans', size: 11 },
                color: '#a8a49e',
                boxWidth: 8,
                padding: 12
              }
            }
          },
          cutout: '72%'
        }
      });
    },

    renderTransactions() {
      const state = appModules.state.getState();
      const prefix = Utils.getMonthYearStr(state.currentDate);
      const txs = state.transactions
        .filter(t => t.date.startsWith(prefix))
        .sort((a,b) => new Date(b.date) - new Date(a.date));

      const list = document.getElementById('transactions-list');
      const empty = document.getElementById('empty-transactions');
      if (!list) return;

      list.innerHTML = '';

      if (txs.length === 0) {
        if (empty) empty.classList.remove('hidden');
      } else {
        if (empty) empty.classList.add('hidden');
        txs.forEach(tx => {
          const cat = Utils.getCategory(tx.categoryId, state.categories);
          const isInc = tx.type === 'income';
          const aiIcon = tx.source === 'chat' ? `<i class="ph-fill ph-robot" style="color:var(--accent);font-size:11px;margin-left:4px"></i>` : '';
          list.innerHTML += `
            <tr>
              <td class="tx-date">${Utils.formatDate(tx.date)}</td>
              <td class="tx-desc">${tx.description}${aiIcon}</td>
              <td>
                <span class="cat-badge" style="background:${cat.color}18;color:${cat.color}">
                  <i class="ph ${cat.icon}" style="font-size:12px"></i>${cat.name}
                </span>
              </td>
              <td class="tx-amount ${isInc ? 'income' : 'expense'}">
                ${isInc ? '+' : '-'} ${Utils.formatCurrency(tx.amount)}
              </td>
              <td class="tx-actions">
                <button class="icon-btn" onclick="appModules.transactions.delete('${tx.id}')">
                  <i class="ph ph-trash"></i>
                </button>
              </td>
            </tr>`;
        });
      }
    },

    renderRecurring() {
      const state = appModules.state.getState();
      const list = document.getElementById('recurring-list');
      if (!list) return;
      list.innerHTML = '';

      if (state.recurringTransactions.length === 0) {
        list.innerHTML = '<div class="empty-state"><i class="ph ph-repeat"></i><p>Nenhuma transação recorrente</p></div>';
        return;
      }

      state.recurringTransactions.forEach(rec => {
        const cat = Utils.getCategory(rec.categoryId, state.categories);
        const isInc = rec.type === 'income';
        list.innerHTML += `
          <div class="rec-item">
            <div class="rec-info">
              <h4>${rec.description}</h4>
              <p><i class="ph ph-repeat"></i> ${rec.frequency} &mdash; Próximo: ${Utils.formatDate(rec.nextDate)}</p>
            </div>
            <div style="text-align:right">
              <div class="rec-amount ${isInc ? 'income' : 'expense'}">
                ${isInc ? '+' : '-'}${Utils.formatCurrency(rec.amount)}
              </div>
              <div style="font-size:11px;color:${cat.color};margin-top:2px">${cat.name}</div>
            </div>
          </div>`;
      });
    },

    renderReports() {
      const state = appModules.state.getState();
      const summary = ReportsModule.generateSummary(state.transactions, state.categories, state.currentDate.toISOString());
      const e = (id, val) => { const el = document.getElementById(id); if(el) el.innerText = val; };
      e('report-avg-expense', Utils.formatCurrency(summary.expense));
      e('report-forecast', Utils.formatCurrency(summary.balance));
      e('report-trend', summary.balance > 0 ? '↑ Positivo' : summary.balance < 0 ? '↓ Negativo' : '→ Neutro');
    },

    renderBudgets() {
      const state = appModules.state.getState();
      const list = document.getElementById('budget-list');
      if (!list) return;
      list.innerHTML = '';
      state.categories.filter(c => c.type === 'expense').forEach(cat => {
        const current = state.budgets[cat.id] || 0;
        list.innerHTML += `
          <div class="budget-item">
            <div class="budget-cat-icon" style="background:${cat.color}18;color:${cat.color}">
              <i class="ph ${cat.icon}"></i>
            </div>
            <span class="budget-cat-name">${cat.name}</span>
            <div class="budget-input-wrap">
              <span>R$</span>
              <input type="number" step="10" value="${current}" data-category="${cat.id}" class="budget-input">
            </div>
          </div>`;
      });
    },

    renderCategories() {
      const state = appModules.state.getState();
      const grid = document.getElementById('categories-grid');
      if (!grid) return;
      grid.innerHTML = '';
      state.categories.forEach(cat => {
        grid.innerHTML += `
          <div class="cat-card">
            <div class="cat-card-icon" style="background:${cat.color}20;color:${cat.color}">
              <i class="ph ${cat.icon}"></i>
            </div>
            <div>
              <div class="cat-card-name">${cat.name}</div>
              <div class="cat-card-type">${cat.type === 'expense' ? 'Saída' : 'Entrada'}</div>
            </div>
          </div>`;
      });
    }
  },

  transactions: {
    openModal() {
      document.getElementById('tx-id').value = '';
      document.getElementById('tx-source').value = 'manual';
      document.getElementById('modal-tx-title').innerText = 'Nova Transação';
      const state = appModules.state.getState();
      const todayStr = new Date().toISOString().split('T')[0];
      document.getElementById('tx-date').value = todayStr;
      this.setType('expense');
      document.getElementById('tx-desc').value = '';
      document.getElementById('tx-amount').value = '';
      appModules.modals.open('modal-transaction');
    },

    setType(type) {
      document.getElementById('tx-type').value = type;
      const btnExp = document.getElementById('btn-type-expense');
      const btnInc = document.getElementById('btn-type-income');
      btnExp.className = type === 'expense' ? 'active-expense' : '';
      btnInc.className = type === 'income' ? 'active-income' : '';
      this.populateCategorySelect(type);
    },

    populateCategorySelect(typeFilter = null) {
      const state = appModules.state.getState();
      const select = document.getElementById('tx-category');
      if (!select) return;
      select.innerHTML = '';
      state.categories.forEach(cat => {
        if (typeFilter && cat.type !== typeFilter && cat.id !== 'cat_7') return;
        select.innerHTML += `<option value="${cat.id}">${cat.name}</option>`;
      });
    },

    save() {
      const id = document.getElementById('tx-id').value;
      const desc = document.getElementById('tx-desc').value.trim();
      const amount = parseFloat(document.getElementById('tx-amount').value);
      const date = document.getElementById('tx-date').value;
      const categoryId = document.getElementById('tx-category').value;
      const type = document.getElementById('tx-type').value;
      const source = document.getElementById('tx-source').value;

      if (!desc || !amount || !date || !categoryId) {
        appModules.ui.showMessage('Atenção', 'Preencha todos os campos!', 'error');
        return;
      }

      const state = appModules.state.getState();
      if (id) {
        const idx = state.transactions.findIndex(t => t.id === id);
        if (idx > -1) state.transactions[idx] = { ...state.transactions[idx], description: desc, amount, date, categoryId, type };
      } else {
        state.transactions.push({ id: Utils.generateId(), description: desc, amount, date, categoryId, type, source, createdAt: new Date().toISOString() });
      }

      appModules.state.setState(state);
      appModules.modals.close('modal-transaction');
      appModules.ui.showMessage('Sucesso', 'Transação salva!');
      appModules.navigation.renderDashboard();
      appModules.navigation.renderTransactions();
    },

    delete(id) {
      if (confirm('Tem certeza que deseja excluir?')) {
        const state = appModules.state.getState();
        state.transactions = state.transactions.filter(t => t.id !== id);
        appModules.state.setState(state);
        appModules.ui.showMessage('Sucesso', 'Transação removida!');
        appModules.navigation.renderTransactions();
        appModules.navigation.renderDashboard();
      }
    }
  },

  chat: {
    handleKeyPress(e) { if (e.key === 'Enter') this.sendMessage(); },

    sendMessage() {
      const input = document.getElementById('chat-input');
      const text = input.value.trim();
      if (!text) return;

      this.appendMessage(text, true);
      input.value = '';

      setTimeout(() => {
        const state = appModules.state.getState();
        const result = NLPModule.process(text, state);

        if (result.success) {
          const todayStr = new Date().toISOString().split('T')[0];
          state.transactions.push({
            id: Utils.generateId(),
            description: result.description,
            amount: result.amount,
            date: todayStr,
            categoryId: result.categoryId,
            type: result.type,
            source: 'chat',
            createdAt: new Date().toISOString()
          });
          appModules.state.setState(state);

          const cat = Utils.getCategory(result.categoryId, state.categories);
          this.appendMessage(`✅ <strong>${result.description}</strong><br>${Utils.formatCurrency(result.amount)} &mdash; ${cat.name}<br><small style="color:var(--text-muted)">Errou a categoria? Edite no histórico.</small>`, false);
        } else {
          this.appendMessage(`❌ ${result.error}`, false);
        }
      }, 500);
    },

    appendMessage(text, isUser) {
      const chatArea = document.getElementById('chat-messages');
      if (!chatArea) return;
      const time = new Date().toLocaleTimeString('pt-BR', { hour: '2-digit', minute: '2-digit' });
      chatArea.innerHTML += `
        <div class="${isUser ? 'msg-user' : 'msg-bot'}">
          <div class="msg-bubble">${text}</div>
          <div class="msg-time">${time}</div>
        </div>`;
      chatArea.scrollTop = chatArea.scrollHeight;
    }
  },

  recurring: {
    openModal() {
      const state = appModules.state.getState();
      const select = document.getElementById('rec-category');
      if (select) {
        select.innerHTML = '';
        state.categories.forEach(cat => {
          select.innerHTML += `<option value="${cat.id}">${cat.name}</option>`;
        });
      }
      appModules.modals.open('modal-recurring');
    }
  },

  budgets: {
    save() {
      const state = appModules.state.getState();
      document.querySelectorAll('[data-category]').forEach(input => {
        state.budgets[input.dataset.category] = parseFloat(input.value) || 0;
      });
      appModules.state.setState(state);
      appModules.ui.showMessage('Sucesso', 'Limites salvos!');
    }
  },

  categories: {
    openModal() { appModules.modals.open('modal-category'); }
  },

  modals: {
    open(id) { const m = document.getElementById(id); if (m) m.classList.remove('hidden'); },
    close(id) { const m = document.getElementById(id); if (m) m.classList.add('hidden'); }
  },

  ui: {
    showMessage(title, text, type = 'success') {
      const box = document.getElementById('message-box');
      const icon = document.getElementById('toast-icon');
      if (!box) return;
      document.getElementById('msg-title').innerText = title;
      document.getElementById('msg-text').innerText = text;
      if (icon) {
        icon.style.background = type === 'error' ? 'var(--red-muted)' : 'var(--green-muted)';
        icon.style.color = type === 'error' ? 'var(--red)' : 'var(--green)';
        icon.innerHTML = type === 'error' ? '<i class="ph ph-x-circle"></i>' : '<i class="ph ph-check-circle"></i>';
      }
      box.classList.remove('hidden');
      clearTimeout(this._toastTimer);
      this._toastTimer = setTimeout(() => box.classList.add('hidden'), 3000);
    },
    closeMessage() {
      const box = document.getElementById('message-box');
      if (box) box.classList.add('hidden');
    }
  },

  auth: {
    logout() {
      if (confirm('Deseja sair?')) { localStorage.clear(); location.reload(); }
    }
  }
};

// ---- Helpers ----
function fillChat(text) {
  const input = document.getElementById('chat-input');
  if (input) { input.value = text; input.focus(); }
}

function saveRecurring() {
  const desc = document.getElementById('rec-desc').value.trim();
  const amount = parseFloat(document.getElementById('rec-amount').value);
  const freq = document.getElementById('rec-freq').value;
  const categoryId = document.getElementById('rec-category').value;

  if (!desc || !amount) {
    appModules.ui.showMessage('Atenção', 'Preencha todos os campos!', 'error');
    return;
  }

  const state = appModules.state.getState();
  const cat = Utils.getCategory(categoryId, state.categories);
  const today = new Date().toISOString().split('T')[0];

  state.recurringTransactions.push({
    id: Utils.generateId(),
    description: desc,
    amount,
    frequency: freq,
    categoryId,
    type: cat.type,
    startDate: today,
    nextDate: today,
    active: true
  });

  appModules.state.setState(state);
  appModules.modals.close('modal-recurring');
  appModules.ui.showMessage('Sucesso', 'Recorrente adicionada!');
  appModules.navigation.renderRecurring();
}

function saveCategory() {
  const name = document.getElementById('cat-name').value.trim();
  const type = document.getElementById('cat-type').value;
  const color = document.getElementById('cat-color').value;

  if (!name) {
    appModules.ui.showMessage('Atenção', 'Informe o nome!', 'error');
    return;
  }

  const state = appModules.state.getState();
  state.categories.push({
    id: Utils.generateId(),
    name,
    type,
    color,
    icon: 'ph-tag'
  });

  appModules.state.setState(state);
  appModules.modals.close('modal-category');
  appModules.ui.showMessage('Sucesso', 'Categoria criada!');
  appModules.navigation.renderCategories();
}

// Close modals on overlay click
document.querySelectorAll('.modal-overlay').forEach(overlay => {
  overlay.addEventListener('click', function(e) {
    if (e.target === this) this.classList.add('hidden');
  });
});

// ---- INIT ----
window.addEventListener('DOMContentLoaded', () => {
  appModules.state.loadFromStorage();
  appModules.navigation.updateMonthDisplay();
  appModules.navigation.switchTab('dashboard');
  appModules.transactions.populateCategorySelect();
  console.log('✅ Rocha Finance inicializado!');
});
</script>
</body>
</html>
