<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#0f6cbd">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-title" content="FieldCheck">
<title>FieldCheck – IT Site Visit</title>
<style>
:root{--bg:#f3f5f8;--card:#fff;--tx:#1b1f24;--mut:#6b7280;--bd:#e3e7ee;--pri:#0f6cbd;--ok:#138a3e;--warn:#b26f00;--bad:#c42b1c;--chip:#eef3fa}
@media (prefers-color-scheme:dark){:root{--bg:#0f1115;--card:#1a1d23;--tx:#e8eaed;--mut:#9aa1ab;--bd:#2a2f37;--pri:#4ea1ff;--ok:#3ccf6e;--warn:#f0b429;--bad:#ff6b5e;--chip:#222833}}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
body{margin:0;font:16px/1.4 -apple-system,"Segoe UI",Roboto,sans-serif;background:var(--bg);color:var(--tx);padding-bottom:calc(76px + env(safe-area-inset-bottom))}
header{position:sticky;top:0;z-index:5;background:#0f6cbd;color:#fff;padding:calc(10px + env(safe-area-inset-top)) 16px 10px;box-shadow:0 2px 8px rgba(0,0,0,.15)}
header .row{display:flex;justify-content:space-between;align-items:center;gap:8px}
header h1{font-size:18px;margin:0;white-space:nowrap}
header small{opacity:.9;font-size:13px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;flex:1;text-align:right}
#finishBtn{border:0;border-radius:8px;padding:7px 10px;background:#fff;color:#0f6cbd;font-weight:700;font-size:13px;cursor:pointer;flex:none}
.bar{height:8px;background:rgba(255,255,255,.3);border-radius:8px;margin-top:8px;overflow:hidden}
.bar i{display:block;height:100%;background:#7CFC9A;width:0;transition:width .3s}
main{padding:12px;max-width:720px;margin:0 auto}
.tab{display:none}.tab.on{display:block}
.card{background:var(--card);border:1px solid var(--bd);border-radius:14px;padding:14px;margin-bottom:12px}
.card h2{font-size:16px;margin:0 0 10px}
input[type=text]{width:100%;padding:12px;border:1px solid var(--bd);border-radius:10px;background:var(--bg);color:var(--tx);font-size:16px}
input:focus,button:focus-visible,summary:focus-visible{outline:2px solid var(--pri);outline-offset:1px}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:6px;padding:12px 14px;border-radius:10px;border:1px solid var(--bd);background:var(--chip);color:var(--tx);font-size:15px;font-weight:600;text-decoration:none;cursor:pointer}
.btn.p{background:var(--pri);border-color:var(--pri);color:#fff}
.btn.ok{background:var(--ok);border-color:var(--ok);color:#fff}
.btn.bad{color:var(--bad)}
.btns{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:10px}
.btns.one{grid-template-columns:1fr}
.muted{color:var(--mut);font-size:13px}
details.sec{background:var(--card);border:1px solid var(--bd);border-radius:14px;margin-bottom:10px;overflow:hidden}
summary{list-style:none;display:flex;justify-content:space-between;align-items:center;padding:14px;font-weight:700;cursor:pointer}
summary::-webkit-details-marker{display:none}
.cnt{font-size:13px;padding:3px 9px;border-radius:20px;background:var(--chip);color:var(--mut)}
.cnt.full{background:var(--ok);color:#fff}
.it{display:flex;align-items:center;border-top:1px solid var(--bd)}
.it label{flex:1;display:flex;align-items:center;gap:12px;padding:12px 14px;cursor:pointer}
.it input{width:24px;height:24px;flex:none;accent-color:var(--ok)}
.it.done span{color:var(--mut);text-decoration:line-through}
.crit{color:var(--warn);font-size:14px}
.ib{border:0;background:none;font-size:18px;padding:10px;cursor:pointer;color:var(--mut)}
.ib.on{color:var(--warn)}
form.add{display:flex;gap:8px;padding:10px 14px;border-top:1px solid var(--bd)}
form.add input{flex:1}
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(140px,1fr));gap:10px}
.ph{background:var(--card);border:1px solid var(--bd);border-radius:12px;overflow:hidden}
.ph img{width:100%;aspect-ratio:4/3;object-fit:cover;display:block;cursor:pointer}
.ph .m{padding:6px;display:flex;gap:4px;align-items:center}
.ph .m input{padding:6px;font-size:13px;border-radius:6px}
.badge{font-size:11px;font-weight:700;padding:2px 6px;border-radius:6px;color:#fff}
.badge.before{background:#7a5af8}.badge.after{background:var(--ok)}
nav{position:fixed;bottom:0;left:0;right:0;display:flex;background:var(--card);border-top:1px solid var(--bd);padding-bottom:env(safe-area-inset-bottom);z-index:6}
nav button{flex:1;border:0;background:none;color:var(--mut);padding:8px 0 10px;font-size:11px;display:flex;flex-direction:column;align-items:center;gap:2px;cursor:pointer}
nav button span{font-size:20px}
nav button.on{color:var(--pri);font-weight:700}
.hi{display:flex;justify-content:space-between;align-items:center;gap:8px}
#toast{position:fixed;left:50%;bottom:90px;transform:translateX(-50%);background:#222;color:#fff;padding:10px 16px;border-radius:20px;font-size:14px;opacity:0;transition:opacity .25s;pointer-events:none;z-index:20}
#toast.on{opacity:1}
.ov{position:fixed;inset:0;background:var(--bg);z-index:30;overflow:auto;display:none}
.ov.on{display:block}
.rbar{position:sticky;top:0;display:flex;gap:8px;padding:calc(10px + env(safe-area-inset-top)) 12px 10px;background:var(--card);border-bottom:1px solid var(--bd)}
.rbar .btn{flex:1;padding:10px 6px;font-size:14px}
.rep{padding:16px;max-width:800px;margin:0 auto;background:#fff;color:#111}
.rep h1{font-size:20px;margin:0 0 4px}.rep h3{margin:16px 0 6px;font-size:15px;border-bottom:2px solid #0f6cbd;padding-bottom:3px}
.rep table{width:100%;border-collapse:collapse;font-size:13px}
.rep td{padding:4px 6px;border-bottom:1px solid #eee;vertical-align:top}
.rep .pg{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.rep .pg figure{margin:0}.rep .pg img{width:100%;border-radius:6px}
.rep figcaption{font-size:12px;color:#555}
.rep .y{color:#138a3e;font-weight:700}.rep .n{color:#c42b1c;font-weight:700}
#viewer img{max-width:100%;display:block;margin:0 auto}
@media print{body{padding:0;background:#fff}body>*:not(#report){display:none!important}#report{position:static;display:block}.rbar{display:none}.rep{max-width:none}.rep figure{break-inside:avoid}}
</style>
</head>
<body>
<header>
  <div class="row"><h1>✅ FieldCheck</h1><small id="hClient">New visit</small><button type="button" id="finishBtn">🏁 Finish</button></div>
  <div class="bar"><i id="hBar"></i></div>
</header>

<main>
<!-- CHECKLIST -->
<section class="tab on" id="t-list">
  <div class="hi" style="margin-bottom:10px">
    <span class="muted">★ = critical</span>
    <button type="button" class="btn" id="editBtn">✏️ Edit list</button>
  </div>
  <div id="list"></div>
  <div id="editTools" style="display:none" class="btns one">
    <button type="button" class="btn bad" id="resetTpl">↺ Reset checklist to defaults</button>
  </div>
</section>

<!-- PHOTOS -->
<section class="tab" id="t-photos">
  <div class="card">
    <h2>📸 Work photos</h2>
    <p class="muted" style="margin:0">Photos are stamped with phase and time. Take at least one <b>AFTER</b> photo before leaving (rack, cabling, labels, devices).</p>
    <div class="btns">
      <button type="button" class="btn" data-cam="before">📷 Before</button>
      <button type="button" class="btn ok" data-cam="after">📷 After</button>
    </div>
    <div class="btns one"><button type="button" class="btn" id="galBtn">🖼️ Add from gallery (as After)</button></div>
    <input type="file" id="camIn" accept="image/*" capture="environment" hidden>
    <input type="file" id="galIn" accept="image/*" multiple hidden>
  </div>
  <div class="grid" id="photoGrid"></div>
</section>

<!-- HISTORY -->
<section class="tab" id="t-hist">
  <div id="histList"></div>
</section>
</main>

<nav>
  <button type="button" data-tab="list" class="on"><span>☑️</span>Checklist</button>
  <button type="button" data-tab="photos"><span>📸</span>Photos</button>
  <button type="button" data-tab="hist"><span>🕘</span>History</button>
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

/* ---------- Header / progress ---------- */
function stats(v){let t=0,d=0;v.sections.forEach(s=>s.items.forEach(i=>{t++;if(i.done)d++}));return{t,d,pct:t?Math.round(d/t*100):0}}
function renderHeader(){const s=stats(cur);$('#hBar').style.width=s.pct+'%';$('#hClient').textContent=s.d+'/'+s.t+' · '+s.pct+'%'}

/* ---------- Checklist tab ---------- */
function renderList(){
  $('#list').innerHTML=cur.sections.map(s=>{
    const d=s.items.filter(i=>i.done).length,full=s.items.length&&d===s.items.length;
    return `<details class="sec" data-s="${s.id}" ${openSecs.has(s.id)?'open':''}>
      <summary><span>${s.icon} ${esc(s.title)}</span><span class="cnt ${full?'full':''}">${d}/${s.items.length}</span></summary>
      ${s.items.map(i=>`<div class="it ${i.done?'done':''}">
        <label><input type="checkbox" data-s="${s.id}" data-i="${i.id}" ${i.done?'checked':''}><span>${esc(i.text)}</span>${i.crit&&!edit?'<b class="crit">★</b>':''}</label>
        ${edit?`<button type="button" class="ib ${i.crit?'on':''}" data-act="crit" data-s="${s.id}" data-i="${i.id}" aria-label="Toggle critical">★</button><button type="button" class="ib" data-act="del" data-s="${s.id}" data-i="${i.id}" aria-label="Delete item">🗑</button>`:''}
      </div>`).join('')}
      ${edit?`<form class="add" data-s="${s.id}"><input type="text" placeholder="Add item…" aria-label="New item"><button class="btn p">Add</button></form>`:''}
    </details>`}).join('');
  $('#editBtn').textContent=edit?'✔ Done':'✏️ Edit list';
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
    const fs=Math.max(14,Math.round(w/45)),bh=fs*1.9;x.fillStyle='rgba(0,0,0,.55)';x.fillRect(0,h-bh,w,bh);
    x.fillStyle='#fff';x.font=`600 ${fs}px sans-serif`;x.textBaseline='middle';
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
  const g=$('#photoGrid');
  if(!cur.photos.length){g.innerHTML='<p class="muted">No photos yet.</p>';return}
  g.innerHTML=cur.photos.map(p=>`<div class="ph"><img src="${photoCache[p.id]||''}" data-id="${p.id}" alt="${p.phase} photo">
    <div class="m"><span class="badge ${p.phase}">${p.phase.toUpperCase()}</span><input type="text" data-cap="${p.id}" value="${esc(p.caption)}" placeholder="Caption" aria-label="Caption"><button type="button" class="ib" data-pdel="${p.id}" aria-label="Delete photo">🗑</button></div></div>`).join('');
}
$$('[data-cam]').forEach(b=>b.addEventListener('click',()=>{camPhase=b.dataset.cam;$('#camIn').click()}));
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

/* ---------- Open items check ---------- */
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
  $('#repBody').innerHTML=`<h1>IT Site Visit Report</h1><div style="color:#555;font-size:13px">Generated ${fmt(Date.now())}</div>
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
  cur=newVisit();photoCache={};save();renderAll();switchTab('hist');toast('Visit saved to history 👍');
});
function renderHist(){
  $('#histList').innerHTML=hist.length?hist.map((v,i)=>{const s=stats(v);return `<div class="card"><div><b>${esc(v.visit.client)||'Unnamed client'}</b><div class="muted">${fmt(v.checkIn)} · ${dur(v.checkIn,v.checkOut)} · ${s.pct}% · ${v.photos.length} 📸</div></div>
  <div class="btns"><button type="button" class="btn" data-hv="${i}">📄 Report</button><button type="button" class="btn bad" data-hd="${i}">🗑 Delete</button></div></div>`}).join(''):'<p class="muted">No completed visits yet. Tap 🏁 Finish to save a visit.</p>';
}
$('#histList').addEventListener('click',async e=>{
  const d=e.target.dataset;
  if(d.hv!==undefined)showReport(hist[+d.hv]);
  if(d.hd!==undefined){const v=hist[+d.hd];if(!confirm(`Delete visit "${v.visit.client||'Unnamed'}" and its photos?`))return;for(const p of v.photos)await idbDel(p.id);hist.splice(+d.hd,1);saveHist();renderHist()}
});

/* ---------- Tabs ---------- */
function switchTab(t){
  $$('nav button').forEach(b=>b.classList.toggle('on',b.dataset.tab===t));
  $$('.tab').forEach(s=>s.classList.toggle('on',s.id==='t-'+t));
  if(t==='hist')renderHist();
  window.scrollTo(0,0);
}
$$('nav button').forEach(b=>b.addEventListener('click',()=>switchTab(b.dataset.tab)));

function renderAll(){renderList();renderPhotos();renderHeader()}
renderAll();
photosFor(cur.id).then(m=>{photoCache=m;renderPhotos()}).catch(()=>toast('Photo storage unavailable'));
})();
</script>
</body>
</html>
