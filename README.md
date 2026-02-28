<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nuñez Saving Vault</title>
<link href="https://fonts.googleapis.com/css2?family=Sora:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root {
  --navy: #0a1628;
  --navy-mid: #0f2044;
  --navy-light: #1a3260;
  --blue: #1e5fc4;
  --blue-bright: #2d7aff;
  --blue-glow: #4d9fff;
  --teal: #00c9b1;
  --gold: #f5a623;
  --gold-light: #ffd166;
  --white: #f8faff;
  --gray-100: #eef2f9;
  --gray-200: #d0daea;
  --gray-400: #7a8fb5;
  --gray-600: #4a5a7e;
  --red: #e53e3e;
  --green: #00b894;
  --green-light: #55efc4;
  --sidebar-w: 260px;
  --radius: 14px;
  --shadow: 0 4px 24px rgba(0,0,0,0.18);
  --transition: all 0.22s cubic-bezier(0.4,0,0.2,1);
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

.badge-corrected {
  background: rgba(245,166,35,0.18);
  color: var(--gold-light);
  border: 1px solid rgba(245,166,35,0.4);
  font-size: 9.5px;
  padding: 2px 7px;
  border-radius: 5px;
  font-weight: 700;
  letter-spacing: 0.5px;
  margin-left: 6px;
  text-transform: uppercase;
}
tr.corrected-row { background: rgba(245,166,35,0.04) !important; }

.stat-card.cash {
  background: linear-gradient(135deg, rgba(0,201,177,0.18) 0%, rgba(45,122,255,0.12) 100%);
  border: 1.5px solid rgba(0,201,177,0.35);
}
.stat-card.cash .stat-value { color: var(--teal); }

.form-note {
  font-size: 11px;
  color: var(--teal);
  margin-top: 5px;
  font-style: italic;
}

body {
  font-family: 'Sora', sans-serif;
  background: var(--navy);
  color: var(--white);
  min-height: 100vh;
  display: flex;
  overflow-x: hidden;
  overflow-y: auto;
}

#sidebar {
  width: var(--sidebar-w);
  min-height: 100vh;
  background: linear-gradient(180deg, var(--navy-mid) 0%, var(--navy) 100%);
  border-right: 1px solid rgba(255,255,255,0.06);
  display: flex;
  flex-direction: column;
  position: fixed;
  left: 0; top: 0; bottom: 0;
  z-index: 100;
  transition: var(--transition);
}

.sidebar-logo {
  padding: 28px 24px 20px;
  border-bottom: 1px solid rgba(255,255,255,0.07);
}
.logo-icon {
  width: 46px; height: 46px;
  background: linear-gradient(135deg, var(--blue-bright), var(--teal));
  border-radius: 12px;
  display: flex; align-items: center; justify-content: center;
  font-size: 22px;
  margin-bottom: 10px;
  box-shadow: 0 4px 18px rgba(45,122,255,0.4);
}
.logo-name {
  font-size: 16px;
  font-weight: 700;
  color: var(--white);
  letter-spacing: -0.3px;
  line-height: 1.2;
}
.logo-sub {
  font-size: 10px;
  color: var(--gray-400);
  font-weight: 500;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  margin-top: 2px;
}

nav { flex: 1; padding: 16px 12px; overflow-y: auto; }

.nav-section-label {
  font-size: 9.5px;
  font-weight: 700;
  letter-spacing: 1.8px;
  text-transform: uppercase;
  color: var(--gray-600);
  padding: 8px 12px 6px;
  margin-top: 8px;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 11px 14px;
  border-radius: 10px;
  cursor: pointer;
  color: var(--gray-400);
  font-size: 13.5px;
  font-weight: 500;
  transition: var(--transition);
  margin-bottom: 2px;
  position: relative;
}
.nav-item:hover { background: rgba(255,255,255,0.06); color: var(--white); }
.nav-item.active {
  background: linear-gradient(135deg, rgba(45,122,255,0.2), rgba(0,201,177,0.1));
  color: var(--blue-glow);
  border: 1px solid rgba(45,122,255,0.25);
}
.nav-item.active::before {
  content: '';
  position: absolute;
  left: 0; top: 50%;
  transform: translateY(-50%);
  width: 3px; height: 60%;
  background: var(--blue-bright);
  border-radius: 0 2px 2px 0;
}
.nav-icon { font-size: 16px; min-width: 20px; text-align: center; }

.sidebar-footer {
  padding: 16px;
  border-top: 1px solid rgba(255,255,255,0.07);
}
.user-badge {
  display: flex; align-items: center; gap: 10px;
  padding: 10px 12px;
  background: rgba(255,255,255,0.04);
  border-radius: 10px;
}
.user-avatar {
  width: 34px; height: 34px;
  background: linear-gradient(135deg, var(--gold), var(--gold-light));
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 14px; font-weight: 700; color: var(--navy);
}
.user-info .user-name { font-size: 12.5px; font-weight: 600; color: var(--white); }
.user-info .user-role { font-size: 10px; color: var(--gold); font-weight: 500; }

#main {
  margin-left: var(--sidebar-w);
  flex: 1;
  min-height: 100vh;
  background: var(--navy);
}

.topbar {
  position: sticky; top: 0; z-index: 50;
  background: rgba(10,22,40,0.95);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255,255,255,0.06);
  padding: 16px 32px;
  display: flex; align-items: center; justify-content: space-between;
}
.topbar-title { font-size: 18px; font-weight: 700; color: var(--white); }
.topbar-date { font-size: 12px; color: var(--gray-400); font-family: 'JetBrains Mono', monospace; }

.content { padding: 28px 32px; }

.page { display: none; }
.page.active { display: block; animation: fadeIn 0.3s ease; }
@keyframes fadeIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }

.summary-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 16px;
  margin-bottom: 28px;
}
.stat-card {
  background: linear-gradient(135deg, var(--navy-mid), var(--navy-light));
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: var(--radius);
  padding: 22px;
  position: relative;
  overflow: hidden;
  transition: var(--transition);
}
.stat-card:hover { transform: translateY(-3px); box-shadow: var(--shadow); border-color: rgba(45,122,255,0.3); }
.stat-card::after {
  content: '';
  position: absolute;
  bottom: 0; right: 0;
  width: 80px; height: 80px;
  border-radius: 50%;
  opacity: 0.05;
}
.stat-card.blue::after { background: var(--blue-bright); }
.stat-card.teal::after { background: var(--teal); }
.stat-card.gold::after { background: var(--gold); }
.stat-card.green::after { background: var(--green); }
.stat-card.red::after { background: var(--red); }

.stat-icon {
  font-size: 24px;
  margin-bottom: 12px;
  display: block;
}
.stat-label { font-size: 11px; color: var(--gray-400); font-weight: 600; letter-spacing: 0.8px; text-transform: uppercase; margin-bottom: 6px; }
.stat-value { font-size: 26px; font-weight: 800; color: var(--white); font-family: 'JetBrains Mono', monospace; }
.stat-value.blue { color: var(--blue-glow); }
.stat-value.teal { color: var(--teal); }
.stat-value.gold { color: var(--gold-light); }
.stat-value.green { color: var(--green-light); }
.stat-value.red { color: #fc8181; }
.stat-sub { font-size: 11px; color: var(--gray-400); margin-top: 4px; }

.section-header {
  display: flex; align-items: center; justify-content: space-between;
  margin-bottom: 18px;
}
.section-title { font-size: 16px; font-weight: 700; color: var(--white); }
.section-sub { font-size: 12px; color: var(--gray-400); margin-top: 2px; }

.btn {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 10px 20px;
  border-radius: 9px;
  font-size: 13px;
  font-weight: 600;
  font-family: 'Sora', sans-serif;
  cursor: pointer;
  border: none;
  transition: var(--transition);
  white-space: nowrap;
}
.btn-primary {
  background: linear-gradient(135deg, var(--blue), var(--blue-bright));
  color: white;
  box-shadow: 0 4px 16px rgba(45,122,255,0.35);
}
.btn-primary:hover { transform: translateY(-1px); box-shadow: 0 6px 22px rgba(45,122,255,0.5); }
.btn-teal { background: linear-gradient(135deg, #00a99d, var(--teal)); color: white; }
.btn-teal:hover { transform: translateY(-1px); box-shadow: 0 6px 22px rgba(0,201,177,0.4); }
.btn-gold { background: linear-gradient(135deg, #e09615, var(--gold)); color: var(--navy); }
.btn-gold:hover { transform: translateY(-1px); box-shadow: 0 6px 22px rgba(245,166,35,0.4); }
.btn-green { background: linear-gradient(135deg, #00a381, var(--green)); color: white; }
.btn-green:hover { transform: translateY(-1px); }
.btn-danger { background: linear-gradient(135deg, #c53030, var(--red)); color: white; }
.btn-danger:hover { transform: translateY(-1px); }
.btn-ghost {
  background: rgba(255,255,255,0.06);
  color: var(--gray-400);
  border: 1px solid rgba(255,255,255,0.1);
}
.btn-ghost:hover { background: rgba(255,255,255,0.1); color: var(--white); }
.btn-sm { padding: 6px 14px; font-size: 12px; border-radius: 7px; }

.table-card {
  background: var(--navy-mid);
  border: 1px solid rgba(255,255,255,0.07);
  border-radius: var(--radius);
  overflow: hidden;
}
.table-toolbar {
  padding: 16px 20px;
  display: flex; align-items: center; gap: 12px;
  border-bottom: 1px solid rgba(255,255,255,0.06);
}
.search-input {
  flex: 1;
  background: rgba(255,255,255,0.05);
  border: 1px solid rgba(255,255,255,0.1);
  border-radius: 8px;
  padding: 8px 14px;
  color: var(--white);
  font-family: 'Sora', sans-serif;
  font-size: 13px;
  outline: none;
  transition: var(--transition);
}
.search-input:focus { border-color: var(--blue-bright); background: rgba(45,122,255,0.08); }
.search-input::placeholder { color: var(--gray-600); }

table { width: 100%; border-collapse: collapse; }
thead tr { border-bottom: 1px solid rgba(255,255,255,0.07); }
thead th {
  padding: 12px 16px;
  font-size: 11px;
  font-weight: 700;
  color: var(--gray-400);
  letter-spacing: 1px;
  text-transform: uppercase;
  text-align: left;
}
tbody tr {
  border-bottom: 1px solid rgba(255,255,255,0.04);
  transition: var(--transition);
}
tbody tr:last-child { border-bottom: none; }
tbody tr:hover { background: rgba(255,255,255,0.03); }
tbody td {
  padding: 14px 16px;
  font-size: 13.5px;
  color: var(--white);
}
.td-mono { font-family: 'JetBrains Mono', monospace; font-size: 13px; }

.badge {
  display: inline-flex; align-items: center;
  padding: 3px 10px;
  border-radius: 20px;
  font-size: 11px;
  font-weight: 600;
}
.badge-green { background: rgba(0,184,148,0.15); color: var(--green-light); border: 1px solid rgba(0,184,148,0.25); }
.badge-red { background: rgba(229,62,62,0.15); color: #fc8181; border: 1px solid rgba(229,62,62,0.25); }
.badge-gold { background: rgba(245,166,35,0.15); color: var(--gold-light); border: 1px solid rgba(245,166,35,0.25); }
.badge-blue { background: rgba(45,122,255,0.15); color: var(--blue-glow); border: 1px solid rgba(45,122,255,0.25); }
.badge-gray { background: rgba(122,143,181,0.15); color: var(--gray-400); border: 1px solid rgba(122,143,181,0.25); }
.badge-teal { background: rgba(0,201,177,0.15); color: var(--teal); border: 1px solid rgba(0,201,177,0.25); }

.modal-overlay {
  position: fixed; inset: 0; z-index: 200;
  background: rgba(0,0,0,0.7);
  backdrop-filter: blur(8px);
  display: flex; align-items: center; justify-content: center;
  padding: 20px;
  opacity: 0; pointer-events: none;
  transition: var(--transition);
}
.modal-overlay.open { opacity: 1; pointer-events: all; }
.modal {
  background: var(--navy-mid);
  border: 1px solid rgba(255,255,255,0.1);
  border-radius: 18px;
  padding: 32px;
  width: 100%; max-width: 520px;
  box-shadow: 0 20px 80px rgba(0,0,0,0.5);
  transform: scale(0.95) translateY(10px);
  transition: var(--transition);
  max-height: 90vh;
  overflow-y: auto;
}
.modal-overlay.open .modal { transform: scale(1) translateY(0); }
.modal-lg { max-width: 680px; }
.modal-header {
  display: flex; align-items: center; justify-content: space-between;
  margin-bottom: 24px;
}
.modal-title { font-size: 18px; font-weight: 700; }
.modal-close {
  width: 32px; height: 32px;
  background: rgba(255,255,255,0.07);
  border: none; border-radius: 8px;
  color: var(--gray-400);
  cursor: pointer;
  font-size: 18px;
  display: flex; align-items: center; justify-content: center;
  transition: var(--transition);
}
.modal-close:hover { background: rgba(229,62,62,0.2); color: #fc8181; }

.form-group { margin-bottom: 18px; }
.form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
label {
  display: block;
  font-size: 12px;
  font-weight: 600;
  color: var(--gray-400);
  text-transform: uppercase;
  letter-spacing: 0.8px;
  margin-bottom: 7px;
}
input, select, textarea {
  width: 100%;
  background: rgba(255,255,255,0.05);
  border: 1px solid rgba(255,255,255,0.1);
  border-radius: 9px;
  padding: 11px 14px;
  color: var(--white);
  font-family: 'Sora', sans-serif;
  font-size: 13.5px;
  outline: none;
  transition: var(--transition);
}
input:focus, select:focus, textarea:focus {
  border-color: var(--blue-bright);
  background: rgba(45,122,255,0.07);
  box-shadow: 0 0 0 3px rgba(45,122,255,0.15);
}
input::placeholder { color: var(--gray-600); }
select option { background: var(--navy-mid); }
.form-note {
  font-size: 11.5px; color: var(--teal);
  margin-top: 6px;
  font-family: 'JetBrains Mono', monospace;
}
.form-actions {
  display: flex; gap: 12px; justify-content: flex-end;
  margin-top: 24px; padding-top: 20px;
  border-top: 1px solid rgba(255,255,255,0.07);
}

.loan-preview {
  background: rgba(0,201,177,0.07);
  border: 1px solid rgba(0,201,177,0.2);
  border-radius: 10px;
  padding: 16px;
  margin: 16px 0;
}
.loan-preview-row {
  display: flex; justify-content: space-between;
  font-size: 13px; padding: 4px 0;
}
.loan-preview-row.total {
  font-weight: 700; font-size: 15px;
  border-top: 1px solid rgba(0,201,177,0.2);
  margin-top: 8px; padding-top: 10px;
  color: var(--teal);
}

#toast-container {
  position: fixed; top: 20px; right: 20px; z-index: 500;
  display: flex; flex-direction: column; gap: 10px;
}
.toast {
  padding: 14px 20px;
  border-radius: 10px;
  font-size: 13.5px;
  font-weight: 500;
  box-shadow: var(--shadow);
  animation: toastIn 0.3s ease;
  display: flex; align-items: center; gap: 10px;
  min-width: 280px;
}
.toast-success { background: linear-gradient(135deg, #00a381, var(--green)); color: white; }
.toast-error { background: linear-gradient(135deg, #c53030, var(--red)); color: white; }
.toast-info { background: linear-gradient(135deg, var(--blue), var(--blue-bright)); color: white; }
.toast-warn { background: linear-gradient(135deg, #c08000, var(--gold)); color: var(--navy); }
@keyframes toastIn { from { opacity: 0; transform: translateX(30px); } to { opacity: 1; transform: translateX(0); } }

.tx-item {
  display: flex; align-items: center; gap: 14px;
  padding: 14px 20px;
  border-bottom: 1px solid rgba(255,255,255,0.04);
  transition: var(--transition);
}
.tx-item:last-child { border-bottom: none; }
.tx-item:hover { background: rgba(255,255,255,0.03); }
.tx-icon {
  width: 38px; height: 38px;
  border-radius: 10px;
  display: flex; align-items: center; justify-content: center;
  font-size: 16px;
  flex-shrink: 0;
}
.tx-info { flex: 1; }
.tx-name { font-size: 13.5px; font-weight: 600; color: var(--white); }
.tx-desc { font-size: 12px; color: var(--gray-400); margin-top: 2px; }
.tx-amount { font-family: 'JetBrains Mono', monospace; font-weight: 700; font-size: 14px; }
.tx-date { font-size: 11px; color: var(--gray-600); }

.receipt {
  background: white; color: #111;
  border-radius: 10px; padding: 28px;
  font-family: 'JetBrains Mono', monospace;
}
.receipt-header { text-align: center; margin-bottom: 20px; }
.receipt-logo { font-size: 20px; font-weight: 800; color: #0a1628; }
.receipt-sub { font-size: 11px; color: #666; }
.receipt-divider { border: 1px dashed #ccc; margin: 12px 0; }
.receipt-row { display: flex; justify-content: space-between; font-size: 12.5px; margin-bottom: 6px; }
.receipt-total { font-weight: 800; font-size: 14px; border-top: 2px solid #111; padding-top: 8px; margin-top: 8px; }
.receipt-footer { text-align: center; font-size: 11px; color: #999; margin-top: 16px; }

.dist-card {
  background: linear-gradient(135deg, rgba(0,201,177,0.1), rgba(45,122,255,0.1));
  border: 1px solid rgba(0,201,177,0.2);
  border-radius: var(--radius);
  padding: 24px;
  margin-bottom: 24px;
}
.dist-title { font-size: 16px; font-weight: 700; margin-bottom: 8px; }
.dist-formula { font-size: 13px; color: var(--gray-400); font-family: 'JetBrains Mono', monospace; margin-bottom: 16px; }
.dist-amounts {
  display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px;
}
.dist-item { text-align: center; }
.dist-item .val { font-size: 22px; font-weight: 800; font-family: 'JetBrains Mono', monospace; }
.dist-item .lbl { font-size: 11px; color: var(--gray-400); margin-top: 4px; }

.empty-state {
  text-align: center; padding: 60px 20px;
  color: var(--gray-600);
}
.empty-state .icon { font-size: 48px; margin-bottom: 14px; opacity: 0.5; }
.empty-state p { font-size: 14px; }

/* ===== DATA BACKUP BANNER ===== */
.backup-banner {
  background: linear-gradient(135deg, rgba(245,166,35,0.15), rgba(255,209,102,0.08));
  border: 1px solid rgba(245,166,35,0.3);
  border-radius: 12px;
  padding: 14px 20px;
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  flex-wrap: wrap;
}
.backup-banner-text { font-size: 13px; color: var(--gold-light); }
.backup-banner-text strong { color: var(--white); }

/* ===== DATA MANAGER PAGE ===== */
.data-manager-card {
  background: var(--navy-mid);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: var(--radius);
  padding: 28px;
  margin-bottom: 20px;
}
.data-manager-card h3 { font-size: 15px; font-weight: 700; margin-bottom: 8px; }
.data-manager-card p { font-size: 13px; color: var(--gray-400); margin-bottom: 16px; line-height: 1.6; }

#login-page {
  position: fixed; inset: 0; z-index: 999;
  background: var(--navy);
  display: flex; align-items: center; justify-content: center;
}
.login-box {
  background: var(--navy-mid);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 20px;
  padding: 44px;
  width: 380px;
  box-shadow: 0 20px 80px rgba(0,0,0,0.5);
}
.login-logo {
  text-align: center; margin-bottom: 32px;
}
.login-logo .icon {
  width: 60px; height: 60px;
  background: linear-gradient(135deg, var(--blue-bright), var(--teal));
  border-radius: 16px;
  display: flex; align-items: center; justify-content: center;
  font-size: 28px; margin: 0 auto 14px;
  box-shadow: 0 8px 30px rgba(45,122,255,0.4);
}
.login-logo h1 { font-size: 20px; font-weight: 800; }
.login-logo p { font-size: 12px; color: var(--gray-400); margin-top: 4px; }
.login-error {
  background: rgba(229,62,62,0.12);
  border: 1px solid rgba(229,62,62,0.25);
  border-radius: 8px; padding: 10px 14px;
  font-size: 12.5px; color: #fc8181;
  margin-bottom: 16px; display: none;
}

@media (max-width: 900px) {
  :root { --sidebar-w: 0px; }
  #sidebar { transform: translateX(-260px); width: 260px; }
  #sidebar.open { transform: translateX(0); box-shadow: 4px 0 30px rgba(0,0,0,0.5); }
  #main { margin-left: 0; }
  .content { padding: 20px 16px; }
  .summary-grid { grid-template-columns: repeat(2, 1fr); }
  .dist-amounts { grid-template-columns: 1fr 1fr; }
  .form-row { grid-template-columns: 1fr; }
}

@media print {
  body * { visibility: hidden; }
  .receipt, .receipt * { visibility: visible; }
  .receipt { position: fixed; top: 0; left: 0; width: 100%; }
}

::-webkit-scrollbar { width: 5px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.1); border-radius: 3px; }
</style>
</head>
<body>

<!-- LOGIN PAGE -->
<div id="login-page">
  <div class="login-box">
    <div class="login-logo">
      <div class="icon">🏦</div>
      <h1>Nuñez Saving Vault</h1>
      <p>Community Savings & Loan System</p>
    </div>
    <div class="login-error" id="login-error">Invalid username or password.</div>
    <div class="form-group">
      <label>Username</label>
      <input type="text" id="login-user" placeholder="Enter username">
    </div>
    <div class="form-group">
      <label>Password</label>
      <input type="password" id="login-pass" placeholder="Enter password" onkeydown="if(event.key==='Enter')doLogin()">
    </div>
    <button class="btn btn-primary" style="width:100%;justify-content:center;padding:13px;" onclick="doLogin()">🔐 Login</button>
    <div style="margin-top:16px;padding:12px;background:rgba(0,201,177,0.07);border:1px solid rgba(0,201,177,0.2);border-radius:9px;font-size:11.5px;color:var(--teal);text-align:center;">
      💾 Your data is saved in this browser's storage.<br>Use <strong>Export Data</strong> to back up or move to another device.
    </div>

  </div>
</div>

<!-- SIDEBAR -->
<div id="sidebar">
  <div class="sidebar-logo">
    <div class="logo-icon">🏦</div>
    <div class="logo-name">Nuñez Saving Vault</div>
    <div class="logo-sub">Community System</div>
  </div>
  <nav>
    <div class="nav-section-label">Main</div>
    <div class="nav-item active" onclick="showPage('dashboard')">
      <span class="nav-icon">📊</span> Dashboard
    </div>
    <div class="nav-section-label">Management</div>
    <div class="nav-item" onclick="showPage('members')">
      <span class="nav-icon">👥</span> Members
    </div>
    <div class="nav-item" onclick="showPage('contributions')">
      <span class="nav-icon">💰</span> Contributions
    </div>
    <div class="nav-item" onclick="showPage('loans')">
      <span class="nav-icon">🏷️</span> Loans
    </div>
    <div class="nav-item" onclick="showPage('payments')">
      <span class="nav-icon">💳</span> Payments
    </div>
    <div class="nav-section-label">Finance</div>
    <div class="nav-item" onclick="showPage('interest')">
      <span class="nav-icon">✨</span> Interest Pool
    </div>
    <div class="nav-item" onclick="showPage('reports')">
      <span class="nav-icon">📋</span> Reports
    </div>
    <div class="nav-section-label">System</div>
    <div class="nav-item" onclick="showPage('transactions')">
      <span class="nav-icon">🔄</span> Transaction Log
    </div>
    <div class="nav-item admin-only" onclick="showPage('datamanager')">
      <span class="nav-icon">💾</span> Data Backup
    </div>
    <div class="nav-item admin-only" onclick="openResetConfirm()" style="color:#fc8181;">
      <span class="nav-icon">🗑️</span> Reset All Data
    </div>
    <div class="nav-item" onclick="doLogout()">
      <span class="nav-icon">🚪</span> Logout
    </div>
  </nav>
  <div class="sidebar-footer">
    <div class="user-badge">
      <div class="user-avatar" id="user-avatar-text">A</div>
      <div class="user-info">
        <div class="user-name" id="user-display">Admin</div>
        <div class="user-role" id="user-role">Administrator</div>
      </div>
    </div>
  </div>
</div>

<!-- MAIN -->
<div id="main">
  <div class="topbar">
    <div>
      <div class="topbar-title" id="page-title">Dashboard</div>
      <div class="topbar-date" id="topbar-date"></div>
    </div>
    <div style="display:flex;gap:10px;align-items:center;">
      <span id="view-only-badge" class="badge badge-teal" style="display:none;">👁️ View Only</span>
      <button class="btn btn-ghost btn-sm admin-only" onclick="showPage('datamanager')" title="Backup your data">💾 Backup</button>
      <span id="week-badge" class="badge badge-gold">📅 Week Collection</span>
    </div>
  </div>

  <div class="content">
    <!-- Member view-only banner -->
    <div id="member-banner" style="display:none;background:linear-gradient(135deg,rgba(0,201,177,0.12),rgba(45,122,255,0.08));border:1px solid rgba(0,201,177,0.25);border-radius:12px;padding:13px 20px;margin-bottom:20px;display:none;align-items:center;gap:12px;">
      <span style="font-size:20px;">👁️</span>
      <div>
        <div style="font-size:13.5px;font-weight:600;color:var(--white);">View Only Mode</div>
        <div style="font-size:12px;color:var(--gray-400);margin-top:2px;">You are logged in as a <strong style="color:var(--teal);">Member</strong>. You can view all records but cannot add, edit, or delete anything.</div>
      </div>
    </div>

    <!-- ======== DASHBOARD ======== -->
    <div class="page active" id="page-dashboard">
      <div class="summary-grid">
        <div class="stat-card blue">
          <span class="stat-icon">👥</span>
          <div class="stat-label">Total Members</div>
          <div class="stat-value blue" id="stat-members">0</div>
          <div class="stat-sub">Active members</div>
        </div>
        <div class="stat-card teal">
          <span class="stat-icon">💰</span>
          <div class="stat-label">Total Contributions</div>
          <div class="stat-value teal" id="stat-contributions">₱0</div>
          <div class="stat-sub">All time</div>
        </div>
        <div class="stat-card gold">
          <span class="stat-icon">🏷️</span>
          <div class="stat-label">Active Loans</div>
          <div class="stat-value gold" id="stat-loans">₱0</div>
          <div class="stat-sub">Outstanding</div>
        </div>
        <div class="stat-card green">
          <span class="stat-icon">✨</span>
          <div class="stat-label">Interest Collected</div>
          <div class="stat-value green" id="stat-interest">₱0</div>
          <div class="stat-sub">Undistributed</div>
        </div>
        <div class="stat-card red">
          <span class="stat-icon">📤</span>
          <div class="stat-label">Interest Distributed</div>
          <div class="stat-value red" id="stat-distributed">₱0</div>
          <div class="stat-sub">Total given out</div>
        </div>
        <div class="stat-card gold">
          <span class="stat-icon">🧑</span>
          <div class="stat-label">Total Active Heads</div>
          <div class="stat-value gold" id="stat-heads">0</div>
          <div class="stat-sub">All active members</div>
        </div>
        <div class="stat-card blue">
          <span class="stat-icon">💵</span>
          <div class="stat-label">Daily Rate / Head</div>
          <div class="stat-value blue" id="stat-perhead" style="font-size:18px;">₱5/day</div>
          <div class="stat-sub">= ₱35/head/week</div>
        </div>
        <div class="stat-card cash">
          <span class="stat-icon">🏦</span>
          <div class="stat-label">Cash on Hand</div>
          <div class="stat-value" id="stat-cash">₱0</div>
          <div class="stat-sub" id="stat-cash-sub">Vault available funds</div>
        </div>
      </div>

      <div style="display:grid;grid-template-columns:1fr 360px;gap:20px;">
        <div class="table-card">
          <div style="padding:18px 20px;border-bottom:1px solid rgba(255,255,255,0.06);">
            <div class="section-title">Recent Transactions</div>
            <div class="section-sub">Latest system activity</div>
          </div>
          <div class="tx-list" id="recent-tx-list">
            <div class="empty-state"><div class="icon">📭</div><p>No transactions yet.</p></div>
          </div>
        </div>
        <div>
          <div class="table-card" style="margin-bottom:16px;">
            <div style="padding:18px 20px;border-bottom:1px solid rgba(255,255,255,0.06);">
              <div class="section-title">Top Contributors</div>
            </div>
            <div id="top-contributors">
              <div class="empty-state" style="padding:30px 20px;"><div class="icon" style="font-size:30px;">🥇</div><p>No data yet.</p></div>
            </div>
          </div>
          <div class="table-card">
            <div style="padding:18px 20px;border-bottom:1px solid rgba(255,255,255,0.06);">
              <div class="section-title">Quick Actions</div>
            </div>
            <div style="padding:16px;display:flex;flex-direction:column;gap:10px;">
              <button class="btn btn-primary write-only" style="width:100%;justify-content:center;" onclick="openModal('modal-add-member')">➕ Add Member</button>
              <button class="btn btn-teal write-only" style="width:100%;justify-content:center;" onclick="openModal('modal-contribution')">💰 Record Contribution</button>
              <button class="btn btn-gold write-only" style="width:100%;justify-content:center;" onclick="openModal('modal-loan')">🏷️ Issue Loan</button>
              <button class="btn btn-green write-only" style="width:100%;justify-content:center;" onclick="showPage('interest')">✨ Distribute Interest</button>
              <div id="member-quick-view" style="display:none;text-align:center;padding:16px 0;color:var(--gray-400);font-size:13px;">
                <div style="font-size:28px;margin-bottom:8px;">👁️</div>
                <div style="font-weight:600;color:var(--white);">View Only Access</div>
                <div style="font-size:12px;margin-top:4px;">You can browse all records<br>but cannot make changes.</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- ======== MEMBERS ======== -->
    <div class="page" id="page-members">
      <div class="section-header">
        <div>
          <div class="section-title">Member Management</div>
          <div class="section-sub">Manage all vault members</div>
        </div>
        <button class="btn btn-primary write-only" onclick="openModal('modal-add-member')">➕ Add Member</button>
      </div>
      <div class="table-card">
        <div class="table-toolbar">
          <input class="search-input" placeholder="🔍 Search members..." oninput="filterMembers(this.value)">
          <button class="btn btn-ghost btn-sm" onclick="renderMembers()">↻ Refresh</button>
        </div>
        <div style="overflow-x:auto;">
          <table>
            <thead>
              <tr>
                <th>Member ID</th>
                <th>Full Name</th>
                <th style="text-align:center;">Heads 🧑</th>
                <th>Contribution</th>
                <th>Active Loan</th>
                <th>Interest Earned</th>
                <th>Status</th>
                <th>Actions</th>
              </tr>
            </thead>
            <tbody id="members-tbody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ======== CONTRIBUTIONS ======== -->
    <div class="page" id="page-contributions">
      <div class="section-header">
        <div>
          <div class="section-title">Weekly Contributions</div>
          <div class="section-sub">Sunday collection records</div>
        </div>
        <button class="btn btn-teal write-only" onclick="openModal('modal-contribution')">💰 Record Contribution</button>
      </div>
      <div class="table-card">
        <div class="table-toolbar">
          <input class="search-input" placeholder="🔍 Search contributions...">
        </div>
        <div style="overflow-x:auto;">
          <table>
            <thead>
              <tr>
                <th>#</th>
                <th>Member</th>
                <th style="text-align:center;">Heads</th>
                <th>Amount</th>
                <th>Date</th>
                <th>Collector</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody id="contributions-tbody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ======== LOANS ======== -->
    <div class="page" id="page-loans">
      <div class="section-header">
        <div>
          <div class="section-title">Loan Management</div>
          <div class="section-sub">All active and completed loans</div>
        </div>
        <button class="btn btn-gold write-only" onclick="openModal('modal-loan')">🏷️ Issue Loan</button>
      </div>
      <div class="table-card">
        <div style="overflow-x:auto;">
          <table>
            <thead>
              <tr>
                <th>Loan ID</th>
                <th>Member</th>
                <th>Principal</th>
                <th>Interest (5%)</th>
                <th>Total</th>
                <th>Remaining</th>
                <th>Status</th>
                <th>Date</th>
                <th>Pay</th>
                <th>Edit</th>
              </tr>
            </thead>
            <tbody id="loans-tbody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ======== PAYMENTS ======== -->
    <div class="page" id="page-payments">
      <div class="section-header">
        <div>
          <div class="section-title">Payment Records</div>
          <div class="section-sub">All loan payment history</div>
        </div>
      </div>
      <div class="table-card">
        <div style="overflow-x:auto;">
          <table>
            <thead>
              <tr>
                <th>#</th>
                <th>Member</th>
                <th>Loan ID</th>
                <th>Payment Type</th>
                <th>Amount</th>
                <th>Date</th>
                <th>Receipt</th>
                <th>Edit</th>
              </tr>
            </thead>
            <tbody id="payments-tbody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ======== INTEREST POOL ======== -->
    <div class="page" id="page-interest">
      <div class="section-header">
        <div>
          <div class="section-title">Interest Pool Distribution</div>
          <div class="section-sub">Distributed proportionally by number of heads per member</div>
        </div>
        <div style="display:flex;align-items:center;gap:10px;flex-wrap:wrap;">
          <span style="font-size:12px;color:var(--gray-400);">Daily rate per head:</span>
          <input type="number" id="rate-per-head" style="width:70px;padding:7px 10px;font-size:13px;" value="5" min="1" onchange="updateRatePerHead(this.value)">
          <span style="font-size:12px;color:var(--gray-400);">₱/day</span>
          <span id="rate-weekly-label" style="font-size:12px;color:var(--teal);font-weight:600;">= ₱35/head/week</span>
        </div>
      </div>
      <div class="dist-card">
        <div class="dist-title">📊 Heads-Based Distribution Summary</div>
        <div class="dist-formula" id="dist-formula">Formula: Total Interest ÷ Total Active Heads = Per Head Share</div>
        <div class="dist-amounts" style="grid-template-columns:repeat(4,1fr);">
          <div class="dist-item">
            <div class="val teal" id="dist-total" style="color:var(--teal)">₱0</div>
            <div class="lbl">Total Interest Pool</div>
          </div>
          <div class="dist-item">
            <div class="val blue" id="dist-members" style="color:var(--blue-glow)">0</div>
            <div class="lbl">Active Members</div>
          </div>
          <div class="dist-item">
            <div class="val gold" id="dist-heads" style="color:var(--gold-light)">0</div>
            <div class="lbl">Total Active Heads 🧑</div>
          </div>
          <div class="dist-item">
            <div class="val" id="dist-perhead" style="color:var(--teal)">₱0</div>
            <div class="lbl">Per Head Share</div>
          </div>
        </div>
        <button class="btn btn-teal write-only" style="margin-top:20px;font-size:14px;padding:12px 28px;" onclick="confirmDistribute()">✨ Distribute Interest (By Heads)</button>
        <div class="member-only-msg" style="display:none;margin-top:16px;padding:12px 18px;background:rgba(0,201,177,0.07);border:1px solid rgba(0,201,177,0.2);border-radius:10px;font-size:13px;color:var(--teal);">👁️ You have view-only access. Interest distribution is restricted to Admin/Treasurer.</div>
      </div>

      <div class="table-card">
        <div style="padding:16px 20px;border-bottom:1px solid rgba(255,255,255,0.06);">
          <div class="section-title">Distribution Preview — Per Member Based on Heads</div>
          <div style="font-size:12px;color:var(--gray-400);margin-top:4px;">📐 Formula: <span style="color:var(--teal);font-family:monospace;">Contribution + Interest Share − Loan (w/ Interest) = Net New Contribution</span></div>
        </div>
        <div style="overflow-x:auto;">
          <table>
            <thead>
              <tr>
                <th>Member</th>
                <th style="text-align:center;">Heads 🧑</th>
                <th>Current Contribution</th>
                <th>Interest Share</th>
                <th>Active Loan (w/ interest)</th>
                <th>Net New Contribution</th>
              </tr>
            </thead>
            <tbody id="dist-preview-tbody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ======== REPORTS ======== -->
    <div class="page" id="page-reports">
      <div class="section-header">
        <div>
          <div class="section-title">Reports</div>
          <div class="section-sub">Generate and export system reports</div>
        </div>
      </div>
      <div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:16px;margin-bottom:28px;">
        <div class="stat-card" style="cursor:pointer;" onclick="generateReport('contributions')">
          <span class="stat-icon">📋</span>
          <div class="stat-label">Weekly Contribution</div>
          <div style="font-size:13px;color:var(--gray-400);margin-top:4px;">View all contribution records</div>
          <button class="btn btn-primary btn-sm" style="margin-top:14px;">Generate Report</button>
        </div>
        <div class="stat-card" style="cursor:pointer;" onclick="generateReport('loans')">
          <span class="stat-icon">🏷️</span>
          <div class="stat-label">Loan Report</div>
          <div style="font-size:13px;color:var(--gray-400);margin-top:4px;">All active & completed loans</div>
          <button class="btn btn-gold btn-sm" style="margin-top:14px;">Generate Report</button>
        </div>
        <div class="stat-card" style="cursor:pointer;" onclick="generateReport('interest')">
          <span class="stat-icon">✨</span>
          <div class="stat-label">Interest Distribution</div>
          <div style="font-size:13px;color:var(--gray-400);margin-top:4px;">Interest history log</div>
          <button class="btn btn-teal btn-sm" style="margin-top:14px;">Generate Report</button>
        </div>
        <div class="stat-card" style="cursor:pointer;" onclick="generateReport('ledger')">
          <span class="stat-icon">📒</span>
          <div class="stat-label">Member Ledger</div>
          <div style="font-size:13px;color:var(--gray-400);margin-top:4px;">Individual member records</div>
          <button class="btn btn-ghost btn-sm" style="margin-top:14px;">Generate Report</button>
        </div>
      </div>
      <div class="table-card" id="report-output" style="display:none;">
        <div style="padding:16px 20px;border-bottom:1px solid rgba(255,255,255,0.06);display:flex;align-items:center;justify-content:space-between;">
          <div class="section-title" id="report-title">Report</div>
          <button class="btn btn-primary btn-sm" onclick="printReport()">🖨️ Print / Export PDF</button>
        </div>
        <div id="report-content" style="padding:20px;"></div>
      </div>
    </div>

    <!-- ======== TRANSACTIONS ======== -->
    <div class="page" id="page-transactions">
      <div class="section-header">
        <div>
          <div class="section-title">Transaction Log</div>
          <div class="section-sub">Complete system activity history</div>
        </div>
      </div>
      <div class="table-card">
        <div style="overflow-x:auto;">
          <table>
            <thead>
              <tr>
                <th>#</th>
                <th>Type</th>
                <th>Description</th>
                <th>Member</th>
                <th>Amount</th>
                <th>Date & Time</th>
              </tr>
            </thead>
            <tbody id="tx-tbody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ======== DATA MANAGER ======== -->
    <div class="page" id="page-datamanager">
      <div class="section-header">
        <div>
          <div class="section-title">💾 Data Backup & Restore</div>
          <div class="section-sub">Export your data to keep it safe, or import to restore/transfer</div>
        </div>
      </div>

      <div style="background:rgba(0,201,177,0.08);border:1px solid rgba(0,201,177,0.25);border-radius:12px;padding:18px 22px;margin-bottom:22px;font-size:13.5px;color:var(--teal);line-height:1.7;">
        ℹ️ <strong style="color:var(--white);">How data works:</strong> All your data (members, contributions, loans, payments) is saved in <strong>this browser's localStorage</strong>. When you copy the HTML code and open it in a new browser or computer, the data won't transfer automatically. Use <strong>Export</strong> to download your data as a file, then <strong>Import</strong> it on the new device to restore everything.
      </div>

      <div style="display:grid;grid-template-columns:1fr 1fr;gap:20px;margin-bottom:20px;">
        <div class="data-manager-card">
          <h3>📤 Export Data</h3>
          <p>Download all your vault data as a JSON file. Use this to back up your data or transfer it to another browser/device.</p>
          <div style="margin-bottom:12px;padding:12px;background:rgba(255,255,255,0.03);border-radius:8px;font-size:12px;color:var(--gray-400);" id="export-summary">Loading...</div>
          <button class="btn btn-primary" onclick="exportData()" style="width:100%;justify-content:center;">📥 Download Data Backup (.json)</button>
        </div>

        <div class="data-manager-card">
          <h3>📨 Import Data</h3>
          <p>Restore data from a previously exported backup file. <strong style="color:#fc8181;">Warning:</strong> This will replace ALL current data.</p>
          <div class="form-group" style="margin-bottom:12px;">
            <input type="file" id="import-file" accept=".json" style="font-size:12px;padding:8px;" onchange="previewImport(this)">
          </div>
          <div id="import-preview" style="display:none;margin-bottom:12px;padding:12px;background:rgba(0,201,177,0.07);border:1px solid rgba(0,201,177,0.2);border-radius:8px;font-size:12px;color:var(--teal);"></div>
          <button class="btn btn-teal" onclick="importData()" style="width:100%;justify-content:center;">📤 Import & Restore Data</button>
        </div>
      </div>

      <div class="data-manager-card">
        <h3>📋 Copy Data as Text</h3>
        <p>Copy all your data as raw JSON text — you can paste it somewhere to save it, or embed it directly into the HTML file so it loads automatically.</p>
        <button class="btn btn-ghost" onclick="copyDataToClipboard()" style="margin-bottom:14px;">📋 Copy JSON to Clipboard</button>
        <div style="font-size:12px;color:var(--gray-400);margin-bottom:10px;">Or view the raw data below:</div>
        <textarea id="data-json-view" style="height:120px;font-size:11px;font-family:monospace;resize:vertical;" readonly></textarea>
      </div>

      <div class="data-manager-card" style="border-color:rgba(255,77,77,0.2);">
        <h3 style="color:#fc8181;">🔐 Embed Data Into HTML (Advanced)</h3>
        <p>To make your data appear automatically when you open the HTML file, you can embed your current data directly into the code. After exporting or copying the data, paste it into the <code style="background:rgba(255,255,255,0.08);padding:2px 6px;border-radius:4px;font-size:11px;">EMBEDDED_DATA</code> variable inside the &lt;script&gt; section of the HTML file.</p>
        <div style="background:rgba(255,255,255,0.04);border-radius:8px;padding:14px;font-size:12px;font-family:monospace;color:var(--gray-400);line-height:1.8;">
          Find this line in the HTML:<br>
          <span style="color:var(--teal);">const EMBEDDED_DATA = null;</span><br><br>
          Replace <span style="color:#fc8181;">null</span> with your exported JSON data to pre-load it.
        </div>
      </div>
    </div>

  </div><!-- /content -->
</div><!-- /main -->

<!-- ======== MODALS ======== -->

<!-- Add / Edit Member -->
<div class="modal-overlay" id="modal-add-member">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title" id="member-modal-title">➕ Add New Member</div>
      <button class="modal-close" onclick="closeModal('modal-add-member')">✕</button>
    </div>
    <input type="hidden" id="edit-member-id">
    <div class="form-group">
      <label>Full Name</label>
      <input type="text" id="member-name" placeholder="Enter full name">
    </div>
    <div class="form-row">
      <div class="form-group">
        <label>Number of Heads 🧑</label>
        <select id="member-heads" onchange="updateHeadsPreview()">
          <option value="1">1 Head</option>
          <option value="2">2 Heads</option>
          <option value="3">3 Heads</option>
          <option value="4">4 Heads</option>
          <option value="5">5 Heads</option>
          <option value="6">6 Heads</option>
          <option value="7">7 Heads</option>
          <option value="8">8 Heads</option>
          <option value="9">9 Heads</option>
          <option value="10">10 Heads</option>
        </select>
        <div class="form-note" id="heads-preview">Weekly contribution: ₱5 × 1 head = ₱5.00</div>
      </div>
      <div class="form-group">
        <label>Status</label>
        <select id="member-status">
          <option value="Active">Active</option>
          <option value="Inactive">Inactive</option>
        </select>
      </div>
    </div>
    <div class="form-row">
      <div class="form-group">
        <label>Initial Contribution (₱)</label>
        <input type="number" id="member-initial" placeholder="0.00" min="0" step="0.01">
      </div>
    </div>
    <div class="form-actions">
      <button class="btn btn-ghost" onclick="closeModal('modal-add-member')">Cancel</button>
      <button class="btn btn-primary" onclick="saveMember()">💾 Save Member</button>
    </div>
  </div>
</div>

<!-- Record Contribution -->
<div class="modal-overlay" id="modal-contribution">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">💰 Record Weekly Contribution</div>
      <button class="modal-close" onclick="closeModal('modal-contribution')">✕</button>
    </div>
    <div class="form-group">
      <label>Select Member</label>
      <select id="contribution-member" onchange="onContributionMemberChange()"></select>
    </div>
    <div id="contribution-heads-info" style="background:rgba(245,166,35,0.08);border:1px solid rgba(245,166,35,0.2);border-radius:9px;padding:12px 14px;margin-bottom:14px;font-size:13px;display:none;">
      <span id="c-heads-badge" style="color:var(--gold-light);font-weight:700;"></span>
      <span style="color:var(--gray-400);"> — Weekly amount auto-computed below</span>
    </div>
    <div class="form-row">
      <div class="form-group">
        <label>Amount (₱)</label>
        <input type="number" id="contribution-amount" placeholder="0.00" min="0.01" step="0.01" oninput="calcContribution()">
      </div>
      <div class="form-group">
        <label>Date</label>
        <input type="date" id="contribution-date">
      </div>
    </div>
    <div class="form-group">
      <label>Collector</label>
      <input type="text" id="contribution-collector" placeholder="Name of collector">
    </div>
    <div class="loan-preview" id="contribution-preview" style="display:none;background:rgba(45,122,255,0.07);border-color:rgba(45,122,255,0.2);">
      <div class="loan-preview-row"><span style="color:var(--gold-light);">🧑 Heads Calculation:</span><span id="cp-heads" class="td-mono" style="color:var(--gold-light);font-size:12px;"></span></div>
      <div class="loan-preview-row"><span>Current Contribution:</span><span id="cp-current" class="td-mono"></span></div>
      <div class="loan-preview-row"><span>Adding:</span><span id="cp-adding" class="td-mono" style="color:var(--teal)"></span></div>
      <div class="loan-preview-row total"><span>New Total:</span><span id="cp-new" class="td-mono"></span></div>
    </div>
    <div class="form-actions">
      <button class="btn btn-ghost" onclick="closeModal('modal-contribution')">Cancel</button>
      <button class="btn btn-teal" onclick="saveContribution()">✅ Record Contribution</button>
    </div>
  </div>
</div>

<!-- Issue Loan -->
<div class="modal-overlay" id="modal-loan">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">🏷️ Issue New Loan</div>
      <button class="modal-close" onclick="closeModal('modal-loan')">✕</button>
    </div>
    <div class="form-group">
      <label>Select Member</label>
      <select id="loan-member" onchange="calcLoan()"></select>
    </div>
    <div class="form-row">
      <div class="form-group">
        <label>Principal Amount (₱)</label>
        <input type="number" id="loan-principal" placeholder="0.00" min="1" step="0.01" oninput="calcLoan()">
      </div>
      <div class="form-group">
        <label>Date</label>
        <input type="date" id="loan-date">
      </div>
    </div>
    <div class="loan-preview" id="loan-preview" style="display:none;">
      <div class="loan-preview-row"><span>Principal:</span><span id="lp-principal" class="td-mono"></span></div>
      <div class="loan-preview-row"><span>Interest (5%):</span><span id="lp-interest" class="td-mono" style="color:var(--gold-light)"></span></div>
      <div class="loan-preview-row total"><span>Total Loan:</span><span id="lp-total" class="td-mono"></span></div>
      <div class="loan-preview-row"><span style="color:var(--gray-400)">Member's contribution:</span><span id="lp-contrib" class="td-mono" style="color:var(--gray-400)"></span></div>
      <div class="loan-preview-row"><span style="color:var(--gray-400)">After deduction:</span><span id="lp-after" class="td-mono" style="color:var(--gray-400)"></span></div>
    </div>
    <div class="form-actions">
      <button class="btn btn-ghost" onclick="closeModal('modal-loan')">Cancel</button>
      <button class="btn btn-gold" onclick="saveLoan()">✅ Issue Loan</button>
    </div>
  </div>
</div>

<!-- Make Payment -->
<div class="modal-overlay" id="modal-payment">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">💳 Make Loan Payment</div>
      <button class="modal-close" onclick="closeModal('modal-payment')">✕</button>
    </div>
    <input type="hidden" id="payment-loan-id">
    <div id="payment-loan-info" style="background:rgba(255,255,255,0.04);border-radius:10px;padding:14px;margin-bottom:16px;font-size:13px;"></div>
    <div class="form-group">
      <label>Payment Type</label>
      <select id="payment-type" onchange="calcPayment()">
        <option value="interest_only">Interest Only</option>
        <option value="principal_only">Principal Only</option>
        <option value="principal_interest">Principal + Interest (Full)</option>
      </select>
    </div>
    <div class="form-row">
      <div class="form-group">
        <label>Amount (₱)</label>
        <input type="number" id="payment-amount" placeholder="0.00" min="0.01" step="0.01">
      </div>
      <div class="form-group">
        <label>Date</label>
        <input type="date" id="payment-date">
      </div>
    </div>
    <div class="loan-preview" id="payment-preview" style="display:none;">
      <div class="loan-preview-row"><span>Remaining Balance Before:</span><span id="pp-before" class="td-mono"></span></div>
      <div class="loan-preview-row"><span>Payment:</span><span id="pp-pay" class="td-mono" style="color:var(--teal)"></span></div>
      <div class="loan-preview-row total"><span>Remaining After:</span><span id="pp-after" class="td-mono"></span></div>
    </div>
    <div class="form-actions">
      <button class="btn btn-ghost" onclick="closeModal('modal-payment')">Cancel</button>
      <button class="btn btn-green" onclick="savePayment()">✅ Process Payment</button>
    </div>
  </div>
</div>

<!-- Receipt Modal -->
<div class="modal-overlay" id="modal-receipt">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">🧾 Payment Receipt</div>
      <button class="modal-close" onclick="closeModal('modal-receipt')">✕</button>
    </div>
    <div class="receipt" id="receipt-content"></div>
    <div class="form-actions">
      <button class="btn btn-ghost" onclick="closeModal('modal-receipt')">Close</button>
      <button class="btn btn-primary" onclick="window.print()">🖨️ Print Receipt</button>
    </div>
  </div>
</div>

<!-- Confirm Distribute Modal -->
<div class="modal-overlay" id="modal-confirm-dist">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">✨ Confirm Distribution</div>
      <button class="modal-close" onclick="closeModal('modal-confirm-dist')">✕</button>
    </div>
    <div id="dist-confirm-body" style="font-size:14px;color:var(--gray-400);line-height:1.7;"></div>
    <div class="form-actions">
      <button class="btn btn-ghost" onclick="closeModal('modal-confirm-dist')">Cancel</button>
      <button class="btn btn-teal" onclick="doDistribute()">✅ Confirm Distribute</button>
    </div>
  </div>
</div>

<!-- Delete Confirm -->
<div class="modal-overlay" id="modal-delete">
  <div class="modal" style="max-width:400px;">
    <div class="modal-header">
      <div class="modal-title" style="color:#fc8181;">⚠️ Delete Member</div>
      <button class="modal-close" onclick="closeModal('modal-delete')">✕</button>
    </div>
    <p style="font-size:14px;color:var(--gray-400);line-height:1.7;">Are you sure you want to delete <strong id="delete-member-name" style="color:var(--white);"></strong>? This action cannot be undone.</p>
    <div class="form-actions">
      <button class="btn btn-ghost" onclick="closeModal('modal-delete')">Cancel</button>
      <button class="btn btn-danger" onclick="confirmDelete()">🗑️ Delete</button>
    </div>
  </div>
</div>

<!-- Reset All Data Modal -->
<div class="modal-overlay" id="modal-reset">
  <div class="modal" style="max-width:420px;">
    <div class="modal-header">
      <div class="modal-title" style="color:#fc8181;">⚠️ Reset All Data</div>
      <button class="modal-close" onclick="closeModal('modal-reset')">✕</button>
    </div>
    <p style="font-size:14px;color:var(--gray-400);line-height:1.8;margin-bottom:10px;">
      This will <strong style="color:#fc8181;">permanently delete</strong> all of the following:
    </p>
    <ul style="font-size:13.5px;color:var(--gray-400);line-height:2;padding-left:20px;margin-bottom:14px;">
      <li>All <strong style="color:var(--white);">Members</strong></li>
      <li>All <strong style="color:var(--white);">Contributions</strong></li>
      <li>All <strong style="color:var(--white);">Loans &amp; Payments</strong></li>
      <li>All <strong style="color:var(--white);">Transaction Logs</strong></li>
      <li>All <strong style="color:var(--white);">Interest Distribution History</strong></li>
      <li>All <strong style="color:var(--white);">Dashboard Statistics</strong></li>
    </ul>
    <p style="font-size:13px;color:#fc8181;font-weight:600;">This action cannot be undone. The system will start completely blank.</p>
    <div style="margin-top:18px;">
      <label style="font-size:12px;margin-bottom:8px;display:block;">Type <strong style="color:var(--white);font-family:monospace;">RESET</strong> to confirm:</label>
      <input type="text" id="reset-confirm-input" placeholder="Type RESET here" style="margin-bottom:0;">
    </div>
    <div class="form-actions">
      <button class="btn btn-ghost" onclick="closeModal('modal-reset')">Cancel</button>
      <button class="btn btn-danger" onclick="doResetAll()">🗑️ Delete Everything</button>
    </div>
  </div>
</div>

<!-- Edit Contribution Modal -->
<div class="modal-overlay" id="modal-edit-contribution">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">✏️ Edit Contribution</div>
      <button class="modal-close" onclick="closeModal('modal-edit-contribution')">✕</button>
    </div>
    <input type="hidden" id="ec-id">
    <div style="background:rgba(245,166,35,0.08);border:1px solid rgba(245,166,35,0.25);border-radius:10px;padding:12px 14px;margin-bottom:14px;font-size:12.5px;color:var(--gold-light);">
      ⚠️ Editing will adjust the member's total contribution balance. Admin only.
    </div>
    <div class="form-group">
      <label>Member</label>
      <input type="text" id="ec-member" disabled style="opacity:0.6;">
    </div>
    <div class="form-row">
      <div class="form-group">
        <label>Original Amount</label>
        <input type="text" id="ec-old-amount" disabled style="opacity:0.6;">
      </div>
      <div class="form-group">
        <label>New Amount (₱)</label>
        <input type="number" id="ec-amount" placeholder="0.00" min="0.01" step="0.01">
      </div>
    </div>
    <div class="form-row">
      <div class="form-group">
        <label>Date</label>
        <input type="date" id="ec-date">
      </div>
      <div class="form-group">
        <label>Collector</label>
        <input type="text" id="ec-collector" placeholder="Name of collector">
      </div>
    </div>
    <div class="form-actions">
      <button class="btn btn-ghost" onclick="closeModal('modal-edit-contribution')">Cancel</button>
      <button class="btn btn-gold" onclick="saveEditContribution()">💾 Save Correction</button>
    </div>
  </div>
</div>

<!-- Edit Loan Modal -->
<div class="modal-overlay" id="modal-edit-loan">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">✏️ Edit Loan Record</div>
      <button class="modal-close" onclick="closeModal('modal-edit-loan')">✕</button>
    </div>
    <input type="hidden" id="el-id">
    <div style="background:rgba(245,166,35,0.08);border:1px solid rgba(245,166,35,0.25);border-radius:10px;padding:12px 14px;margin-bottom:14px;font-size:12.5px;color:var(--gold-light);">
      ⚠️ Editing the principal will recalculate interest (5%) and adjust member contribution & interest pool. Admin only.
    </div>
    <div class="form-group">
      <label>Member</label>
      <input type="text" id="el-member" disabled style="opacity:0.6;">
    </div>
    <div class="form-row">
      <div class="form-group">
        <label>Original Principal</label>
        <input type="text" id="el-old-principal" disabled style="opacity:0.6;">
      </div>
      <div class="form-group">
        <label>New Principal (₱)</label>
        <input type="number" id="el-principal" placeholder="0.00" min="1" step="0.01" oninput="previewLoanEdit()">
      </div>
    </div>
    <div class="form-group">
      <label>Date</label>
      <input type="date" id="el-date">
    </div>
    <div class="loan-preview" id="el-preview" style="display:none;">
      <div class="loan-preview-row"><span>New Principal:</span><span id="el-p-principal" class="td-mono"></span></div>
      <div class="loan-preview-row"><span>New Interest (5%):</span><span id="el-p-interest" class="td-mono" style="color:var(--gold-light)"></span></div>
      <div class="loan-preview-row total"><span>New Total Loan:</span><span id="el-p-total" class="td-mono"></span></div>
    </div>
    <div class="form-actions">
      <button class="btn btn-ghost" onclick="closeModal('modal-edit-loan')">Cancel</button>
      <button class="btn btn-gold" onclick="saveEditLoan()">💾 Save Correction</button>
    </div>
  </div>
</div>

<!-- Edit Payment Modal -->
<div class="modal-overlay" id="modal-edit-payment">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">✏️ Edit Payment Record</div>
      <button class="modal-close" onclick="closeModal('modal-edit-payment')">✕</button>
    </div>
    <input type="hidden" id="ep-id">
    <div style="background:rgba(245,166,35,0.08);border:1px solid rgba(245,166,35,0.25);border-radius:10px;padding:12px 14px;margin-bottom:14px;font-size:12.5px;color:var(--gold-light);">
      ⚠️ Editing will adjust loan balance and member active loan. Admin only.
    </div>
    <div class="form-group">
      <label>Member</label>
      <input type="text" id="ep-member" disabled style="opacity:0.6;">
    </div>
    <div class="form-row">
      <div class="form-group">
        <label>Original Amount</label>
        <input type="text" id="ep-old-amount" disabled style="opacity:0.6;">
      </div>
      <div class="form-group">
        <label>New Amount (₱)</label>
        <input type="number" id="ep-amount" placeholder="0.00" min="0.01" step="0.01">
      </div>
    </div>
    <div class="form-row">
      <div class="form-group">
        <label>Payment Type</label>
        <select id="ep-type">
          <option value="interest_only">Interest Only</option>
          <option value="principal_only">Principal Only</option>
          <option value="principal_interest">Principal + Interest (Full)</option>
        </select>
      </div>
      <div class="form-group">
        <label>Date</label>
        <input type="date" id="ep-date">
      </div>
    </div>
    <div class="form-actions">
      <button class="btn btn-ghost" onclick="closeModal('modal-edit-payment')">Cancel</button>
      <button class="btn btn-gold" onclick="saveEditPayment()">💾 Save Correction</button>
    </div>
  </div>
</div>

<div id="toast-container"></div>

<script>
// ================================================================
// ⚙️ GOOGLE SHEETS API URL
// Paste your Apps Script Web App URL below after deploying
// ================================================================
const SCRIPT_URL = 'YOUR_APPS_SCRIPT_URL_HERE';

// ================================================================
// IN-MEMORY DATA (loaded fresh from Google Sheets on login)
// ================================================================
let members = [];
let contributions = [];
let loans = [];
let payments = [];
let transactions = [];
let distHistory = [];
let settings = { interestPool: 0, totalDistributed: 0, dailyRatePerHead: 5 };

// ================================================================
// GOOGLE SHEETS API LAYER
// ================================================================
async function api(action, data={}) {
  try {
    // Build URL with action as query param (GET-style) for CORS compatibility
    const url = SCRIPT_URL + '?action=' + encodeURIComponent(action);
    const res = await fetch(url, {
      method: 'POST',
      body: JSON.stringify({ action, ...data }),
      headers: { 'Content-Type': 'text/plain;charset=utf-8' }
    });
    const text = await res.text();
    // Apps Script sometimes returns HTML on auth errors
    if (text.trim().startsWith('<')) {
      throw new Error('Apps Script returned an HTML page. Please check deployment settings — make sure "Who has access" is set to "Anyone".');
    }
    const json = JSON.parse(text);
    if (!json.success) throw new Error(json.error || 'API error');
    return json;
  } catch(err) {
    console.error('API Error:', err);
    toast('⚠️ ' + err.message, 'error');
    throw err;
  }
}

async function loadAllData() {
  showLoading(true);
  try {
    const res = await api('getAll');
    const d = res.data;
    members       = (d.members || []).map(migrateM);
    contributions = (d.contributions || []).map(migrateC);
    loans         = d.loans || [];
    payments      = d.payments || [];
    transactions  = d.transactions || [];
    distHistory   = d.distHistory || [];
    settings      = { interestPool:0, totalDistributed:0, dailyRatePerHead:5, ...(d.settings||{}) };
    // Normalize number fields
    members = members.map(m => ({
      ...m,
      heads: parseInt(m.heads)||1,
      total_contribution: parseFloat(m.total_contribution)||0,
      active_loan: parseFloat(m.active_loan)||0,
      total_interest_earned: parseFloat(m.total_interest_earned)||0
    }));
    loans = loans.map(l => ({
      ...l,
      principal: parseFloat(l.principal)||0,
      interest: parseFloat(l.interest)||0,
      total_amount: parseFloat(l.total_amount)||0,
      remaining_balance: parseFloat(l.remaining_balance)||0
    }));
    payments = payments.map(p => ({ ...p, amount: parseFloat(p.amount)||0 }));
    contributions = contributions.map(c => ({ ...c, amount: parseFloat(c.amount)||0, heads: parseInt(c.heads)||1 }));
    settings.interestPool = parseFloat(settings.interestPool)||0;
    settings.totalDistributed = parseFloat(settings.totalDistributed)||0;
    settings.dailyRatePerHead = parseFloat(settings.dailyRatePerHead)||5;
  } finally {
    showLoading(false);
  }
}

function migrateM(m) {
  return { heads:1, active_loan:0, total_interest_earned:0, status:'Active', joined: today(), ...m };
}
function migrateC(c) {
  return { heads:1, ...c };
}

async function logTx(type, desc, memberName, amount) {
  const tx = { id: genId('TX'), type, desc, member: memberName||'-', amount: amount||0, date: new Date().toISOString() };
  transactions.unshift(tx);
  if (transactions.length > 500) transactions = transactions.slice(0, 500);
  try { await api('logTransaction', { data: tx }); } catch(e) { /* non-blocking */ }
}

// Loading overlay
function showLoading(show, msg='Loading data...') {
  let el = document.getElementById('loading-overlay');
  if (!el) {
    el = document.createElement('div');
    el.id = 'loading-overlay';
    el.style.cssText = 'position:fixed;inset:0;z-index:9999;background:rgba(10,22,40,0.85);display:flex;flex-direction:column;align-items:center;justify-content:center;gap:16px;backdrop-filter:blur(6px);';
    el.innerHTML = '<div style="font-size:40px;animation:spin 1s linear infinite;">⟳</div><div style="font-size:16px;font-weight:600;color:#f8faff;">'+msg+'</div><div style="font-size:12px;color:#7a8fb5;">Connecting to Google Sheets...</div><style>@keyframes spin{from{transform:rotate(0)}to{transform:rotate(360deg)}}</style>';
    document.body.appendChild(el);
  }
  el.style.display = show ? 'flex' : 'none';
}

let currentUser = null;
let deleteMemberIdPending = null;

const USERS = {
  admin: { pass: 'admin123', role: 'Administrator', name: 'Admin' },
  treasurer: { pass: 'vault456', role: 'Treasurer', name: 'Treasurer' },
  member: { pass: 'member789', role: 'Member', name: 'Member' }
};

// Permission helper
function isAdmin() { return currentUser?.role === 'Administrator'; }
function isTreasurer() { return currentUser?.role === 'Treasurer'; }
function canWrite() { return currentUser?.role === 'Administrator' || currentUser?.role === 'Treasurer'; }
function isMemberOnly() { return currentUser?.role === 'Member'; }

// ================================================================
// AUTH
// ================================================================
function doLogin() {
  const u = document.getElementById('login-user').value.trim().toLowerCase();
  const p = document.getElementById('login-pass').value;
  if (USERS[u] && USERS[u].pass === p) {
    currentUser = { username: u, ...USERS[u] };
    document.getElementById('login-page').style.display = 'none';
    document.getElementById('user-display').textContent = USERS[u].name;
    document.getElementById('user-role').textContent = USERS[u].role;
    document.getElementById('user-avatar-text').textContent = USERS[u].name[0].toUpperCase();
    applyRoleUI();
    initApp();
  } else {
    document.getElementById('login-error').style.display = 'block';
  }
}

function applyRoleUI() {
  const memberOnly = isMemberOnly();

  // Show/hide admin-only elements
  document.querySelectorAll('.admin-only').forEach(el => {
    el.style.display = memberOnly ? 'none' : '';
  });
  // Show/hide write-only elements (buttons to add/edit)
  document.querySelectorAll('.write-only').forEach(el => {
    el.style.display = memberOnly ? 'none' : '';
  });
  // Show member-only messages (view restrictions notice)
  document.querySelectorAll('.member-only-msg').forEach(el => {
    el.style.display = memberOnly ? 'block' : 'none';
  });

  // Show/hide member quick view panel
  const mqv = document.getElementById('member-quick-view');
  if (mqv) mqv.style.display = memberOnly ? 'block' : 'none';

  // Show member banner
  const banner = document.getElementById('member-banner');
  if (banner) banner.style.display = memberOnly ? 'flex' : 'none';
  if (badge) badge.style.display = memberOnly ? 'flex' : 'none';

  // Color-code user role in sidebar
  const roleEl = document.getElementById('user-role');
  if (roleEl) {
    roleEl.style.color = memberOnly ? 'var(--teal)' : 'var(--gold)';
  }
}

// Guard against member accessing restricted pages
function guardPage(id) {
  if (isMemberOnly() && (id === 'datamanager')) {
    toast('Access restricted for Member accounts.', 'error');
    showPage('dashboard');
    return true;
  }
  return false;
}

function doLogout() {
  currentUser = null;
  document.getElementById('login-page').style.display = 'flex';
  document.getElementById('login-user').value = '';
  document.getElementById('login-pass').value = '';
  document.getElementById('login-error').style.display = 'none';
}

// ================================================================
// APP INIT
// ================================================================
async function initApp() {
  updateTopbarDate();
  setInterval(updateTopbarDate, 60000);
  if (SCRIPT_URL === 'YOUR_APPS_SCRIPT_URL_HERE') {
    toast('⚠️ Please set your SCRIPT_URL at the top of the HTML file!', 'error');
    showPage('dashboard');
    return;
  }
  try {
    await loadAllData();
    toast('✅ Connected to Google Sheets!', 'success');
  } catch(e) {
    toast('❌ Failed to load data. Check your SCRIPT_URL.', 'error');
  }
  showPage('dashboard');
}

function openResetConfirm() {
  if (isMemberOnly()) { toast('👁️ View Only: You cannot perform this action.', 'warn'); return; }
  document.getElementById('reset-confirm-input').value = '';
  openModal('modal-reset');
}

async function doResetAll() {
  const input = document.getElementById('reset-confirm-input').value.trim();
  if (input !== 'RESET') { toast('You must type RESET to confirm.', 'error'); return; }
  showLoading(true, 'Resetting all data...');
  try {
    await api('resetAll');
    members = []; contributions = []; loans = []; payments = [];
    transactions = []; distHistory = [];
    settings = { interestPool: 0, totalDistributed: 0, dailyRatePerHead: 5 };
    closeModal('modal-reset');
    toast('All data has been reset.', 'warn');
    showPage('dashboard');
  } finally { showLoading(false); }
}

function updateTopbarDate() {
  const now = new Date();
  document.getElementById('topbar-date').textContent =
    now.toLocaleDateString('en-PH', { weekday:'long', year:'numeric', month:'long', day:'numeric' }) +
    ' | ' + now.toLocaleTimeString('en-PH', { hour:'2-digit', minute:'2-digit' });
}

// ================================================================
// NAVIGATION
// ================================================================
function showPage(id) {
  if (guardPage && guardPage(id)) return;
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  document.getElementById('page-' + id).classList.add('active');
  document.querySelectorAll('.nav-item').forEach(n => {
    if (n.textContent.toLowerCase().includes(id.substring(0,5))) n.classList.add('active');
  });
  const titles = {
    dashboard:'Dashboard', members:'Member Management', contributions:'Weekly Contributions',
    loans:'Loan Management', payments:'Payment Records', interest:'Interest Pool',
    reports:'Reports', transactions:'Transaction Log', datamanager:'Data Backup & Restore'
  };
  document.getElementById('page-title').textContent = titles[id] || id;

  if (id==='dashboard') refreshDashboard();
  else if (id==='members') renderMembers();
  else if (id==='contributions') renderContributions();
  else if (id==='loans') renderLoans();
  else if (id==='payments') renderPayments();
  else if (id==='interest') renderInterest();
  else if (id==='transactions') renderTransactions();
  else if (id==='datamanager') renderDataManager();
}

// ================================================================
// MODALS
// ================================================================
function openModal(id) {
  // Block write modals for member-only accounts
  const writeModals = ['modal-add-member','modal-contribution','modal-loan','modal-payment','modal-confirm-dist','modal-reset','modal-edit-contribution','modal-edit-loan','modal-edit-payment'];
  if (isMemberOnly() && writeModals.includes(id)) {
    toast('👁️ View Only: You cannot perform this action.', 'warn');
    return;
  }
  if (id==='modal-contribution') {
    populateMemberDropdown('contribution-member');
    document.getElementById('contribution-date').valueAsDate = new Date();
    document.getElementById('contribution-preview').style.display='none';
    document.getElementById('contribution-amount').value = '';
    setTimeout(onContributionMemberChange, 50);
  }
  if (id==='modal-loan') {
    populateMemberDropdown('loan-member');
    document.getElementById('loan-date').valueAsDate = new Date();
    document.getElementById('loan-preview').style.display='none';
  }
  if (id==='modal-add-member') { resetMemberForm(); }
  document.getElementById(id).classList.add('open');
}

function closeModal(id) { document.getElementById(id).classList.remove('open'); }

// ================================================================
// TOAST
// ================================================================
function toast(msg, type='success') {
  const icons = { success:'✅', error:'❌', info:'ℹ️', warn:'⚠️' };
  const el = document.createElement('div');
  el.className = `toast toast-${type}`;
  el.innerHTML = `<span>${icons[type]}</span> ${msg}`;
  document.getElementById('toast-container').appendChild(el);
  setTimeout(() => el.remove(), 3500);
}

// ================================================================
// HELPERS
// ================================================================
const fmt = (n) => '₱' + parseFloat(n||0).toLocaleString('en-PH', { minimumFractionDigits:2, maximumFractionDigits:2 });
const genId = (prefix) => prefix + Date.now().toString(36).toUpperCase() + Math.random().toString(36).substr(2,3).toUpperCase();
const today = () => new Date().toISOString().split('T')[0];
const fmtDate = (d) => new Date(d).toLocaleDateString('en-PH', { year:'numeric', month:'short', day:'numeric' });
const fmtDateTime = (d) => new Date(d).toLocaleString('en-PH', { year:'numeric', month:'short', day:'numeric', hour:'2-digit', minute:'2-digit' });

// save() is now a no-op — all writes go directly to Google Sheets via api()
function save() { /* data is saved per-operation via api() calls */ }

// ================================================================
// DATA BACKUP / EXPORT (still useful as local backup)
// ================================================================
function getAllData() {
  return { members, contributions, loans, payments, transactions, distHistory, settings, exportedAt: new Date().toISOString(), version: 'nsv-sheets-v1' };
}

function exportData() {
  const data = JSON.stringify(getAllData(), null, 2);
  const blob = new Blob([data], { type: 'application/json' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = `nunez-vault-backup-${today()}.json`;
  a.click();
  URL.revokeObjectURL(url);
  toast('Data exported successfully!', 'success');
}

function copyDataToClipboard() {
  const data = JSON.stringify(getAllData());
  navigator.clipboard.writeText(data).then(() => {
    toast('Data copied to clipboard!', 'success');
  }).catch(() => {
    // Fallback
    const ta = document.getElementById('data-json-view');
    ta.select();
    document.execCommand('copy');
    toast('Data copied! (fallback method)', 'info');
  });
}

let importedData = null;

function previewImport(input) {
  const file = input.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = (e) => {
    try {
      importedData = JSON.parse(e.target.result);
      const preview = document.getElementById('import-preview');
      preview.style.display = 'block';
      preview.innerHTML = `
        ✅ Valid backup file detected:<br>
        👥 ${(importedData.members||[]).length} members &nbsp;|&nbsp;
        💰 ${(importedData.contributions||[]).length} contributions &nbsp;|&nbsp;
        🏷️ ${(importedData.loans||[]).length} loans<br>
        💳 ${(importedData.payments||[]).length} payments &nbsp;|&nbsp;
        📅 Exported: ${importedData.exportedAt ? fmtDate(importedData.exportedAt) : 'Unknown'}
      `;
    } catch(err) {
      importedData = null;
      toast('Invalid backup file. Please use a file exported from this system.', 'error');
    }
  };
  reader.readAsText(file);
}

async function importData() {
  if (!importedData) { toast('Please select a valid backup file first.', 'error'); return; }
  if (!confirm('This will REPLACE ALL current data with the backup. Are you sure?')) return;
  showLoading(true, 'Restoring backup...');
  try {
    await api('resetAll');
    // Re-add all data record by record
    for (const m of (importedData.members||[])) { await api('addMember', { data: m }); }
    for (const c of (importedData.contributions||[])) { await api('addContribution', { data: { ...c, skipMemberUpdate: true } }); }
    for (const l of (importedData.loans||[])) { await api('addLoan', { data: l }); }
    for (const p of (importedData.payments||[])) { await api('addPayment', { data: p }); }
    if (importedData.settings) await api('updateSettings', { data: importedData.settings });
    // Reload fresh
    await loadAllData();
    importedData = null;
    document.getElementById('import-file').value = '';
    document.getElementById('import-preview').style.display = 'none';
    toast('Backup restored successfully!', 'success');
    refreshDashboard();
    renderDataManager();
  } finally { showLoading(false); }
}

function renderDataManager() {
  const summary = document.getElementById('export-summary');
  if (summary) {
    summary.innerHTML = `
      👥 <strong>${members.length}</strong> members &nbsp;|&nbsp;
      💰 <strong>${contributions.length}</strong> contributions<br>
      🏷️ <strong>${loans.length}</strong> loans &nbsp;|&nbsp;
      💳 <strong>${payments.length}</strong> payments<br>
      ✨ Interest Pool: <strong>${fmt(settings.interestPool)}</strong>
    `;
  }
  const jsonView = document.getElementById('data-json-view');
  if (jsonView) {
    jsonView.value = JSON.stringify(getAllData(), null, 2);
  }
}

// ================================================================
// MEMBERS
// ================================================================
async function addMember(name, initial=0, status='Active', heads=1, notify=true) {
  const m = {
    id: genId('MBR'),
    name,
    heads: parseInt(heads)||1,
    total_contribution: parseFloat(initial)||0,
    active_loan: 0,
    total_interest_earned: 0,
    status,
    joined: today()
  };
  await api('addMember', { data: m });
  members.push(m);
  await logTx('Member', `New member added: ${name} (${m.heads} head${m.heads>1?'s':''})`, name, 0);
  if (notify) toast(`Member "${name}" added!`, 'success');
  return m;
}

async function saveMember() {
  const name = document.getElementById('member-name').value.trim();
  const initial = parseFloat(document.getElementById('member-initial').value)||0;
  const status = document.getElementById('member-status').value;
  const heads = parseInt(document.getElementById('member-heads').value)||1;
  const editId = document.getElementById('edit-member-id').value;

  if (!name) { toast('Please enter member name.', 'error'); return; }

  showLoading(true, 'Saving member...');
  try {
    if (editId) {
      const m = members.find(x => x.id === editId);
      if (m) {
        m.name = name; m.status = status; m.heads = heads;
        await api('updateMember', { data: m });
        await logTx('Member', `Member updated: ${name} (${heads} head${heads>1?'s':''})`, name, 0);
        toast(`Member "${name}" updated!`, 'success');
      }
    } else {
      const newM = await addMember(name, initial, status, heads);
      if (initial > 0) {
        const c = { id: genId('CTB'), member_id: newM.id, member_name: name, amount: initial, heads: heads, date: today(), collector: currentUser.name };
        contributions.push(c);
        await api('addContribution', { data: { ...c, skipMemberUpdate: true } });
      }
    }
  } finally { showLoading(false); }
  closeModal('modal-add-member');
  renderMembers();
  refreshDashboard();
}

function resetMemberForm() {
  document.getElementById('member-modal-title').textContent = '➕ Add New Member';
  document.getElementById('edit-member-id').value = '';
  document.getElementById('member-name').value = '';
  document.getElementById('member-initial').value = '';
  document.getElementById('member-status').value = 'Active';
  document.getElementById('member-heads').value = '1';
  updateHeadsPreview();
}

function editMember(id) {
  const m = members.find(x => x.id===id);
  if (!m) return;
  document.getElementById('member-modal-title').textContent = '✏️ Edit Member';
  document.getElementById('edit-member-id').value = m.id;
  document.getElementById('member-name').value = m.name;
  document.getElementById('member-initial').value = m.total_contribution;
  document.getElementById('member-status').value = m.status;
  document.getElementById('member-heads').value = m.heads||1;
  updateHeadsPreview();
  openModal('modal-add-member');
}

function deleteMember(id) {
  const m = members.find(x=>x.id===id);
  if (!m) return;
  deleteMemberIdPending = id;
  document.getElementById('delete-member-name').textContent = m.name;
  openModal('modal-delete');
}

async function confirmDelete() {
  if (!deleteMemberIdPending) return;
  const m = members.find(x=>x.id===deleteMemberIdPending);
  if (m) {
    showLoading(true, 'Deleting member...');
    try {
      await api('deleteMember', { id: deleteMemberIdPending });
      members = members.filter(x=>x.id!==deleteMemberIdPending);
      await logTx('Member', `Member deleted: ${m.name}`, m.name, 0);
      toast(`Member "${m.name}" deleted.`, 'warn');
      renderMembers();
      refreshDashboard();
    } finally { showLoading(false); }
  }
  closeModal('modal-delete');
  deleteMemberIdPending = null;
}

function renderMembers(filter='') {
  const tbody = document.getElementById('members-tbody');
  const list = filter ? members.filter(m => m.name.toLowerCase().includes(filter.toLowerCase())) : members;
  if (!list.length) { tbody.innerHTML = `<tr><td colspan="8"><div class="empty-state"><div class="icon">👥</div><p>No members found.</p></div></td></tr>`; return; }
  tbody.innerHTML = list.map(m => `
    <tr>
      <td><span class="badge badge-blue">${m.id}</span></td>
      <td><strong>${m.name}</strong></td>
      <td style="text-align:center;"><span class="badge badge-gold" style="font-size:13px;padding:4px 14px;">${m.heads||1} 🧑</span></td>
      <td class="td-mono" style="color:var(--teal)">${fmt(m.total_contribution)}</td>
      <td class="td-mono" style="color:${m.active_loan>0?'#fc8181':'var(--gray-400)'}">${fmt(m.active_loan)}</td>
      <td class="td-mono" style="color:var(--gold-light)">${fmt(m.total_interest_earned)}</td>
      <td><span class="badge ${m.status==='Active'?'badge-green':'badge-gray'}">${m.status}</span></td>
      <td>
        ${canWrite() ? `<button class="btn btn-ghost btn-sm" onclick="editMember('${m.id}')">✏️</button>
        <button class="btn btn-danger btn-sm" style="margin-left:6px;" onclick="deleteMember('${m.id}')">🗑️</button>` : '<span style="color:var(--gray-600);font-size:12px;">—</span>'}
      </td>
    </tr>
  `).join('');
}

function filterMembers(val) { renderMembers(val); }

// ================================================================
// CONTRIBUTIONS
// ================================================================
function populateMemberDropdown(selectId) {
  const sel = document.getElementById(selectId);
  sel.innerHTML = members.filter(m=>m.status==='Active').map(m =>
    `<option value="${m.id}">${m.name} (${m.heads||1} head${(m.heads||1)>1?'s':''})</option>`
  ).join('');
}

function calcContribution() {
  const memberId = document.getElementById('contribution-member').value;
  const m = members.find(x=>x.id===memberId);
  if (!m) { document.getElementById('contribution-preview').style.display='none'; return; }
  const heads = m.heads || 1;
  const dailyRate = settings.dailyRatePerHead || 5;
  const weeklyPerHead = dailyRate * 7;
  const autoAmount = weeklyPerHead * heads;
  const amountField = document.getElementById('contribution-amount');
  if (!amountField.value) amountField.value = autoAmount.toFixed(2);
  const amount = parseFloat(amountField.value)||0;
  if (!amount) { document.getElementById('contribution-preview').style.display='none'; return; }
  document.getElementById('cp-heads').textContent = `₱${dailyRate}/day × 7 days × ${heads} head${heads>1?'s':''} = ${fmt(autoAmount)}`;
  document.getElementById('cp-current').textContent = fmt(m.total_contribution);
  document.getElementById('cp-adding').textContent = '+' + fmt(amount);
  document.getElementById('cp-new').textContent = fmt(m.total_contribution + amount);
  document.getElementById('contribution-preview').style.display = 'block';
}

function updateHeadsPreview() {
  const heads = parseInt(document.getElementById('member-heads').value)||1;
  const dailyRate = settings.dailyRatePerHead || 5;
  const weeklyPerHead = dailyRate * 7;
  const weeklyTotal = weeklyPerHead * heads;
  document.getElementById('heads-preview').textContent =
    `₱${dailyRate}/day × 7 days = ₱${weeklyPerHead}/head/week  →  ₱${weeklyPerHead} × ${heads} head${heads>1?'s':''} = ₱${weeklyTotal.toFixed(2)}/week`;
}

async function updateRatePerHead(val) {
  const rate = parseFloat(val)||5;
  settings.dailyRatePerHead = rate;
  try { await api('updateSettings', { data: { dailyRatePerHead: rate } }); } catch(e) { /* non-blocking */ }
  renderInterest();
  refreshDashboard();
  updateHeadsPreview();
  toast(`Daily rate updated to ₱${rate}/head/day  →  ₱${(rate*7).toFixed(2)}/head/week`, 'info');
}

function onContributionMemberChange() {
  const memberId = document.getElementById('contribution-member').value;
  const m = members.find(x=>x.id===memberId);
  document.getElementById('contribution-amount').value = '';
  if (m) {
    const heads = m.heads||1;
    const dailyRate = settings.dailyRatePerHead||5;
    const weeklyPerHead = dailyRate * 7;
    const weeklyTotal = weeklyPerHead * heads;
    document.getElementById('c-heads-badge').textContent =
      `${heads} head${heads>1?'s':''} — ₱${dailyRate}/day × 7 days × ${heads} = ₱${weeklyTotal.toFixed(2)}/week`;
    document.getElementById('contribution-heads-info').style.display='block';
  } else {
    document.getElementById('contribution-heads-info').style.display='none';
  }
  calcContribution();
}

async function saveContribution() {
  const memberId = document.getElementById('contribution-member').value;
  const amount = parseFloat(document.getElementById('contribution-amount').value);
  const date = document.getElementById('contribution-date').value || today();
  const collector = document.getElementById('contribution-collector').value.trim() || currentUser.name;
  const m = members.find(x=>x.id===memberId);
  if (!m) { toast('Select a member.', 'error'); return; }
  if (!amount || amount <= 0) { toast('Enter valid amount.', 'error'); return; }
  const heads = m.heads || 1;
  const c = { id: genId('CTB'), member_id: memberId, member_name: m.name, heads: heads, amount, date, collector };
  showLoading(true, 'Recording contribution...');
  try {
    await api('addContribution', { data: c });
    m.total_contribution += amount;
    contributions.push(c);
    await logTx('Contribution', `Contribution: ${m.name} (${heads} head${heads>1?'s':''}) → ${fmt(amount)}`, m.name, amount);
    toast(`Contribution of ${fmt(amount)} recorded for ${m.name}!`, 'success');
    closeModal('modal-contribution');
    renderContributions();
    refreshDashboard();
  } finally { showLoading(false); }
}

function renderContributions() {
  const tbody = document.getElementById('contributions-tbody');
  if (!contributions.length) { tbody.innerHTML = `<tr><td colspan="7"><div class="empty-state"><div class="icon">💰</div><p>No contributions yet.</p></div></td></tr>`; return; }
  tbody.innerHTML = [...contributions].reverse().map((c, i) => `
    <tr class="${c.corrected?'corrected-row':''}">
      <td>${contributions.length - i}</td>
      <td><strong>${c.member_name}</strong>${c.corrected?'<span class="badge-corrected">corrected</span>':''}</td>
      <td style="text-align:center;"><span class="badge badge-gold">${c.heads||1} 🧑</span></td>
      <td class="td-mono" style="color:var(--teal)">${fmt(c.amount)}</td>
      <td>${fmtDate(c.date)}</td>
      <td>${c.collector||'-'}</td>
      <td>${currentUser?.role==='Administrator'?`<button class="btn btn-ghost btn-sm" onclick="openEditContribution('${c.id}')">✏️ Edit</button>`:canWrite()?'<span style="color:var(--gray-600);font-size:11px;">Admin only</span>':'<span style="color:var(--gray-600);font-size:12px;">—</span>'}</td>
    </tr>
  `).join('');
}

// ================================================================
// LOANS
// ================================================================
function calcLoan() {
  const memberId = document.getElementById('loan-member').value;
  const principal = parseFloat(document.getElementById('loan-principal').value)||0;
  const m = members.find(x=>x.id===memberId);
  if (!m || !principal) { document.getElementById('loan-preview').style.display='none'; return; }
  const interest = principal * 0.05;
  const total = principal + interest;
  document.getElementById('lp-principal').textContent = fmt(principal);
  document.getElementById('lp-interest').textContent = fmt(interest);
  document.getElementById('lp-total').textContent = fmt(total);
  document.getElementById('lp-contrib').textContent = fmt(m.total_contribution);
  document.getElementById('lp-after').textContent = fmt(m.total_contribution - principal);
  document.getElementById('loan-preview').style.display = 'block';
}

async function saveLoan() {
  const memberId = document.getElementById('loan-member').value;
  const principal = parseFloat(document.getElementById('loan-principal').value);
  const date = document.getElementById('loan-date').value || today();
  const m = members.find(x=>x.id===memberId);
  if (!m) { toast('Select a member.', 'error'); return; }
  if (!principal || principal <= 0) { toast('Enter valid principal amount.', 'error'); return; }
  if (principal > m.total_contribution) { toast(`Principal exceeds contribution! Max: ${fmt(m.total_contribution)}`, 'error'); return; }
  const interest = principal * 0.05;
  const total = principal + interest;
  const loan = { id: genId('LN'), member_id: memberId, member_name: m.name, principal, interest, total_amount: total, remaining_balance: total, status: 'Active', date };
  showLoading(true, 'Issuing loan...');
  try {
    await api('addLoan', { data: loan });
    loans.push(loan);
    m.total_contribution -= principal;
    m.active_loan += total;
    settings.interestPool += interest;
    await logTx('Loan', `Loan issued to ${m.name} | Principal: ${fmt(principal)} | Interest: ${fmt(interest)}`, m.name, total);
    toast(`Loan of ${fmt(total)} issued to ${m.name}!`, 'success');
    closeModal('modal-loan');
    renderLoans();
    refreshDashboard();
  } finally { showLoading(false); }
}

function renderLoans() {
  const tbody = document.getElementById('loans-tbody');
  if (!loans.length) { tbody.innerHTML = `<tr><td colspan="10"><div class="empty-state"><div class="icon">🏷️</div><p>No loans yet.</p></div></td></tr>`; return; }
  tbody.innerHTML = [...loans].reverse().map(l => `
    <tr class="${l.corrected?'corrected-row':''}">
      <td><span class="badge badge-gold" style="font-size:10px;">${l.id}</span>${l.corrected?'<span class="badge-corrected">corrected</span>':''}</td>
      <td><strong>${l.member_name}</strong></td>
      <td class="td-mono">${fmt(l.principal)}</td>
      <td class="td-mono" style="color:var(--gold-light)">${fmt(l.interest)}</td>
      <td class="td-mono">${fmt(l.total_amount)}</td>
      <td class="td-mono" style="color:${l.remaining_balance>0?'#fc8181':'var(--green-light)'}">${fmt(l.remaining_balance)}</td>
      <td><span class="badge ${l.status==='Active'?'badge-red':'badge-green'}">${l.status}</span></td>
      <td>${fmtDate(l.date)}</td>
      <td>${l.status==='Active' && canWrite() ?`<button class="btn btn-primary btn-sm" onclick="openPaymentModal('${l.id}')">💳 Pay</button>`:'—'}</td>
      <td>${currentUser?.role==='Administrator'?`<button class="btn btn-ghost btn-sm" onclick="openEditLoan('${l.id}')">✏️</button>`:canWrite()?'<span style="color:var(--gray-600);font-size:11px;">Admin only</span>':'—'}</td>
    </tr>
  `).join('');
}

// ================================================================
// PAYMENTS
// ================================================================
function openPaymentModal(loanId) {
  const l = loans.find(x=>x.id===loanId);
  if (!l) return;
  document.getElementById('payment-loan-id').value = loanId;
  document.getElementById('payment-date').valueAsDate = new Date();
  document.getElementById('payment-preview').style.display = 'none';
  document.getElementById('payment-loan-info').innerHTML = `
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;">
      <div><div style="font-size:11px;color:var(--gray-400);">Member</div><div style="font-weight:600;">${l.member_name}</div></div>
      <div><div style="font-size:11px;color:var(--gray-400);">Loan ID</div><div style="font-weight:600;font-family:monospace;font-size:12px;">${l.id}</div></div>
      <div><div style="font-size:11px;color:var(--gray-400);">Principal</div><div>${fmt(l.principal)}</div></div>
      <div><div style="font-size:11px;color:var(--gray-400);">Interest</div><div style="color:var(--gold-light);">${fmt(l.interest)}</div></div>
      <div><div style="font-size:11px;color:var(--gray-400);">Total Loan</div><div>${fmt(l.total_amount)}</div></div>
      <div><div style="font-size:11px;color:var(--gray-400);">Remaining</div><div style="color:#fc8181;font-weight:700;">${fmt(l.remaining_balance)}</div></div>
    </div>
  `;
  const type = document.getElementById('payment-type').value;
  setPaymentAmount(l, type);
  openModal('modal-payment');
}

function setPaymentAmount(l, type) {
  if (type === 'interest_only') document.getElementById('payment-amount').value = l.interest.toFixed(2);
  else if (type === 'principal_only') document.getElementById('payment-amount').value = l.principal.toFixed(2);
  else document.getElementById('payment-amount').value = l.remaining_balance.toFixed(2);
}

function calcPayment() {
  const loanId = document.getElementById('payment-loan-id').value;
  const l = loans.find(x=>x.id===loanId);
  const type = document.getElementById('payment-type').value;
  if (l) setPaymentAmount(l, type);
}

async function savePayment() {
  const loanId = document.getElementById('payment-loan-id').value;
  const type = document.getElementById('payment-type').value;
  const amount = parseFloat(document.getElementById('payment-amount').value);
  const date = document.getElementById('payment-date').value || today();
  const l = loans.find(x=>x.id===loanId);
  const m = members.find(x=>x.id===l?.member_id);
  if (!l || !m) { toast('Loan not found.', 'error'); return; }
  if (!amount || amount <= 0) { toast('Enter valid amount.', 'error'); return; }
  if (amount > l.remaining_balance) { toast(`Amount exceeds remaining balance of ${fmt(l.remaining_balance)}!`, 'error'); return; }
  const typeLabels = { interest_only:'Interest Only', principal_only:'Principal Only', principal_interest:'Principal + Interest' };
  const pay = { id: genId('PAY'), loan_id: loanId, member_id: m.id, member_name: m.name, payment_type: type, type_label: typeLabels[type], amount, date };
  showLoading(true, 'Processing payment...');
  try {
    await api('addPayment', { data: pay });
    l.remaining_balance -= amount;
    m.active_loan = Math.max(0, m.active_loan - amount);
    if (l.remaining_balance <= 0) { l.remaining_balance = 0; l.status = 'Paid'; m.active_loan = 0; }
    payments.push(pay);
    await logTx('Payment', `Payment (${typeLabels[type]}) by ${m.name}`, m.name, amount);
    showReceipt(pay, l, m);
    toast(`Payment of ${fmt(amount)} processed!`, 'success');
    closeModal('modal-payment');
    renderLoans();
    renderPayments();
    refreshDashboard();
  } finally { showLoading(false); }
}

function showReceipt(pay, loan, member) {
  const now = new Date();
  document.getElementById('receipt-content').innerHTML = `
    <div class="receipt-header">
      <div class="receipt-logo">🏦 Nuñez Saving Vault</div>
      <div class="receipt-sub">Community Savings & Loan System</div>
      <div class="receipt-sub" style="margin-top:4px;">Official Payment Receipt</div>
    </div>
    <div class="receipt-divider"></div>
    <div class="receipt-row"><span>Receipt No:</span><span>${pay.id}</span></div>
    <div class="receipt-row"><span>Date:</span><span>${fmtDateTime(now)}</span></div>
    <div class="receipt-divider"></div>
    <div class="receipt-row"><span>Member:</span><span>${member.name}</span></div>
    <div class="receipt-row"><span>Loan ID:</span><span>${loan.id}</span></div>
    <div class="receipt-row"><span>Payment Type:</span><span>${pay.type_label}</span></div>
    <div class="receipt-divider"></div>
    <div class="receipt-row"><span>Original Loan:</span><span>${fmt(loan.total_amount)}</span></div>
    <div class="receipt-row"><span>Amount Paid:</span><span>${fmt(pay.amount)}</span></div>
    <div class="receipt-row receipt-total"><span>Remaining Balance:</span><span>${fmt(loan.remaining_balance)}</span></div>
    <div class="receipt-row" style="margin-top:6px;"><span>Loan Status:</span><span style="font-weight:700;">${loan.status}</span></div>
    <div class="receipt-footer">
      <div style="margin-bottom:4px;">Processed by: ${currentUser.name} (${currentUser.role})</div>
      Thank you for your payment! — Nuñez Saving Vault
    </div>
  `;
  openModal('modal-receipt');
}

function renderPayments() {
  const tbody = document.getElementById('payments-tbody');
  if (!payments.length) { tbody.innerHTML = `<tr><td colspan="8"><div class="empty-state"><div class="icon">💳</div><p>No payments yet.</p></div></td></tr>`; return; }
  tbody.innerHTML = [...payments].reverse().map((p, i) => `
    <tr class="${p.corrected?'corrected-row':''}">
      <td>${payments.length - i}</td>
      <td><strong>${p.member_name}</strong>${p.corrected?'<span class="badge-corrected">corrected</span>':''}</td>
      <td style="font-family:monospace;font-size:12px;">${p.loan_id}</td>
      <td><span class="badge badge-blue">${p.type_label}</span></td>
      <td class="td-mono" style="color:var(--teal)">${fmt(p.amount)}</td>
      <td>${fmtDate(p.date)}</td>
      <td><button class="btn btn-ghost btn-sm" onclick="viewReceipt('${p.id}')">🧾 View</button></td>
      <td>${currentUser?.role==='Administrator'?`<button class="btn btn-ghost btn-sm" onclick="openEditPayment('${p.id}')">✏️ Edit</button>`:canWrite()?'<span style="color:var(--gray-600);font-size:11px;">Admin only</span>':'—'}</td>
    </tr>
  `).join('');
}

function viewReceipt(payId) {
  const pay = payments.find(x=>x.id===payId);
  const loan = loans.find(x=>x.id===pay?.loan_id);
  const member = members.find(x=>x.id===pay?.member_id);
  if (pay && loan && member) showReceipt(pay, loan, member);
}

// ================================================================
// INTEREST DISTRIBUTION
// ================================================================
function renderInterest() {
  const activeMembers = members.filter(m=>m.status==='Active');
  const pool = settings.interestPool;
  const totalHeads = activeMembers.reduce((s,m)=>s+(m.heads||1),0);
  const perHead = totalHeads > 0 ? pool / totalHeads : 0;
  const dailyRate = settings.dailyRatePerHead || 5;
  const weeklyPerHead = dailyRate * 7;

  const rateField = document.getElementById('rate-per-head');
  if (rateField) rateField.value = dailyRate;
  const weeklyLabel = document.getElementById('rate-weekly-label');
  if (weeklyLabel) weeklyLabel.textContent = `= ₱${weeklyPerHead}/head/week`;

  document.getElementById('dist-total').textContent = fmt(pool);
  document.getElementById('dist-members').textContent = activeMembers.length;
  document.getElementById('dist-heads').textContent = totalHeads;
  document.getElementById('dist-perhead').textContent = fmt(perHead);
  document.getElementById('dist-formula').innerHTML =
    `<span>Interest Pool Formula: ${fmt(pool)} ÷ ${totalHeads} heads = ${fmt(perHead)}/head</span>
     <span style="margin-left:18px;color:var(--gold-light);">📐 Net = Contribution + Interest Share − Loan</span>`;

  const tbody = document.getElementById('dist-preview-tbody');
  if (!activeMembers.length) { tbody.innerHTML = `<tr><td colspan="6"><div class="empty-state" style="padding:30px;"><p>No active members.</p></div></td></tr>`; return; }
  tbody.innerHTML = activeMembers.map(m => {
    const heads = m.heads||1;
    const memberShare = perHead * heads;
    const weeklyContrib = weeklyPerHead * heads;
    const activeLoan = m.active_loan || 0;
    const netNewContribution = m.total_contribution + memberShare - activeLoan;
    const netColor = netNewContribution >= 0 ? 'var(--green-light)' : '#fc8181';
    return `
    <tr>
      <td><strong>${m.name}</strong></td>
      <td style="text-align:center;">
        <span class="badge badge-gold">${heads} 🧑</span>
        <div style="font-size:10px;color:var(--gray-400);margin-top:3px;">₱${weeklyPerHead}×${heads}=₱${weeklyContrib}/wk</div>
      </td>
      <td class="td-mono">${fmt(m.total_contribution)}</td>
      <td class="td-mono" style="color:var(--teal)">+${fmt(memberShare)}
        <div style="font-size:10px;color:var(--gray-400);">${fmt(perHead)}/head × ${heads}</div>
      </td>
      <td class="td-mono" style="color:${activeLoan>0?'#fc8181':'var(--gray-400)'};">
        ${activeLoan>0?'−'+fmt(activeLoan):'—'}
      </td>
      <td class="td-mono" style="color:${netColor};font-weight:700;">
        ${fmt(netNewContribution)}
        <div style="font-size:10px;color:var(--gray-600);font-weight:400;">${fmt(m.total_contribution)} + ${fmt(memberShare)} − ${fmt(activeLoan)}</div>
      </td>
    </tr>`;
  }).join('');
}

function confirmDistribute() {
  const pool = settings.interestPool;
  const activeMembers = members.filter(m=>m.status==='Active');
  if (pool <= 0) { toast('No interest to distribute.', 'warn'); return; }
  if (!activeMembers.length) { toast('No active members.', 'error'); return; }
  const totalHeads = activeMembers.reduce((s,m)=>s+(m.heads||1),0);
  const perHead = pool / totalHeads;
  const dailyRate = settings.dailyRatePerHead || 5;
  document.getElementById('dist-confirm-body').innerHTML = `
    <p style="margin-bottom:12px;">You are about to distribute the interest pool based on <strong style="color:var(--gold-light);">number of heads</strong>:</p>
    <div style="background:rgba(0,201,177,0.08);border:1px solid rgba(0,201,177,0.2);border-radius:10px;padding:14px;font-family:monospace;font-size:13px;">
      <div style="display:flex;justify-content:space-between;margin-bottom:6px;"><span>Daily Rate per Head:</span><strong style="color:var(--gold-light);">₱${dailyRate}/day × 7 = ₱${dailyRate*7}/head/week</strong></div>
      <div style="display:flex;justify-content:space-between;margin-bottom:6px;"><span>Total Interest Pool:</span><strong style="color:var(--teal);">${fmt(pool)}</strong></div>
      <div style="display:flex;justify-content:space-between;margin-bottom:6px;"><span>Active Members:</span><strong>${activeMembers.length}</strong></div>
      <div style="display:flex;justify-content:space-between;margin-bottom:6px;"><span>Total Active Heads:</span><strong style="color:var(--gold-light);">${totalHeads}</strong></div>
      <div style="display:flex;justify-content:space-between;"><span>Per Head Share:</span><strong style="color:var(--teal);">${fmt(perHead)}</strong></div>
    </div>
    <div style="margin-top:14px;font-size:12.5px;color:var(--gray-400);">
      <strong style="color:var(--white);">Distribution per member:</strong><br>
      ${activeMembers.map(m => {
        const share = perHead*(m.heads||1);
        const loan = m.active_loan||0;
        const net = m.total_contribution + share - loan;
        const col = net>=0?'var(--green-light)':'#fc8181';
        return `${m.name} (${m.heads||1}h) → <span style="color:var(--teal);font-family:monospace;">+${fmt(share)}</span> → Net: <span style="color:${col};font-family:monospace;font-weight:700;">${fmt(net)}</span>`;
      }).join('<br>')}
    </div>
  `;
  openModal('modal-confirm-dist');
}

async function doDistribute() {
  const pool = settings.interestPool;
  const activeMembers = members.filter(m=>m.status==='Active');
  if (pool <= 0 || !activeMembers.length) return;
  const totalHeads = activeMembers.reduce((s,m)=>s+(m.heads||1),0);
  const perHead = pool / totalHeads;
  const memberUpdates = activeMembers.map(m => ({ id: m.id, share: perHead * (m.heads||1) }));
  const record = { id: genId('DST'), total: pool, members: activeMembers.length, totalHeads, perHead, date: new Date().toISOString() };
  showLoading(true, 'Distributing interest...');
  try {
    await api('distribute', { data: { memberUpdates, record } });
    activeMembers.forEach(m => {
      const memberShare = perHead * (m.heads||1);
      m.total_contribution += memberShare;
      m.total_interest_earned += memberShare;
    });
    distHistory.push(record);
    settings.totalDistributed += pool;
    settings.interestPool = 0;
    await logTx('Distribution', `Interest distributed: ${fmt(pool)} ÷ ${totalHeads} heads = ${fmt(perHead)}/head`, 'All Members', pool);
    toast(`Interest distributed! ${fmt(perHead)}/head across ${totalHeads} heads.`, 'success');
    closeModal('modal-confirm-dist');
    renderInterest();
    refreshDashboard();
  } finally { showLoading(false); }
}

// ================================================================
// TRANSACTIONS LOG
// ================================================================
function renderTransactions() {
  const tbody = document.getElementById('tx-tbody');
  if (!transactions.length) { tbody.innerHTML = `<tr><td colspan="6"><div class="empty-state"><div class="icon">🔄</div><p>No transactions yet.</p></div></td></tr>`; return; }
  const txIcons = { Member:'👥', Contribution:'💰', Loan:'🏷️', Payment:'💳', Distribution:'✨', Correction:'✏️' };
  const txColors = { Member:'badge-blue', Contribution:'badge-teal', Loan:'badge-gold', Payment:'badge-green', Distribution:'badge-blue', Correction:'badge-gold' };
  tbody.innerHTML = transactions.map((t, i) => `
    <tr>
      <td>${i+1}</td>
      <td><span class="badge ${txColors[t.type]||'badge-gray'}">${txIcons[t.type]||'🔄'} ${t.type}</span></td>
      <td style="max-width:300px;font-size:12.5px;">${t.desc}</td>
      <td>${t.member}</td>
      <td class="td-mono" style="color:${t.amount>0?'var(--teal)':'var(--gray-400)'}">${t.amount>0?fmt(t.amount):'-'}</td>
      <td style="font-size:12px;color:var(--gray-400);">${fmtDateTime(t.date)}</td>
    </tr>
  `).join('');
}

// ================================================================
// CASH ON HAND
// ================================================================
function calculateCashOnHand() {
  const totalContributions = contributions.reduce((s,c) => s + (c.amount||0), 0);
  const totalPaymentsReceived = payments.reduce((s,p) => s + (p.amount||0), 0);
  const totalLoanReleased = loans.reduce((s,l) => s + (l.principal||0), 0);
  const interestDistributed = settings.totalDistributed || 0;
  const cash = totalContributions + totalPaymentsReceived - totalLoanReleased - interestDistributed;
  return Math.max(0, cash);
}

// ================================================================
// DASHBOARD
// ================================================================
function refreshDashboard() {
  const activeM = members.filter(m=>m.status==='Active');
  const totalContrib = members.reduce((s,m)=>s+m.total_contribution,0);
  const totalLoans = members.reduce((s,m)=>s+m.active_loan,0);
  const totalHeads = activeM.reduce((s,m)=>s+(m.heads||1),0);
  const cash = calculateCashOnHand();

  document.getElementById('stat-members').textContent = members.length;
  document.getElementById('stat-contributions').textContent = fmt(totalContrib);
  document.getElementById('stat-loans').textContent = fmt(totalLoans);
  document.getElementById('stat-interest').textContent = fmt(settings.interestPool);
  document.getElementById('stat-distributed').textContent = fmt(settings.totalDistributed);
  document.getElementById('stat-heads').textContent = totalHeads;
  const dailyRate = settings.dailyRatePerHead||5;
  document.getElementById('stat-perhead').textContent = `₱${dailyRate}/day (₱${dailyRate*7}/wk)`;
  document.getElementById('stat-cash').textContent = fmt(cash);
  document.getElementById('stat-cash-sub').textContent = `Contribs + Payments − Loans Released − Distributed`;

  const rtl = document.getElementById('recent-tx-list');
  const recent = transactions.slice(0, 8);
  if (!recent.length) { rtl.innerHTML = `<div class="empty-state"><div class="icon">📭</div><p>No transactions yet.</p></div>`; }
  else {
    const txBg = { Member:'rgba(45,122,255,0.15)', Contribution:'rgba(0,201,177,0.15)', Loan:'rgba(245,166,35,0.15)', Payment:'rgba(0,184,148,0.15)', Distribution:'rgba(45,122,255,0.15)', Correction:'rgba(245,166,35,0.15)' };
    const txIcons = { Member:'👥', Contribution:'💰', Loan:'🏷️', Payment:'💳', Distribution:'✨', Correction:'✏️' };
    rtl.innerHTML = recent.map(t => `
      <div class="tx-item">
        <div class="tx-icon" style="background:${txBg[t.type]||'rgba(255,255,255,0.07)'};">${txIcons[t.type]||'🔄'}</div>
        <div class="tx-info">
          <div class="tx-name">${t.desc.length>50?t.desc.substr(0,50)+'...':t.desc}</div>
          <div class="tx-desc">${t.member} · ${fmtDate(t.date)}</div>
        </div>
        <div>
          <div class="tx-amount" style="color:var(--teal)">${t.amount>0?fmt(t.amount):''}</div>
          <div class="tx-date">${t.type}</div>
        </div>
      </div>
    `).join('');
  }

  const tc = document.getElementById('top-contributors');
  const sorted = [...members].sort((a,b)=>b.total_contribution-a.total_contribution).slice(0,5);
  if (!sorted.length) { tc.innerHTML = `<div class="empty-state" style="padding:30px;"><p>No data.</p></div>`; }
  else {
    tc.innerHTML = sorted.map((m, i) => `
      <div class="tx-item">
        <div class="tx-icon" style="background:rgba(245,166,35,0.15);color:var(--gold-light);font-weight:800;">${i+1}</div>
        <div class="tx-info"><div class="tx-name">${m.name}</div><div class="tx-desc">${m.status}</div></div>
        <div class="tx-amount" style="color:var(--teal)">${fmt(m.total_contribution)}</div>
      </div>
    `).join('');
  }
}

// ================================================================
// EDIT / CORRECTION FUNCTIONS
// ================================================================
function openEditContribution(id) {
  if (currentUser?.role !== 'Administrator') { toast('Only Admins can edit transactions.', 'error'); return; }
  const c = contributions.find(x=>x.id===id);
  if (!c) return;
  document.getElementById('ec-id').value = c.id;
  document.getElementById('ec-member').value = c.member_name;
  document.getElementById('ec-old-amount').value = '₱' + parseFloat(c.amount).toFixed(2);
  document.getElementById('ec-amount').value = c.amount;
  document.getElementById('ec-date').value = c.date;
  document.getElementById('ec-collector').value = c.collector||'';
  document.getElementById('modal-edit-contribution').classList.add('open');
}

async function saveEditContribution() {
  const id = document.getElementById('ec-id').value;
  const newAmount = parseFloat(document.getElementById('ec-amount').value);
  const newDate = document.getElementById('ec-date').value;
  const newCollector = document.getElementById('ec-collector').value.trim();
  if (!newAmount || newAmount <= 0) { toast('Enter a valid amount.', 'error'); return; }
  const c = contributions.find(x=>x.id===id);
  if (!c) { toast('Contribution not found.', 'error'); return; }
  const m = members.find(x=>x.id===c.member_id);
  if (!m) { toast('Member not found.', 'error'); return; }
  const oldAmount = c.amount;
  const diff = newAmount - oldAmount;
  if (m.total_contribution + diff < 0) { toast('Correction not allowed. It will cause negative balance.', 'error'); return; }
  showLoading(true, 'Saving correction...');
  try {
    const updated = { ...c, amount: newAmount, date: newDate||c.date, collector: newCollector||c.collector, corrected: true };
    await api('editContribution', { data: updated });
    m.total_contribution += diff;
    c.amount = newAmount; c.date = updated.date; c.collector = updated.collector; c.corrected = true;
    await logTx('Correction', 'Contribution edited: ' + m.name + ' | ' + fmt(oldAmount) + ' → ' + fmt(newAmount), m.name, newAmount);
    toast('Contribution corrected: ' + fmt(oldAmount) + ' → ' + fmt(newAmount), 'success');
    closeModal('modal-edit-contribution');
    renderContributions();
    refreshDashboard();
  } finally { showLoading(false); }
}

function openEditLoan(id) {
  if (currentUser?.role !== 'Administrator') { toast('Only Admins can edit transactions.', 'error'); return; }
  const l = loans.find(x=>x.id===id);
  if (!l) return;
  document.getElementById('el-id').value = l.id;
  document.getElementById('el-member').value = l.member_name;
  document.getElementById('el-old-principal').value = '₱' + parseFloat(l.principal).toFixed(2);
  document.getElementById('el-principal').value = l.principal;
  document.getElementById('el-date').value = l.date;
  document.getElementById('el-preview').style.display = 'none';
  document.getElementById('modal-edit-loan').classList.add('open');
}

function previewLoanEdit() {
  const newPrincipal = parseFloat(document.getElementById('el-principal').value)||0;
  if (!newPrincipal) { document.getElementById('el-preview').style.display='none'; return; }
  const interest = newPrincipal * 0.05;
  const total = newPrincipal + interest;
  document.getElementById('el-p-principal').textContent = fmt(newPrincipal);
  document.getElementById('el-p-interest').textContent = fmt(interest);
  document.getElementById('el-p-total').textContent = fmt(total);
  document.getElementById('el-preview').style.display = 'block';
}

async function saveEditLoan() {
  const id = document.getElementById('el-id').value;
  const newPrincipal = parseFloat(document.getElementById('el-principal').value);
  const newDate = document.getElementById('el-date').value;
  if (!newPrincipal || newPrincipal <= 0) { toast('Enter a valid principal.', 'error'); return; }
  const l = loans.find(x=>x.id===id);
  if (!l) { toast('Loan not found.', 'error'); return; }
  const m = members.find(x=>x.id===l.member_id);
  if (!m) { toast('Member not found.', 'error'); return; }
  const oldPrincipal = l.principal;
  const oldTotal = l.total_amount;
  const principalDiff = newPrincipal - oldPrincipal;
  const newInterest = newPrincipal * 0.05;
  const newTotal = newPrincipal + newInterest;
  if (m.total_contribution - principalDiff < 0) { toast('Correction not allowed. Negative contribution balance.', 'error'); return; }
  const paidSoFar = oldTotal - l.remaining_balance;
  const updatedLoan = { ...l, principal: newPrincipal, interest: newInterest, total_amount: newTotal,
    remaining_balance: Math.max(0, newTotal - paidSoFar), date: newDate||l.date, corrected: true };
  updatedLoan.status = updatedLoan.remaining_balance <= 0 ? 'Paid' : 'Active';
  showLoading(true, 'Saving loan correction...');
  try {
    await api('editLoan', { data: updatedLoan });
    m.total_contribution -= principalDiff;
    m.active_loan = Math.max(0, m.active_loan + (newTotal - oldTotal));
    settings.interestPool = Math.max(0, settings.interestPool + (newInterest - l.interest));
    Object.assign(l, updatedLoan);
    await logTx('Correction', 'Loan edited: ' + m.name + ' | Principal ' + fmt(oldPrincipal) + ' → ' + fmt(newPrincipal), m.name, newPrincipal);
    toast('Loan corrected! Principal ' + fmt(oldPrincipal) + ' → ' + fmt(newPrincipal), 'success');
    closeModal('modal-edit-loan');
    renderLoans();
    refreshDashboard();
    renderInterest();
  } finally { showLoading(false); }
}

function openEditPayment(id) {
  if (currentUser?.role !== 'Administrator') { toast('Only Admins can edit transactions.', 'error'); return; }
  const p = payments.find(x=>x.id===id);
  if (!p) return;
  document.getElementById('ep-id').value = p.id;
  document.getElementById('ep-member').value = p.member_name;
  document.getElementById('ep-old-amount').value = '₱' + parseFloat(p.amount).toFixed(2);
  document.getElementById('ep-amount').value = p.amount;
  document.getElementById('ep-type').value = p.payment_type;
  document.getElementById('ep-date').value = p.date;
  document.getElementById('modal-edit-payment').classList.add('open');
}

async function saveEditPayment() {
  const id = document.getElementById('ep-id').value;
  const newAmount = parseFloat(document.getElementById('ep-amount').value);
  const newType = document.getElementById('ep-type').value;
  const newDate = document.getElementById('ep-date').value;
  const typeLabels = { interest_only:'Interest Only', principal_only:'Principal Only', principal_interest:'Principal + Interest' };
  if (!newAmount || newAmount <= 0) { toast('Enter a valid amount.', 'error'); return; }
  const p = payments.find(x=>x.id===id);
  if (!p) { toast('Payment not found.', 'error'); return; }
  const l = loans.find(x=>x.id===p.loan_id);
  const m = members.find(x=>x.id===p.member_id);
  if (!l || !m) { toast('Related loan or member not found.', 'error'); return; }
  const oldAmount = p.amount;
  const diff = newAmount - oldAmount;
  const newRemaining = l.remaining_balance - diff;
  if (newRemaining < 0) { toast('Correction not allowed. Negative loan balance.', 'error'); return; }
  const updated = { ...p, amount: newAmount, payment_type: newType, type_label: typeLabels[newType], date: newDate||p.date, corrected: true };
  showLoading(true, 'Saving payment correction...');
  try {
    await api('editPayment', { data: updated });
    l.remaining_balance = newRemaining;
    l.status = newRemaining <= 0 ? 'Paid' : 'Active';
    m.active_loan = Math.max(0, m.active_loan + diff);
    Object.assign(p, updated);
    await logTx('Correction', 'Payment edited: ' + m.name + ' | ' + fmt(oldAmount) + ' → ' + fmt(newAmount), m.name, newAmount);
    toast('Payment corrected: ' + fmt(oldAmount) + ' → ' + fmt(newAmount), 'success');
    closeModal('modal-edit-payment');
    renderPayments();
    renderLoans();
    refreshDashboard();
  } finally { showLoading(false); }
}

// ================================================================
// REPORTS
// ================================================================
function generateReport(type) {
  const out = document.getElementById('report-output');
  const content = document.getElementById('report-content');
  const title = document.getElementById('report-title');
  out.style.display = 'block';

  if (type === 'contributions') {
    title.textContent = '📋 Weekly Contribution Report';
    const total = contributions.reduce((s,c)=>s+c.amount,0);
    content.innerHTML = `
      <div style="margin-bottom:16px;display:flex;gap:20px;flex-wrap:wrap;">
        <div class="stat-card blue" style="flex:1;min-width:150px;"><div class="stat-label">Total Records</div><div class="stat-value blue">${contributions.length}</div></div>
        <div class="stat-card teal" style="flex:1;min-width:150px;"><div class="stat-label">Total Amount</div><div class="stat-value teal">${fmt(total)}</div></div>
      </div>
      <table style="width:100%;border-collapse:collapse;font-size:13px;">
        <thead><tr style="border-bottom:2px solid rgba(255,255,255,0.1);">
          <th style="padding:10px;text-align:left;color:var(--gray-400);">#</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Member</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Amount</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Date</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Collector</th>
        </tr></thead>
        <tbody>${contributions.map((c,i)=>`
          <tr style="border-bottom:1px solid rgba(255,255,255,0.04);">
            <td style="padding:9px 10px;">${i+1}</td>
            <td style="padding:9px 10px;font-weight:600;">${c.member_name}</td>
            <td style="padding:9px 10px;font-family:monospace;color:var(--teal);">${fmt(c.amount)}</td>
            <td style="padding:9px 10px;">${fmtDate(c.date)}</td>
            <td style="padding:9px 10px;">${c.collector||'-'}</td>
          </tr>`).join('')}</tbody>
      </table>`;
  }
  else if (type === 'loans') {
    title.textContent = '🏷️ Loan Report';
    const totalPrincipal = loans.reduce((s,l)=>s+l.principal,0);
    const totalInterest = loans.reduce((s,l)=>s+l.interest,0);
    content.innerHTML = `
      <div style="margin-bottom:16px;display:flex;gap:16px;flex-wrap:wrap;">
        <div class="stat-card blue" style="flex:1;min-width:140px;"><div class="stat-label">Total Loans</div><div class="stat-value blue">${loans.length}</div></div>
        <div class="stat-card gold" style="flex:1;min-width:140px;"><div class="stat-label">Total Principal</div><div class="stat-value gold">${fmt(totalPrincipal)}</div></div>
        <div class="stat-card green" style="flex:1;min-width:140px;"><div class="stat-label">Total Interest</div><div class="stat-value green">${fmt(totalInterest)}</div></div>
      </div>
      <table style="width:100%;border-collapse:collapse;font-size:13px;">
        <thead><tr style="border-bottom:2px solid rgba(255,255,255,0.1);">
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Member</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Principal</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Interest</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Total</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Remaining</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Status</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Date</th>
        </tr></thead>
        <tbody>${loans.map(l=>`
          <tr style="border-bottom:1px solid rgba(255,255,255,0.04);">
            <td style="padding:9px 10px;font-weight:600;">${l.member_name}</td>
            <td style="padding:9px 10px;font-family:monospace;">${fmt(l.principal)}</td>
            <td style="padding:9px 10px;font-family:monospace;color:var(--gold-light);">${fmt(l.interest)}</td>
            <td style="padding:9px 10px;font-family:monospace;">${fmt(l.total_amount)}</td>
            <td style="padding:9px 10px;font-family:monospace;color:${l.remaining_balance>0?'#fc8181':'var(--green-light)'};">${fmt(l.remaining_balance)}</td>
            <td style="padding:9px 10px;">${l.status}</td>
            <td style="padding:9px 10px;">${fmtDate(l.date)}</td>
          </tr>`).join('')}</tbody>
      </table>`;
  }
  else if (type === 'interest') {
    title.textContent = '✨ Interest Distribution Report';
    content.innerHTML = `
      <div style="margin-bottom:16px;display:flex;gap:16px;flex-wrap:wrap;">
        <div class="stat-card teal" style="flex:1;min-width:150px;"><div class="stat-label">Current Pool</div><div class="stat-value teal">${fmt(settings.interestPool)}</div></div>
        <div class="stat-card green" style="flex:1;min-width:150px;"><div class="stat-label">Total Distributed</div><div class="stat-value green">${fmt(settings.totalDistributed)}</div></div>
        <div class="stat-card blue" style="flex:1;min-width:150px;"><div class="stat-label">Events</div><div class="stat-value blue">${distHistory.length}</div></div>
      </div>
      <table style="width:100%;border-collapse:collapse;font-size:13px;">
        <thead><tr style="border-bottom:2px solid rgba(255,255,255,0.1);">
          <th style="padding:10px;text-align:left;color:var(--gray-400);">#</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Total Distributed</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Members</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Total Heads 🧑</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Per Head</th>
          <th style="padding:10px;text-align:left;color:var(--gray-400);">Date</th>
        </tr></thead>
        <tbody>${distHistory.length?distHistory.map((d,i)=>`
          <tr style="border-bottom:1px solid rgba(255,255,255,0.04);">
            <td style="padding:9px 10px;">${i+1}</td>
            <td style="padding:9px 10px;font-family:monospace;color:var(--teal);">${fmt(d.total)}</td>
            <td style="padding:9px 10px;">${d.members}</td>
            <td style="padding:9px 10px;font-family:monospace;color:var(--gold-light);">${d.totalHeads||d.members}</td>
            <td style="padding:9px 10px;font-family:monospace;color:var(--teal);">${fmt(d.perHead||d.share)}</td>
            <td style="padding:9px 10px;">${fmtDateTime(d.date)}</td>
          </tr>`).join(''):`<tr><td colspan="6" style="padding:30px;text-align:center;color:var(--gray-600);">No distributions yet.</td></tr>`}
        </tbody>
      </table>`;
  }
  else if (type === 'ledger') {
    title.textContent = '📒 Individual Member Ledger';
    content.innerHTML = members.map(m => {
      const mContribs = contributions.filter(c=>c.member_id===m.id);
      const mLoans = loans.filter(l=>l.member_id===m.id);
      const mPayments = payments.filter(p=>p.member_id===m.id);
      return `
        <div style="margin-bottom:28px;padding-bottom:28px;border-bottom:1px solid rgba(255,255,255,0.07);">
          <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:14px;flex-wrap:wrap;gap:10px;">
            <div>
              <div style="font-size:16px;font-weight:700;">${m.name}
                <span class="badge ${m.status==='Active'?'badge-green':'badge-gray'}" style="margin-left:8px;">${m.status}</span>
                <span class="badge badge-gold" style="margin-left:6px;">${m.heads||1} 🧑</span>
              </div>
              <div style="font-size:11px;color:var(--gray-400);margin-top:3px;font-family:monospace;">${m.id}</div>
            </div>
            <div style="display:flex;gap:12px;flex-wrap:wrap;">
              <div style="text-align:right;"><div style="font-size:10px;color:var(--gray-400);">CONTRIBUTION</div><div style="font-family:monospace;font-weight:700;color:var(--teal);">${fmt(m.total_contribution)}</div></div>
              <div style="text-align:right;"><div style="font-size:10px;color:var(--gray-400);">ACTIVE LOAN</div><div style="font-family:monospace;font-weight:700;color:#fc8181;">${fmt(m.active_loan)}</div></div>
              <div style="text-align:right;"><div style="font-size:10px;color:var(--gray-400);">INTEREST EARNED</div><div style="font-family:monospace;font-weight:700;color:var(--gold-light);">${fmt(m.total_interest_earned)}</div></div>
            </div>
          </div>
          <div style="font-size:12px;color:var(--gray-400);">Contributions: ${mContribs.length} | Loans: ${mLoans.length} | Payments: ${mPayments.length}</div>
        </div>`;
    }).join('') || '<p style="color:var(--gray-600);text-align:center;padding:30px;">No members found.</p>';
  }
  out.scrollIntoView({ behavior:'smooth', block:'start' });
}

function printReport() { window.print(); }

// ================================================================
// KEYBOARD SHORTCUTS
// ================================================================
document.addEventListener('keydown', e => {
  if (e.key === 'Escape') document.querySelectorAll('.modal-overlay.open').forEach(m => m.classList.remove('open'));
});

// ================================================================
// START
// ================================================================
window.addEventListener('load', () => {
  document.querySelectorAll('input[type="date"]').forEach(i => { if (!i.value) i.valueAsDate = new Date(); });
});
</script>
</body>
</html>
