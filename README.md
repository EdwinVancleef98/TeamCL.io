<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#1a0f3a">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-title" content="FieldCheck">
<title>FieldCheck</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Manrope:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<style>
:root{
  --bg1:#1b1036;--bg2:#2a1259;--bg3:#140c2b;
  --glass:rgba(255,255,255,.06);--glass2:rgba(255,255,255,.10);--line:rgba(255,255,255,.10);
  --tx:#f4f1ff;--mut:#a59cc4;--dim:#6f6791;
  --pink:#f9a8d4;--green:#5ee6a0;--blue:#93c5fd;--violet:#c084fc;--coral:#ff7a7a;--amber:#fbbf24;
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html{background:var(--bg3)}
body{margin:0;min-height:100vh;font:500 16px/1.45 "Manrope","Plus Jakarta Sans","Segoe UI",-apple-system,Roboto,sans-serif;color:var(--tx);
  background:radial-gradient(120% 60% at 100% 0%,#3a1a78 0%,transparent 60%),radial-gradient(90% 50% at 0% 100%,#2a1260 0%,transparent 60%),linear-gradient(180deg,var(--bg1),var(--bg3));
  background-attachment:fixed;padding-bottom:calc(120px + env(safe-area-inset-bottom))}
main{padding:0 18px;max-width:720px;margin:0 auto}
header{padding:calc(22px + env(safe-area-inset-top)) 22px 14px;max-width:720px;margin:0 auto;display:flex;justify-content:space-between;align-items:center;gap:12px}
.date{font-size:13px;letter-spacing:.06em;text-transform:uppercase;color:var(--mut);font-weight:600}
.greet{font-size:32px;font-weight:800;letter-spacing:-.02em;margin:2px 0 0;line-height:1.1}
.avatar{width:54px;height:54px;border-radius:50%;flex:none;display:grid;place-items:center;font-weight:800;font-size:15px;position:relative;
  background:linear-gradient(135deg,#a78bfa,#f9a8d4);border:3px solid rgba(255,255,255,.15);box-shadow:0 6px 20px rgba(167,139,250,.35)}
.avatar::after{content:"";position:absolute;top:0;right:0;width:12px;height:12px;border-radius:50%;background:#5eead4;border:2px solid var(--bg1)}
.tab{display:none}.tab.on{display:block;animation:fade .3s ease}
@keyframes fade{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}
.card{background:linear-gradient(160deg,rgba(255,255,255,.09),rgba(255,255,255,.03));border:1px solid var(--line);border-radius:28px;padding:20px;margin-bottom:16px;
  backdrop-filter:blur(18px);-webkit-backdrop-filter:blur(18px);box-shadow:0 10px 30px rgba(0,0,0,.25)}
.ch{display:flex;align-items:center;gap:12px;margin-bottom:14px}
.ch h2{font-size:19px;font-weight:600;margin:0;flex:1}
.ch .side{color:var(--mut);font-size:14px}
.ic{width:42px;height:42px;border-radius:50%;display:grid;place-items:center;background:rgba(192,132,252,.18);font-size:19px;flex:none}
.ic.r{background:rgba(255,122,122,.18)}.ic.g{background:rgba(94,230,160,.16)}.ic.b{background:rgba(147,197,253,.16)}
/* progress card */
.dash{display:flex;align-items:center;gap:20px}
.rings{width:140px;height:140px;flex:none;filter:drop-shadow(0 0 10px rgba(249,168,212,.25))}
.rings circle{fill:none;stroke-linecap:round;transition:stroke-dashoffset .6s ease}
.mets{flex:1;min-width:0}
.met{margin-bottom:14px}.met:last-child{margin:0}
.met .l{display:flex;justify-content:space-between;font-size:14px;color:var(--mut);margin-bottom:7px}
.met .l b{color:var(--tx);font-weight:700}
.trk{height:8px;border-radius:8px;background:rgba(255,255,255,.08);overflow:hidden}
.trk i{display:block;height:100%;border-radius:8px;width:0;transition:width .6s ease}
@media (max-width:380px){.dash{flex-direction:column;align-items:stretch}.rings{margin:0 auto}}
/* buttons */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:8px;padding:13px 16px;border-radius:18px;border:1px solid var(--line);background:var(--glass2);color:var(--tx);font:700 15px "Manrope",sans-serif;cursor:pointer;transition:transform .1s}
.btn:active{transform:scale(.97)}
.btn.p{border:0;background:linear-gradient(135deg,#c084fc,#f0abfc);color:#2a1259;box-shadow:0 6px 22px rgba(192,132,252,.45)}
.btn.ok{border:0;background:linear-gradient(135deg,#34d399,#5ee6a0);color:#063b24;box-shadow:0 6px 22px rgba(94,230,160,.3)}
.btn.bad{color:var(--coral)}
.btn.sm{padding:9px 14px;font-size:13px;border-radius:14px}
.btns{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:14px}
.btns.one{grid-template-columns:1fr}
.muted{color:var(--mut);font-size:14px}
input[type=text]{width:100%;padding:12px 14px;border:1px solid var(--line);border-radius:14px;background:rgba(0,0,0,.2);color:var(--tx);font:500 15px "Manrope",sans-serif}
input::placeholder{color:var(--dim)}
input:focus,button:focus-visible,summary:focus-visible{outline:2px solid var(--violet);outline-offset:2px}
/* checklist */
.lh{display:flex;justify-content:space-between;align-items:center;margin:6px 4px 12px}
.lh h3{margin:0;font-size:20px;font-weight:700}
details.sec{background:linear-gradient(160deg,rgba(255,255,255,.08),rgba(255,255,255,.03));border:1px solid var(--line);border-radius:24px;margin-bottom:12px;overflow:hidden;backdrop-filter:blur(18px);-webkit-backdrop-filter:blur(18px)}
summary{list-style:none;display:flex;align-items:center;gap:12px;padding:14px 16px;font-weight:600;font-size:16px;cursor:pointer}
summary::-webkit-details-marker{display:none}
summary .t{flex:1}
summary .ic{width:38px;height:38px;font-size:17px}
.cnt{font-size:13px;font-weight:700;padding:4px 11px;border-radius:20px;background:rgba(255,255,255,.08);color:var(--mut)}
.cnt.full{background:rgba(94,230,160,.2);color:var(--green)}
.mini{height:3px;background:rgba(255,255,255,.06)}.mini i{display:block;height:100%;background:linear-gradient(90deg,#c084fc,#f9a8d4);transition:width .4s}
.it{display:flex;align-items:center;border-top:1px solid rgba(255,255,255,.06)}
.it label{flex:1;display:flex;align-items:center;gap:14px;padding:13px 16px;cursor:pointer}
.it input{appearance:none;-webkit-appearance:none;width:26px;height:26px;flex:none;border-radius:9px;border:2px solid rgba(255,255,255,.25);display:grid;place-items:center;transition:all .15s;margin:0}
.it input:checked{background:linear-gradient(135deg,#34d399,#5ee6a0);border-color:transparent;box-shadow:0 0 12px rgba(94,230,160,.5)}
.it input:checked::after{content:"✓";color:#063b24;font-weight:800;font-size:15px}
.it span{font-size:15px}
.it.done span{color:var(--dim);text-decoration:line-through}
.crit{color:var(--amber);font-size:13px;filter:drop-shadow(0 0 4px rgba(251,191,36,.5))}
.ib{border:0;background:none;font-size:17px;padding:10px;cursor:pointer;color:var(--dim)}
.ib.on{color:var(--amber)}
form.add{display:flex;gap:8px;padding:12px 16px;border-top:1px solid rgba(255,255,255,.06)}
form.add input{flex:1}
/* photos */
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(150px,1fr));gap:12px}
.ph{background:var(--glass);border:1px solid var(--line);border-radius:22px;overflow:hidden}
.ph img{width:100%;aspect-ratio:4/3;object-fit:cover;display:block;cursor:pointer}
.ph .m{padding:8px;display:flex;gap:6px;align-items:center}
.ph .m input{padding:7px 9px;font-size:13px;border-radius:10px}
.badge{font-size:10px;font-weight:800;padding:3px 7px;border-radius:8px;letter-spacing:.04em}
.badge.before{background:rgba(147,197,253,.2);color:var(--blue)}.badge.after{background:rgba(94,230,160,.2);color:var(--green)}
.empty{text-align:center;padding:30px 10px;color:var(--dim)}
/* history */
.hrow{display:flex;align-items:center;gap:14px}
.hrow .pct{width:52px;height:52px;flex:none}
.hrow b{font-size:16px}
/* bottom nav */
nav{position:fixed;left:50%;transform:translateX(-50%);bottom:calc(14px + env(safe-area-inset-bottom));width:calc(100% - 28px);max-width:560px;height:72px;
  display:flex;align-items:center;justify-content:space-around;background:rgba(28,18,58,.78);border:1px solid var(--line);border-radius:36px;
  backdrop-filter:blur(22px);-webkit-backdrop-filter:blur(22px);box-shadow:0 12px 34px rgba(0,0,0,.45);z-index:6}
nav button{border:0;background:none;color:var(--dim);width:54px;height:54px;border-radius:50%;display:grid;place-items:center;cursor:pointer;transition:all .2s}
nav button svg{width:24px;height:24px}
nav button.on{color:#fff;background:rgba(255,255,255,.1)}
nav .gap{width:74px}
#fab{position:absolute;left:50%;top:-30px;transform:translateX(-50%);width:76px;height:76px;border-radius:50%;border:0;cursor:pointer;
  background:linear-gradient(135deg,#d8b4fe,#c084fc);box-shadow:0 0 0 6px rgba(28,18,58,.9),0 0 34px rgba(192,132,252,.7);display:grid;place-items:center}
#fab span{width:40px;height:40px;border-radius:50%;background:#2a1259;display:grid;place-items:center;color:#e9d5ff}
#fab svg{width:20px;height:20px}
#fab:active{transform:translateX(-50%) scale(.94)}
#toast{position:fixed;left:50%;bottom:110px;transform:translateX(-50%);background:rgba(255,255,255,.95);color:#2a1259;font-weight:700;padding:10px 18px;border-radius:20px;font-size:14px;opacity:0;transition:opacity .25s;pointer-events:none;z-index:40;white-space:nowrap}
#toast.on{opacity:1}
/* overlays */
.ov{position:fixed;inset:0;background:var(--bg3);z-index:30;overflow:auto;display:none}
.ov.on{display:block}
.rbar{position:sticky;top:0;display:flex;gap:8px;padding:calc(12px + env(safe-area-inset-top)) 14px 12px;background:rgba(27,16,54,.92);backdrop-filter:blur(16px);-webkit-backdrop-filter:blur(16px);border-bottom:1px solid var(--line);z-index:2}
.rbar .btn{flex:1;padding:11px 6px;font-size:14px}
.rep{padding:20px;max-width:800px;margin:16px auto;background:#fff;color:#1b1036;border-radius:20px;font-family:"Manrope",sans-serif}
.rep h1{font-size:22px;margin:0 0 4px;font-weight:800}.rep h3{margin:18px 0 6px;font-size:15px;border-bottom:2px solid #c084fc;padding-bottom:4px}
.rep table{width:100%;border-collapse:collapse;font-size:13px}
.rep td{padding:5px 6px;border-bottom:1px solid #eee;vertical-align:top}
.rep .pg{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.rep .pg figure{margin:0}.rep .pg img{width:100%;border-radius:8px}
.rep figcaption{font-size:12px;color:#555}
.rep .y{color:#138a3e;font-weight:800}.rep .n{color:#c42b1c;font-weight:800}
#viewer img{max-width:100%;display:block;margin:0 auto}
@media print{html,body{background:#fff}body>*:not(#report){display:none!important}#report{position:static;display:block;background:#fff}.rbar{display:none}.rep{max-width:none;margin:0;border-radius:0}.rep figure{break-inside:avoid}}
@media (prefers-reduced-motion:reduce){*{animation:none!important;transition:none!important}}
</style>
</head>
<body>
<header>
  <div><div class="date" id="hDate"></div><h1 class="greet" id="hGreet">Hello</h1></div>
  <div class="avatar" id="hPct" aria-label="Progress">0%</div>
</header>

<main>
<!-- CHECKLIST -->
<section class="tab on" id="t-list">
  <div class="card">
    <div class="ch"><div class="ic">🛠️</div><h2>Visit Progress</h2><span class="side" id="dTime">Today</span></div>
    <div class="dash">
      <svg class="rings" viewBox="0 0 140 140" aria-hidden="true">
        <circle cx="70" cy="70" r="62" stroke="rgba(249,168,212,.15)" stroke-width="11"/>
        <circle cx="70" cy="70" r="46" stroke="rgba(94,230,160,.15)" stroke-width="11"/>
        <circle cx="70" cy="70" r="30" stroke="rgba(147,197,253,.15)" stroke-width="11"/>
        <circle id="r1" cx="70" cy="70" r="62" stroke="#f9a8d4" stroke-width="11" transform="rotate(-90 70 70)"/>
        <circle id="r2" cx="70" cy="70" r="46" stroke="#5ee6a0" stroke-width="11" transform="rotate(-90 70 70)"/>
        <circle id="r3" cx="70" cy="70" r="30" stroke="#93c5fd" stroke-width="11" transform="rotate(-90 70 70)"/>
      </svg>
      <div class="mets">
        <div class="met"><div class="l">Checklist<b id="m1">0/0</b></div><div class="trk"><i id="b1" style="background:#f9a8d4"></i></div></div>
        <div class="met"><div class="l">Critical ★<b id="m2">0/0</b></div><div class="trk"><i id="b2" style="background:#5ee6a0"></i></div></div>
        <div class="met"><div class="l">Kit packed<b id="m3">0/0</b></div><div class="trk"><i id="b3" style="background:#93c5fd"></i></div></div>
      </div>
    </div>
  </div>
  <div class="lh"><h3>Checklist</h3><button type="button" class="btn sm" id="editBtn">✏️ Edit</button></div>
  <div id="list"></div>
  <div id="editTools" style="display:none" class="btns one">
    <button type="button" class="btn bad" id="resetTpl">↺ Reset checklist to defaults</button>
  </div>
</section>

<!-- PHOTOS -->
<section class="tab" id="t-photos">
  <div class="card">
    <div class="ch"><div class="ic r">📸</div><h2>Work Photos</h2><span class="side" id="phCount">0</span></div>
    <p class="muted" style="margin:0">Each photo is stamped with phase & time. Take at least one <b style="color:var(--green)">AFTER</b> photo before you leave.</p>
    <div class="btns">
      <button type="button" class="btn" data-cam="before">📷 Before</button>
      <button type="button" class="btn ok" data-cam="after">📷 After</button>
    </div>
    <div class="btns one"><button type="button" class="btn" id="galBtn">🖼️ From gallery (After)</button></div>
    <input type="file" id="camIn" accept="image/*" capture="environment" hidden>
    <input type="file" id="galIn" accept="image/*" multiple hidden>
  </div>
  <div class="grid" id="photoGrid"></div>
</section>

<!-- HISTORY -->
<section class="tab" id="t-hist">
  <div class="lh"><h3>History</h3></div>
  <div id="histList"></div>
</section>
</main>

<nav aria-label="Main">
  <button type="button" data-tab="list" class="on" aria-label="Checklist"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M10.6 3.2a2 2 0 0 1 2.8 0l7 6.4c.4.4.6.9.6 1.5V19a2 2 0 0 1-2 2h-3.5a1 1 0 0 1-1-1v-4.5h-5V20a1 1 0 0 1-1 1H5a2 2 0 0 1-2-2v-7.9c0-.6.2-1.1.6-1.5z"/></svg></button>
  <button type="button" data-tab="photos" aria-label="Photos"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M9 3h6l1.6 2H20a2 2 0 0 1 2 2v11a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V7a2 2 0 0 1 2-2h3.4zm3 5a4.5 4.5 0 1 0 0 9 4.5 4.5 0 0 0 0-9zm0 2.2a2.3 2.3 0 1 1 0 4.6 2.3 2.3 0 0 1 0-4.6z"/></svg></button>
  <div class="gap"></div>
  <button type="button" data-tab="hist" aria-label="History"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M7 2a1 1 0 0 1 1 1v1h8V3a1 1 0 1 1 2 0v1h1a3 3 0 0 1 3 3v12a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3V7a3 3 0 0 1 3-3h1V3a1 1 0 0 1 1-1zM4 10v9a1 1 0 0 0 1 1h14a1 1 0 0 0 1-1v-9zm3 2h2v2H7zm4 0h2v2h-2zm4 0h2v2h-2zm-8 4h2v2H7zm4 0h2v2h-2z"/></svg></button>
  <button type="button" id="finishBtn" aria-label="Finish visit"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M5 2a1 1 0 0 1 1 1v.3C7.3 2.8 8.7 2.6 10.3 3c1.3.3 2.4.9 3.6 1.2 1.4.3 3 .2 5.2-.9a1 1 0 0 1 1.4.9v9a1 1 0 0 1-.6.9c-2.6 1.3-4.6 1.4-6.5 1-1.3-.3-2.4-.9-3.6-1.2-1.3-.3-2.6-.3-3.8.3V21a1 1 0 1 1-2 0V3a1 1 0 0 1 1-1z"/></svg></button>
  <button type="button" id="fab" aria-label="Take AFTER photo"><span><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round"><path d="M12 5v14M5 12h14"/></svg></span></button>
</nav>

<div class="ov" id="report">
  <div class="rbar">
    <button type="button" class="btn" id="rClose">✖ Close</button>
    <button type="button" class="btn" id="rPrint">🖨️ PDF</button>
    <button type="button" class="btn p" id="rShare">📤 Share</button>
  </div>
  <div class="rep" id="repBody"></div>
</div>
<div class="ov" id="viewer"><div class="rbar"><button type="button" class="btn" id="vClose">✖ Close</button></div><img id="vImg" alt="Photo"></div>
<div id="toast" aria-live="polite"></div>

<script>
(function(){
const $=s=>document.querySelector(s), $$=s=>[...document.querySelectorAll(s)];
const uid=()=>Date.now().toString(36)+Math.random().toString(36).slice(2,6);
const esc=s=>String(s??'').replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const fmt=t=>t?new Date(t).toLocaleString([], {dateStyle:'medium',timeStyle:'short'}):'—';
const load=k=>{try{return JSON.parse(localStorage.getItem(k))}catch(e){return null}};
const store=(k,v)=>{try{localStorage.setItem(k,JSON.stringify(v));return true}catch(e){toast('⚠️ Storage full – delete old visits');return false}};
function toast(m){const t=$('#toast');t.textContent=m;t.classList.add('on');clearTimeout(t._h);t._h=setTimeout(()=>t.classList.remove('on'),2200)}
function dur(a,b){if(!a)return'';const m=Math.max(0,Math.round(((b||Date.now())-a)/60000));return Math.floor(m/60)+'h '+(m%60)+'m'}

/* ---------- Greeting ---------- */
function renderGreet(){const d=new Date(),h=d.getHours();
  $('#hDate').textContent=d.toLocaleDateString('en-US',{weekday:'long',month:'short',day:'numeric'});
  $('#hGreet').textContent=h<12?'Good morning':h<17?'Good afternoon':'Good evening';}

/* ---------- Default checklist ---------- */
const mk=(id,title,icon,arr)=>({id,title,icon,items:arr.map(t=>({id:uid(),text:t.replace(/^!/,''),crit:t[0]==='!'}))});
const DEFAULT=()=>[
 mk('prep','Before Departure','🧭',['!Confirm appointment & on-site contact','Review ticket scope & previous visit notes','Download firmware / installers / licenses needed','!Credentials ready (password vault, VPN, admin accounts)','Spare parts for this job loaded in car','Phone & laptop charged']),
 mk('arrive','On Arrival','📍',['Check in with contact & confirm scope','!Take BEFORE photos (rack, desk, cabling)','Note existing damage / issues before touching anything','!Backup configs before changes (firewall, switch, router)','Check UPS / power status']),
 mk('work','Work & Testing','🛠️',['!Issue resolved & tested with the end user','!Internet & network connectivity verified','Wi-Fi / VLAN / DHCP working as expected','Printers, shared drives, email tested','Devices online in cloud dashboard (Meraki / UniFi / Intune)','!Config saved (write mem) & backup exported','Windows / firmware / AV status checked']),
 mk('sec','Security & Documentation','🔐',['!Temporary accounts / passwords removed','!Logged out of all admin sessions on client PCs','Changed passwords stored in vault','Documentation updated (IPs, diagram, asset list)','Cables & ports labeled']),
 mk('clean','Site Cleanup','🧹',['!Take AFTER photos','Packaging & cable offcuts removed','Cables tidied (velcro / ties)','Rack / cabinet doors closed & locked','Ceiling tiles / floor boxes put back','Equipment powered on & LEDs normal']),
 mk('kit','My Kit – Packed?','🎒',['!Laptop','!Laptop charger','!Console cable (USB / RJ45)','USB-Ethernet adapter','Cable tester','Crimper & RJ45 connectors','Screwdriver set','Spare patch cables','Bootable USB drive','Label maker','Flashlight','Power bank / phone charger','Velcro & cable ties','!Faulty / RMA parts collected','!Client keys / access card returned']),
 mk('hand','Client Handoff','🤝',['!Explained work done to client','Follow-up items agreed / next visit booked','Client satisfaction confirmed'])
];
const ICB={prep:'',arrive:'r',work:'',sec:'b',clean:'g',kit:'b',hand:'r'};

let tpl=load('fc_tpl')||DEFAULT();
let hist=load('fc_hist')||[];
const newVisit=()=>({id:uid(),created:Date.now(),visit:{client:''},checkIn:Date.now(),checkOut:null,sections:tpl.map(s=>({id:s.id,title:s.title,icon:s.icon,items:s.items.map(i=>({...i,done:false}))})),photos:[]});
let cur=load('fc_cur')||newVisit();
let edit=false, openSecs=new Set(['prep']), photoCache={}, camPhase='after', reportVisit=null;
const save=()=>store('fc_cur',cur), saveTpl=()=>store('fc_tpl',tpl), saveHist=()=>store('fc_hist',hist);

/* ---------- IndexedDB for photos ---------- */
const DB=new Promise((res,rej)=>{const r=indexedDB.open('fieldcheck',1);r.onupgradeneeded=()=>r.result.createObjectStore('photos',{keyPath:'id'});r.onsuccess=()=>res(r.result);r.onerror=()=>rej(r.error)});
async function idb(mode,fn){const db=await DB;return new Promise((res,rej)=>{const tx=db.transaction('photos',mode);const r=fn(tx.objectStore('photos'));tx.oncomplete=()=>res(r&&r.result);tx.onerror=()=>rej(tx.error)})}
const idbPut=o=>idb('readwrite',s=>s.put(o));
const idbDel=id=>idb('readwrite',s=>s.delete(id));
async function photosFor(vid){const all=await idb('readonly',s=>s.getAll())||[];const m={};all.filter(p=>p.visit===vid).forEach(p=>m[p.id]=p.data);return m}

/* ---------- Progress dashboard ---------- */
function stats(v){let t=0,d=0;v.sections.forEach(s=>s.items.forEach(i=>{t++;if(i.done)d++}));return{t,d,pct:t?Math.round(d/t*100):0}}
function sub(v,f){let t=0,d=0;v.sections.forEach(s=>s.items.forEach(i=>{if(f(s,i)){t++;if(i.done)d++}}));return{t,d,p:t?d/t:0}}
function ring(id,r,p){const c=2*Math.PI*r,e=$(id);e.style.strokeDasharray=c;e.style.strokeDashoffset=c*(1-Math.min(1,Math.max(0,p)))}
function renderHeader(){
  const s=stats(cur),cr=sub(cur,(s,i)=>i.crit),kt=sub(cur,s=>s.id==='kit');
  $('#hPct').textContent=s.pct+'%';
  $('#m1').textContent=`${s.d}/${s.t}`;$('#m2').textContent=`${cr.d}/${cr.t}`;$('#m3').textContent=`${kt.d}/${kt.t}`;
  $('#b1').style.width=s.pct+'%';$('#b2').style.width=cr.p*100+'%';$('#b3').style.width=kt.p*100+'%';
  ring('#r1',62,s.t?s.d/s.t:0);ring('#r2',46,cr.p);ring('#r3',30,kt.p);
  $('#dTime').textContent='⏱ '+dur(cur.checkIn);
}

/* ---------- Checklist ---------- */
function renderList(){
  $('#list').innerHTML=cur.sections.map(s=>{
    const d=s.items.filter(i=>i.done).length,full=s.items.length&&d===s.items.length,p=s.items.length?d/s.items.length*100:0;
    return `<details class="sec" data-s="${s.id}" ${openSecs.has(s.id)?'open':''}>
      <summary><span class="ic ${ICB[s.id]||''}">${s.icon}</span><span class="t">${esc(s.title)}</span><span class="cnt ${full?'full':''}">${d}/${s.items.length}</span></summary>
      <div class="mini"><i style="width:${p}%"></i></div>
      ${s.items.map(i=>`<div class="it ${i.done?'done':''}">
        <label><input type="checkbox" data-s="${s.id}" data-i="${i.id}" ${i.done?'checked':''}><span>${esc(i.text)}</span>${i.crit&&!edit?'<b class="crit">★</b>':''}</label>
        ${edit?`<button type="button" class="ib ${i.crit?'on':''}" data-act="crit" data-s="${s.id}" data-i="${i.id}" aria-label="Toggle critical">★</button><button type="button" class="ib" data-act="del" data-s="${s.id}" data-i="${i.id}" aria-label="Delete item">🗑</button>`:''}
      </div>`).join('')}
      ${edit?`<form class="add" data-s="${s.id}"><input type="text" placeholder="Add item…" aria-label="New item"><button class="btn p sm">Add</button></form>`:''}
    </details>`}).join('');
  $('#editBtn').textContent=edit?'✔ Done':'✏️ Edit';
  $('#editTools').style.display=edit?'grid':'none';
}
const L=$('#list');
L.addEventListener('toggle',e=>{const d=e.target;if(d.dataset&&d.dataset.s){d.open?openSecs.add(d.dataset.s):openSecs.delete(d.dataset.s)}},true);
L.addEventListener('change',e=>{
  const c=e.target;if(c.type!=='checkbox')return;
  const it=cur.sections.find(s=>s.id===c.dataset.s).items.find(i=>i.id===c.dataset.i);
  it.done=c.checked;save();renderList();renderHeader();
  if(navigator.vibrate)navigator.vibrate(15);
});
L.addEventListener('click',e=>{
  const b=e.target.closest('[data-act]');if(!b)return;
  const sid=b.dataset.s,iid=b.dataset.i,secs=[cur.sections,tpl].map(a=>a.find(s=>s.id===sid)).filter(Boolean);
  if(b.dataset.act==='del'){secs.forEach(s=>s.items=s.items.filter(i=>i.id!==iid))}
  else secs.forEach(s=>{const i=s.items.find(x=>x.id===iid);if(i)i.crit=!i.crit});
  save();saveTpl();renderList();renderHeader();
});
L.addEventListener('submit',e=>{
  e.preventDefault();const f=e.target,inp=f.querySelector('input'),txt=inp.value.trim();if(!txt)return;
  const id=uid(),sid=f.dataset.s;
  cur.sections.find(s=>s.id===sid).items.push({id,text:txt,crit:false,done:false});
  const ts=tpl.find(s=>s.id===sid);if(ts)ts.items.push({id,text:txt,crit:false});
  save();saveTpl();renderList();renderHeader();
  const ni=$(`form.add[data-s="${sid}"] input`);if(ni)ni.focus();
});
$('#editBtn').addEventListener('click',()=>{edit=!edit;renderList()});
$('#resetTpl').addEventListener('click',()=>{if(!confirm('Reset checklist to defaults? Custom items will be removed.'))return;tpl=DEFAULT();saveTpl();cur.sections=newVisit().sections;save();renderList();renderHeader();toast('Checklist reset')});

/* ---------- Photos ---------- */
function compress(file,phase){return new Promise((res,rej)=>{
  const img=new Image(),url=URL.createObjectURL(file);
  img.onload=()=>{const max=1280,s=Math.min(1,max/Math.max(img.width,img.height)),w=Math.round(img.width*s),h=Math.round(img.height*s);
    const c=document.createElement('canvas');c.width=w;c.height=h;const x=c.getContext('2d');x.drawImage(img,0,0,w,h);
    const fs=Math.max(14,Math.round(w/45)),bh=fs*1.9;x.fillStyle='rgba(27,16,54,.7)';x.fillRect(0,h-bh,w,bh);
    x.fillStyle='#fff';x.font=`700 ${fs}px sans-serif`;x.textBaseline='middle';
    x.fillText(`${phase.toUpperCase()} · ${new Date().toLocaleString()}`,fs*.6,h-bh/2,w-fs);
    URL.revokeObjectURL(url);res(c.toDataURL('image/jpeg',.72))};
  img.onerror=()=>{URL.revokeObjectURL(url);rej()};img.src=url})}
async function addPhotos(files,phase){
  let n=0;
  for(const f of files){try{const data=await compress(f,phase),id=uid();await idbPut({id,visit:cur.id,data});photoCache[id]=data;cur.photos.push({id,phase,caption:'',ts:Date.now()});n++}catch(e){toast('Could not read image')}}
  if(n){if(phase==='after')autoTick('clean','AFTER photos');if(phase==='before')autoTick('arrive','BEFORE photos');save();renderPhotos();renderList();renderHeader();toast(`${n} ${phase} photo${n>1?'s':''} saved`)}
}
function autoTick(sid,needle){const s=cur.sections.find(x=>x.id===sid);if(!s)return;const i=s.items.find(x=>x.text.includes(needle));if(i)i.done=true}
function renderPhotos(){
  const g=$('#photoGrid');$('#phCount').textContent=cur.photos.length+' saved';
  if(!cur.photos.length){g.innerHTML='<div class="empty">No photos yet</div>';return}
  g.innerHTML=cur.photos.map(p=>`<div class="ph"><img src="${photoCache[p.id]||''}" data-id="${p.id}" alt="${p.phase} photo">
    <div class="m"><span class="badge ${p.phase}">${p.phase.toUpperCase()}</span><input type="text" data-cap="${p.id}" value="${esc(p.caption)}" placeholder="Caption" aria-label="Caption"><button type="button" class="ib" data-pdel="${p.id}" aria-label="Delete photo">🗑</button></div></div>`).join('');
}
$$('[data-cam]').forEach(b=>b.addEventListener('click',()=>{camPhase=b.dataset.cam;$('#camIn').click()}));
$('#fab').addEventListener('click',()=>{camPhase='after';$('#camIn').click()});
$('#galBtn').addEventListener('click',()=>$('#galIn').click());
$('#camIn').addEventListener('change',e=>{addPhotos([...e.target.files],camPhase);e.target.value=''});
$('#galIn').addEventListener('change',e=>{addPhotos([...e.target.files],'after');e.target.value=''});
$('#photoGrid').addEventListener('input',e=>{const id=e.target.dataset.cap;if(!id)return;cur.photos.find(p=>p.id===id).caption=e.target.value;save()});
$('#photoGrid').addEventListener('click',async e=>{
  const d=e.target.dataset;
  if(d.pdel){if(!confirm('Delete this photo?'))return;cur.photos=cur.photos.filter(p=>p.id!==d.pdel);await idbDel(d.pdel);delete photoCache[d.pdel];save();renderPhotos()}
  else if(d.id){$('#vImg').src=photoCache[d.id];$('#viewer').classList.add('on')}
});
$('#vClose').addEventListener('click',()=>$('#viewer').classList.remove('on'));

/* ---------- Open items ---------- */
function openItems(){
  const issues=[];
  cur.sections.forEach(s=>s.items.forEach(i=>{if(!i.done&&(i.crit||s.id==='kit'))issues.push(`${s.icon} ${i.text}`)}));
  if(!cur.photos.some(p=>p.phase==='after'))issues.push('📸 No AFTER photo taken');
  return issues;
}

/* ---------- Report ---------- */
function reportText(v){
  const s=stats(v),L=[`IT SITE VISIT REPORT`,`Client: ${v.visit.client||'—'}`,`Started: ${fmt(v.checkIn)}`,`Finished: ${fmt(v.checkOut)}`,`Time on site: ${dur(v.checkIn,v.checkOut)||'—'}`,`Checklist: ${s.d}/${s.t} (${s.pct}%)`,``];
  v.sections.forEach(sec=>{L.push(sec.title.toUpperCase());sec.items.forEach(i=>L.push(`${i.done?'✔':'✘'} ${i.text}`));L.push('')});
  L.push(`Photos: ${v.photos.filter(p=>p.phase==='before').length} before, ${v.photos.filter(p=>p.phase==='after').length} after`);
  return L.join('\n');
}
async function showReport(v){
  reportVisit=v;const pics=v.id===cur.id?photoCache:await photosFor(v.id),s=stats(v),row=(k,x)=>`<tr><td><b>${k}</b></td><td>${esc(x)||'—'}</td></tr>`;
  $('#repBody').innerHTML=`<h1>IT Site Visit Report</h1><div style="color:#666;font-size:13px">Generated ${fmt(Date.now())}</div>
  <h3>Visit</h3><table>${row('Client',v.visit.client)}${row('Started',fmt(v.checkIn))}${row('Finished',fmt(v.checkOut))}${row('Time on site',dur(v.checkIn,v.checkOut))}${row('Checklist',`${s.d}/${s.t} (${s.pct}%)`)}</table>
  ${v.sections.map(sec=>`<h3>${sec.icon} ${esc(sec.title)}</h3><table>${sec.items.map(i=>`<tr><td style="width:24px" class="${i.done?'y':'n'}">${i.done?'✔':'✘'}</td><td>${esc(i.text)}</td></tr>`).join('')}</table>`).join('')}
  ${v.photos.length?`<h3>Photos</h3><div class="pg">${v.photos.map(p=>pics[p.id]?`<figure><img src="${pics[p.id]}" alt=""><figcaption><b>${p.phase.toUpperCase()}</b> ${esc(p.caption)}</figcaption></figure>`:'').join('')}</div>`:''}`;
  reportVisit._pics=pics;$('#report').classList.add('on');window.scrollTo(0,0);
}
$('#rClose').addEventListener('click',()=>$('#report').classList.remove('on'));
$('#rPrint').addEventListener('click',()=>window.print());
$('#rShare').addEventListener('click',async()=>{
  const v=reportVisit,text=reportText(v),title=`Visit report – ${v.visit.client||'Client'}`;
  try{
    const files=await Promise.all(v.photos.filter(p=>v._pics[p.id]).map(async(p,i)=>{const b=await (await fetch(v._pics[p.id])).blob();return new File([b],`${p.phase}-${i+1}.jpg`,{type:'image/jpeg'})}));
    if(files.length&&navigator.canShare&&navigator.canShare({files})){await navigator.share({title,text,files});return}
    if(navigator.share){await navigator.share({title,text});return}
    await navigator.clipboard.writeText(text);toast('Report copied to clipboard');
  }catch(e){if(e.name!=='AbortError'){try{await navigator.clipboard.writeText(text);toast('Report copied to clipboard')}catch(_){toast('Sharing not available – use PDF')}}}
});

/* ---------- Finish & history ---------- */
$('#finishBtn').addEventListener('click',()=>{
  const issues=openItems();
  if(issues.length&&!confirm(`${issues.length} item(s) still open:\n\n• ${issues.slice(0,8).join('\n• ')}${issues.length>8?'\n…':''}\n\nFinish anyway?`))return;
  const nm=prompt('Client name for this visit (optional):',cur.visit.client||'');if(nm===null)return;
  cur.visit.client=nm.trim();cur.checkOut=Date.now();if(!cur.checkIn)cur.checkIn=cur.created;
  hist.unshift(cur);if(!saveHist()){hist.shift();return}
  cur=newVisit();photoCache={};save();renderAll();switchTab('hist');toast('Visit saved 👍');
});
function miniRing(p){const c=2*Math.PI*20;return `<svg class="pct" viewBox="0 0 52 52"><circle cx="26" cy="26" r="20" fill="none" stroke="rgba(255,255,255,.1)" stroke-width="6"/><circle cx="26" cy="26" r="20" fill="none" stroke="#c084fc" stroke-width="6" stroke-linecap="round" stroke-dasharray="${c}" stroke-dashoffset="${c*(1-p/100)}" transform="rotate(-90 26 26)"/><text x="26" y="30" text-anchor="middle" font-size="12" font-weight="800" fill="#f4f1ff">${p}</text></svg>`}
function renderHist(){
  $('#histList').innerHTML=hist.length?hist.map((v,i)=>{const s=stats(v);return `<div class="card"><div class="hrow">${miniRing(s.pct)}<div style="min-width:0"><b>${esc(v.visit.client)||'Unnamed client'}</b><div class="muted">${fmt(v.checkIn)}</div><div class="muted">⏱ ${dur(v.checkIn,v.checkOut)} · 📸 ${v.photos.length}</div></div></div>
  <div class="btns"><button type="button" class="btn p" data-hv="${i}">📄 Report</button><button type="button" class="btn bad" data-hd="${i}">🗑 Delete</button></div></div>`}).join(''):'<div class="card empty">No completed visits yet.<br>Tap the 🏁 flag to finish a visit.</div>';
}
$('#histList').addEventListener('click',async e=>{
  const d=e.target.dataset;
  if(d.hv!==undefined)showReport(hist[+d.hv]);
  if(d.hd!==undefined){const v=hist[+d.hd];if(!confirm(`Delete visit "${v.visit.client||'Unnamed'}" and its photos?`))return;for(const p of v.photos)await idbDel(p.id);hist.splice(+d.hd,1);saveHist();renderHist()}
});

/* ---------- Tabs ---------- */
function switchTab(t){
  $$('nav button[data-tab]').forEach(b=>b.classList.toggle('on',b.dataset.tab===t));
  $$('.tab').forEach(s=>s.classList.toggle('on',s.id==='t-'+t));
  if(t==='hist')renderHist();
  window.scrollTo(0,0);
}
$$('nav button[data-tab]').forEach(b=>b.addEventListener('click',()=>switchTab(b.dataset.tab)));

function renderAll(){renderGreet();renderList();renderPhotos();renderHeader()}
renderAll();
setInterval(()=>{renderGreet();$('#dTime').textContent='⏱ '+dur(cur.checkIn)},60000);
photosFor(cur.id).then(m=>{photoCache=m;renderPhotos()}).catch(()=>toast('Photo storage unavailable'));
})();
</script>
</body>
</html>
