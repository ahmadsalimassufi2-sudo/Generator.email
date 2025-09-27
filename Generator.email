<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>📧 Email Sementara Keren — Dengan Salin Email & OTP</title>
<style>
  :root{
    --glass-bg: rgba(255,255,255,0.15);
    --accent:#2563eb; --accent-2:#10b981; --muted:rgba(255,255,255,0.8);
    --toast-bg: rgba(2,6,23,0.85);
  }
  /* Background */
  body{
    margin:0; min-height:100vh; display:flex; align-items:center; justify-content:center;
    font-family: Inter, "Segoe UI", system-ui, -apple-system, Roboto, "Helvetica Neue", Arial;
    background: linear-gradient(270deg,#4facfe,#00f2fe,#43e97b,#f8ffae,#ff6a00,#ee0979);
    background-size:1200% 1200%; animation:gr 20s ease infinite;
  }
  @keyframes gr { 0%{background-position:0% 50%}50%{background-position:100% 50%}100%{background-position:0% 50%} }

  /* Card glass */
  .card{
    width:920px; max-width:95vw; border-radius:14px; padding:20px;
    background:var(--glass-bg); color:white; box-shadow:0 12px 40px rgba(2,6,23,0.25);
    backdrop-filter: blur(10px);
    display:grid; grid-template-columns: 1fr 420px; gap:18px; align-items:start;
  }
  header{grid-column:1/-1; display:flex; align-items:center; gap:12px; margin-bottom:6px}
  h1{margin:0; font-size:1.15rem}
  p.lead{margin:0;color:var(--muted); font-size:0.92rem}

  /* Left area */
  .left{padding:12px}
  .email-box{
    background: rgba(255,255,255,0.07); padding:12px; border-radius:10px; display:flex; gap:10px; align-items:center; justify-content:space-between;
    cursor:pointer; transition:all .18s;
  }
  .email-box:hover{transform:translateY(-3px)}
  .email-text{font-weight:700; font-size:0.98rem; word-break:break-all}
  .controls{display:flex; gap:10px; margin-top:10px}
  .btn{padding:10px 12px; border-radius:10px; border: none; cursor:pointer; font-weight:600}
  .btn.primary{background:var(--accent); color:white}
  .btn.ghost{background:transparent; border:1px solid rgba(255,255,255,0.12); color:white}
  .btn.warn{background:#f59e0b; color:#081124}

  .inbox{margin-top:14px; max-height:440px; overflow:auto; padding-right:6px}
  .mail-item{
    background: rgba(255,255,255,0.04); padding:10px; border-radius:10px; margin-bottom:10px; transition:all .15s; border:1px solid rgba(255,255,255,0.03);
  }
  .mail-item:hover{background:rgba(255,255,255,0.06)}
  .mail-meta{display:flex; justify-content:space-between; gap:8px; align-items:center; font-size:0.9rem}
  .mail-from{font-weight:700}
  .mail-sub{color:var(--muted); font-size:0.92rem; margin-top:6px}

  /* Right area */
  .right{padding:12px; background: linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.02)); border-radius:10px}
  .msg-meta{font-size:0.9rem; color:var(--muted); margin-bottom:8px}
  .msg-body{background: rgba(0,0,0,0.04); color: #012; padding:12px; border-radius:8px; min-height:160px; max-height:420px; overflow:auto}
  .msg-body pre{white-space:pre-wrap; font-family:inherit; margin:0}
  .otp-badge{display:inline-flex; align-items:center; gap:8px; background:var(--accent-2); color:#002; padding:8px 10px; border-radius:999px; font-weight:800; margin-right:8px}

  /* small actions */
  .action-row{display:flex; gap:8px; align-items:center; margin-top:12px}

  /* Toast */
  .toast{
    position:fixed; right:22px; bottom:22px; background:var(--toast-bg); color:white; padding:10px 14px; border-radius:10px;
    box-shadow:0 8px 30px rgba(2,6,23,0.45); transform: translateY(24px); opacity:0; transition:all .25s;
  }
  .toast.show{transform:translateY(0); opacity:1}

  /* responsive */
  @media (max-width:980px){ .card{grid-template-columns:1fr; width:92vw} .right{order:3} }
</style>
</head>
<body>
  <div class="card" role="main" aria-labelledby="title">
    <header>
      <div>
        <h1 id="title">📧 Email Sementara — Keren & Praktis</h1>
        <p class="lead">Buat alamat email sementara, cek inbox, dan salin OTP secara otomatis. API: 1secmail (tanpa API key).</p>
      </div>
    </header>

    <!-- left column -->
    <div class="left" aria-live="polite">
      <div class="email-box" id="emailBox" title="Klik untuk menyalin email (setelah dibuat)">
        <div class="email-text" id="emailText">Belum ada email — klik "Buat Email"</div>
        <div style="display:flex; gap:8px; align-items:center">
          <button class="btn ghost" id="copyEmailBtn" style="display:none">📋 Salin</button>
        </div>
      </div>

      <div class="controls">
        <button class="btn primary" id="genBtn">✨ Buat Email</button>
        <button class="btn" id="checkBtn" style="background:linear-gradient(90deg,#06b6d4,#7c3aed); color:white">📥 Cek Inbox</button>
        <button class="btn ghost" id="autoRefreshBtn">🔁 Auto-Refresh: Mati</button>
      </div>

      <div class="inbox" id="inboxList">
        <div style="color:var(--muted); margin-top:12px">Inbox kosong — buat email lalu cek inbox.</div>
      </div>
    </div>

    <!-- right column -->
    <div class="right" aria-live="assertive">
      <div class="msg-meta" id="msgMeta">Pilih pesan dari inbox untuk melihat isi.</div>
      <div class="msg-body" id="msgBody"><pre style="color:inherit">Pesan akan tampil di sini.</pre></div>

      <div class="action-row" id="actionRow" style="display:none">
        <div id="otpContainer"></div>
        <button class="btn ghost" id="copyOtpBtn" style="display:none">📋 Salin OTP</button>
        <button class="btn ghost" id="copyFullBtn" style="display:none">📥 Salin Isi</button>
      </div>
    </div>
  </div>

  <div id="toast" class="toast" role="status" aria-live="polite"></div>

<script>
/* --- Config & State --- */
const API = 'https://www.1secmail.com/api/v1/';
const DOMAINS = ['1secmail.com','1secmail.org','1secmail.net','esiix.com']; // bisa tambah domain
const STORAGE_KEY = 'tempmail_keren_history';
let state = { login:'', domain:'', email:'', messages: [], autoRefresh:false, autoInterval:null };
const $ = id => document.getElementById(id);

/* --- Utils --- */
function randStr(n=8){ return Math.random().toString(36).slice(2,2+n) }
function toast(text){ const t=$('toast'); t.textContent=text; t.classList.add('show'); setTimeout(()=>t.classList.remove('show'),2000) }
async function copy(text){
  try{ await navigator.clipboard.writeText(text); return true }catch(e){ return false }
}
function isUrlValid(s){
  try{ const u=new URL(s); return u.protocol==='http:'||u.protocol==='https:' }catch(e){ return false }
}
function extractOtpFromText(text){
  if(!text) return null;
  // prefer longest or first occurrence 4-8 digits, also allow multiple occurrences — return first
  const m = text.match(/\b(\d{4,8})\b/g);
  return m ? m[0] : null;
}
function stripHtml(html){
  try{ const d=new DOMParser().parseFromString(html,'text/html'); return d.body.textContent||'' }catch(e){ return html.replace(/<\/?[^>]+(>|$)/g,'') }
}

/* --- DOM references --- */
const emailText = $('emailText'), emailBox = $('emailBox'), copyEmailBtn = $('copyEmailBtn');
const genBtn = $('genBtn'), checkBtn = $('checkBtn'), inboxList = $('inboxList');
const msgMeta = $('msgMeta'), msgBody = $('msgBody'), otpContainer = $('otpContainer');
const copyOtpBtn = $('copyOtpBtn'), copyFullBtn = $('copyFullBtn'), actionRow = $('actionRow');
const autoRefreshBtn = $('autoRefreshBtn');

/* --- Functions --- */
function setCurrent(email){
  state.email = email;
  const parts = email.split('@');
  state.login = parts[0]||'';
  state.domain = parts[1]||'';
  emailText.textContent = email;
  copyEmailBtn.style.display = 'inline-block';
  toast('Alamat email dibuat dan siap disalin ✨');
  saveHistory(email);
}

function generateEmail(){
  const login = randStr(8);
  const domain = DOMAINS[Math.floor(Math.random()*DOMAINS.length)];
  setCurrent(login + '@' + domain);
  inboxList.innerHTML = '<div style="color:var(--muted); margin-top:12px">Inbox belum dicek.</div>';
  clearMessageView();
}

async function checkInbox(){
  if(!state.email){ toast('Buat email dulu ya 😇'); return; }
  inboxList.innerHTML = '<div style="color:var(--muted); margin-top:8px">Memuat inbox...</div>';
  try{
    const url = `${API}?action=getMessages&login=${encodeURIComponent(state.login)}&domain=${encodeURIComponent(state.domain)}`;
    const res = await fetch(url);
    if(!res.ok) throw new Error('Status ' + res.status);
    const data = await res.json();
    state.messages = Array.isArray(data) ? data : [];
    renderInbox();
    toast('Inbox diperbarui ✔️');
  }catch(e){
    inboxList.innerHTML = `<div style="color:#ffb4b4">Error memuat inbox: ${e.message}</div>`;
  }
}

function renderInbox(){
  inboxList.innerHTML = '';
  if(!state.messages.length){
    inboxList.innerHTML = '<div style="color:var(--muted); margin-top:12px">Inbox kosong.</div>';
    return;
  }
  // newest first
  const arr = state.messages.slice().reverse();
  arr.forEach(m => {
    const div = document.createElement('div');
    div.className = 'mail-item';
    div.innerHTML = `
      <div class="mail-meta">
        <div><span class="mail-from">${escapeHtml(m.from)}</span><div class="mail-sub">${escapeHtml(m.subject||'(tanpa subjek)')}</div></div>
        <div style="text-align:right"><div class="small">${escapeHtml(m.date)}</div><button class="btn ghost small" data-id="${m.id}">Buka</button></div>
      </div>
    `;
    inboxList.appendChild(div);
    div.querySelector('button[data-id]').addEventListener('click', ()=> openMessage(m.id));
  });
}

function clearMessageView(){
  msgMeta.textContent = 'Pilih pesan dari inbox untuk melihat isinya.';
  msgBody.innerHTML = '<pre style="color:inherit">Pesan akan tampil di sini.</pre>';
  actionRow.style.display = 'none';
  otpContainer.innerHTML = '';
  copyOtpBtn.style.display = 'none';
  copyFullBtn.style.display = 'none';
}

async function openMessage(id){
  msgBody.innerHTML = '<pre style="color:inherit">Memuat pesan...</pre>';
  msgMeta.textContent = 'Memuat...';
  actionRow.style.display = 'none';
  try{
    const url = `${API}?action=readMessage&login=${encodeURIComponent(state.login)}&domain=${encodeURIComponent(state.domain)}&id=${encodeURIComponent(id)}`;
    const res = await fetch(url);
    if(!res.ok) throw new Error('Status ' + res.status);
    const data = await res.json();
    const from = data.from || '';
    const subject = data.subject || '(tanpa subjek)';
    const date = data.date || '';
    let body = (data.textBody && data.textBody.trim()) ? data.textBody : (data.htmlBody || '');
    if(!body) body = '(Tidak ada isi pesan)';
    if(data.htmlBody && (!data.textBody || data.textBody.trim()==='')) body = stripHtml(data.htmlBody);
    msgMeta.textContent = `${from} — ${subject} — ${date}`;
    msgBody.innerHTML = `<pre style="color:inherit">${escapeHtml(body)}</pre>`;
    // OTP detection
    const otp = extractOtpFromText(body);
    otpContainer.innerHTML = '';
    if(otp){
      otpContainer.innerHTML = `<span class="otp-badge">🔐 ${otp}</span>`;
      copyOtpBtn.style.display = 'inline-block';
      copyFullBtn.style.display = 'inline-block';
      copyOtpBtn.onclick = async ()=> {
        const ok = await copy(otp);
        copyOtpBtn.textContent = ok ? 'Tersalin!' : 'Gagal';
        setTimeout(()=> copyOtpBtn.textContent = '📋 Salin OTP', 1200);
        if(ok) toast('OTP disalin 🔑');
      };
      copyOtpBtn.textContent = '📋 Salin OTP';
    } else {
      otpContainer.innerHTML = `<span style="color:var(--muted)">Tidak menemukan OTP (4–8 digit).</span>`;
      copyOtpBtn.style.display = 'none';
      copyFullBtn.style.display = 'inline-block';
    }
    // copy full message
    copyFullBtn.style.display = 'inline-block';
    copyFullBtn.onclick = async ()=> {
      const ok = await copy(body);
      copyFullBtn.textContent = ok ? 'Tersalin!' : 'Gagal';
      setTimeout(()=> copyFullBtn.textContent = '📥 Salin Isi', 1200);
      if(ok) toast('Isi pesan disalin 📥');
    };
    actionRow.style.display = 'flex';
  }catch(e){
    msgBody.innerHTML = `<pre style="color:inherit">Error memuat pesan: ${e.message}</pre>`;
    msgMeta.textContent = '—';
  }
}

/* --- Events --- */
genBtn.addEventListener('click', generateEmail);
$('copyEmailBtn').addEventListener('click', async ()=>{
  if(!state.email) return toast('Belum ada email');
  const ok = await copy(state.email);
  $('copyEmailBtn').textContent = ok ? 'Tersalin!' : 'Gagal';
  setTimeout(()=> $('copyEmailBtn').textContent = '📋 Salin', 1200);
  if(ok) toast('Alamat email disalin 📋');
});
emailBox.addEventListener('click', async ()=> {
  if(!state.email) return generateEmail();
  const ok = await copy(state.email);
  toast(ok ? 'Alamat email disalin 📋' : 'Gagal menyalin');
});

// check inbox
checkBtn.addEventListener('click', checkInbox);

// auto refresh toggle
autoRefreshBtn.addEventListener('click', ()=>{
  state.autoRefresh = !state.autoRefresh;
  if(state.autoRefresh){
    autoRefreshBtn.textContent = '🔁 Auto-Refresh: Hidup';
    state.autoInterval = setInterval(()=> {
      if(state.email) checkInbox();
    }, 8000); // tiap 8 detik
    toast('Auto-refresh aktif (8s)');
  } else {
    autoRefreshBtn.textContent = '🔁 Auto-Refresh: Mati';
    if(state.autoInterval) { clearInterval(state.autoInterval); state.autoInterval = null; }
    toast('Auto-refresh dimatikan');
  }
});

/* --- History (simple) --- */
function saveHistory(email){
  try{
    const raw = localStorage.getItem(STORAGE_KEY);
    const arr = raw ? JSON.parse(raw) : [];
    if(!arr.includes(email)) arr.push(email);
    while(arr.length>30) arr.shift();
    localStorage.setItem(STORAGE_KEY, JSON.stringify(arr));
    // you could render history somewhere
  }catch(e){}
}

/* --- Helpers --- */
function escapeHtml(s){ if(!s) return ''; return String(s).replaceAll('&','&amp;').replaceAll('<','&lt;').replaceAll('>','&gt;'); }

/* --- Init --- */
(function init(){
  // set copy button label icon
  $('copyEmailBtn').textContent = '📋 Salin';
  copyOtpBtn.textContent = '📋 Salin OTP';
  copyFullBtn.textContent = '📥 Salin Isi';
  autoRefreshBtn.textContent = '🔁 Auto-Refresh: Mati';
  // restore last email if exists
  try{
    const raw = localStorage.getItem(STORAGE_KEY);
    const arr = raw ? JSON.parse(raw) : [];
    if(arr.length){
      const last = arr[arr.length-1];
      state.email = last;
      const parts = last.split('@'); state.login=parts[0]; state.domain=parts[1];
      emailText.textContent = last; copyEmailBtn.style.display='inline-block';
    }
  }catch(e){}
})();
</script>
</body>
</html>
