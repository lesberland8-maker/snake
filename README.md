# snake 
<!doctype html><html lang="fr"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover,user-scalable=no">
<title>Snake Family.io</title>
<style>
:root{--bg:#0b1020;--card:#161d36;--card2:#222c52;--tx:#f2f5ff;--mut:#8f9bc4;--ac:#46f0a0;--ac2:#ffb347;color-scheme:dark;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{height:100%;margin:0;background:var(--bg);color:var(--tx);font-family:system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;overflow:hidden;touch-action:none;user-select:none;-webkit-user-select:none}
body{position:relative}
#cv{position:fixed;inset:0;width:100%;height:100%}
.hide{display:none!important}
.scr{position:absolute;inset:0;display:none;flex-direction:column;background:radial-gradient(circle at 50% 0,#1b2650,var(--bg) 70%);z-index:5}
.scr.on{display:flex}
.pg{display:none;flex:1;flex-direction:column;align-items:center;gap:12px;padding:16px;overflow:auto;touch-action:pan-y}
.pg.on{display:flex}
h1{margin:4px 0;font-size:34px;letter-spacing:1px}h1 span{color:var(--ac)}
h2{margin:0;font-size:20px}
canvas.pv{width:170px;height:170px}
input[type=text]{background:var(--card);border:2px solid var(--card2);color:var(--tx);border-radius:12px;padding:10px 14px;font-size:16px;text-align:center;width:200px}
button{font:inherit;color:var(--tx);border:0;cursor:pointer}
.big{background:var(--ac);color:#04281a;font-weight:800;font-size:22px;padding:14px 56px;border-radius:40px;box-shadow:0 6px 0 #1e9e68}
.big:active{transform:translateY(4px);box-shadow:0 2px 0 #1e9e68}
.ghost{background:var(--card2);padding:12px 22px;border-radius:30px;font-weight:600}
#nav{display:flex;background:var(--card);border-top:1px solid var(--card2)}
#nav button{flex:1;background:none;padding:14px 4px;color:var(--mut);font-size:13px;font-weight:600}
#nav button.on{color:var(--ac)}
.stats{display:flex;gap:10px;width:100%;max-width:420px}
.stats div{flex:1;background:var(--card);border-radius:14px;padding:10px;text-align:center}
.stats b{display:block;font-size:20px}.stats small,small{color:var(--mut)}
.bar{width:100%;max-width:420px;height:12px;background:var(--card);border-radius:8px;overflow:hidden}
.bar i{display:block;height:100%;background:linear-gradient(90deg,var(--ac),var(--ac2));width:0}
.grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;width:100%;max-width:420px}
.cell{background:var(--card);border:2px solid transparent;border-radius:14px;padding:8px;display:flex;flex-direction:column;align-items:center;gap:4px;font-size:13px}
.cell img{width:64px;height:64px;border-radius:50%;object-fit:cover;border:2px solid #fff}
.cell.sel{border-color:var(--ac)}.cell.lk{opacity:.45}.cell em{font-style:normal;font-size:11px;color:var(--ac2)}
.sw{display:block;width:64px;height:20px;border-radius:10px;margin:22px 0}
.rows{width:100%;max-width:420px;display:flex;flex-direction:column;gap:8px}
.row{display:flex;align-items:center;gap:10px;background:var(--card);border-radius:14px;padding:8px 12px;opacity:.55}
.row.got{opacity:1;border:1px solid var(--ac)}
.row img{width:40px;height:40px;border-radius:50%;object-fit:cover}.row .sw{width:40px;height:14px;margin:13px 0}
.row b{flex:1;font-size:14px}.row em{font-style:normal;font-size:12px;color:var(--ac)}
.lv{width:28px;height:28px;border-radius:50%;background:var(--card2);display:grid;place-items:center;font-weight:800;font-size:13px}
label{width:100%;max-width:420px;background:var(--card);border-radius:14px;padding:12px 14px;display:flex;flex-direction:column;gap:8px;font-size:15px}
label b{color:var(--ac);float:right}input[type=range]{width:100%;accent-color:var(--ac)}
#hud{position:absolute;inset:0;pointer-events:none;z-index:2}
#sc{position:absolute;left:12px;top:calc(env(safe-area-inset-top,0px) + 10px);font-weight:800;font-size:18px;background:#0008;padding:6px 12px;border-radius:12px}
#lb{position:absolute;right:10px;top:calc(env(safe-area-inset-top,0px) + 10px);font-size:12px;background:#0008;padding:6px 10px;border-radius:12px;min-width:120px}
#lb div{display:flex;justify-content:space-between;gap:10px}#lb .me{color:var(--ac);font-weight:700}
#bst{position:absolute;right:22px;bottom:calc(env(safe-area-inset-bottom,0px) + 30px);width:84px;height:84px;border-radius:50%;background:#ffb347cc;font-size:34px;pointer-events:auto;touch-action:none;box-shadow:0 0 0 4px #fff3}
#bst:active{background:#ff8a1f}
#jb{position:fixed;z-index:3;border-radius:50%;border:2px solid #fff6;background:#ffffff14;transform:translate(-50%,-50%);pointer-events:none}
#jk{position:absolute;left:50%;top:50%;width:46%;height:46%;border-radius:50%;background:#fffc;transform:translate(-50%,-50%)}
#dead{justify-content:center;align-items:center;gap:12px;text-align:center;padding:20px;background:#0b1020ee}
</style></head><body>
<canvas id="cv"></canvas>
<div id="hud" class="hide"><div id="sc"></div><div id="lb"></div><button id="bst">⚡</button></div>
<div id="jb" class="hide"><div id="jk"></div></div>
<input type="file" id="ph" accept="image/*" class="hide">

<div id="menu" class="scr on">
 <section class="pg on" id="p-lobby">
  <h1>SNAKE<span>.FAMILY</span></h1>
  <canvas id="pv" class="pv" width="340" height="340"></canvas>
  <input type="text" id="nm" maxlength="12" placeholder="Ton pseudo">
  <small id="who"></small>
  <button class="big" id="play">JOUER</button>
  <div class="stats"><div><small>Record</small><b id="s1">0</b></div><div><small>Éliminations</small><b id="s2">0</b></div><div><small>Niveau</small><b id="s3">0</b></div></div>
  <div class="bar"><i id="xb"></i></div><small id="xt"></small>
 </section>
 <section class="pg" id="p-locker">
  <h2>Casier</h2><canvas id="pv2" class="pv" width="340" height="340"></canvas>
  <small>Personnages</small><div class="grid" id="gc"></div>
  <button class="ghost" id="phb"></button>
  <small>Skins</small><div class="grid" id="gs"></div>
 </section>
 <section class="pg" id="p-pass">
  <h2>Passe de combat</h2><b id="pl"></b>
  <div class="bar"><i id="pb"></i></div><small id="pt"></small>
  <small>Joue pour gagner de l’XP : score + éliminations</small>
  <div class="rows" id="pr"></div>
 </section>
 <section class="pg" id="p-set">
  <h2>Paramètres</h2>
  <label>Sensibilité du joystick <span><b id="v1"></b></span><input type="range" id="r1" min="0.5" max="2" step="0.1"></label>
  <label>Nombre de bots <span><b id="v2"></b></span><input type="range" id="r2" min="5" max="25" step="1"></label>
  <label>Taille du joystick <span><b id="v3"></b></span><input type="range" id="r3" min="0.8" max="1.6" step="0.1"></label>
  <small>Le joystick apparaît là où tu poses le pouce. Bouton ⚡ pour accélérer.<br>Clavier : flèches / WASD + espace.</small>
  <button class="ghost" id="rst">Réinitialiser la progression</button>
 </section>
 <div id="nav"><button data-p="lobby" class="on">🏠 Lobby</button><button data-p="locker">🗄️ Casier</button><button data-p="pass">🏆 Passe</button><button data-p="set">⚙️ Réglages</button></div>
</div>

<div id="dead" class="scr"><h2 id="d1"></h2><div id="d2"></div><div id="d3"></div>
 <button class="big" id="again">REJOUER</button><button class="ghost" id="tolobby">Lobby</button></div>

<script>
const $=id=>document.getElementById(id);
const CH=[{id:'P',n:'Cyril',c:'#3b82f6'},{id:'M',n:'Séverine',c:'#ec4899'},{id:'G1',n:'Noa',c:'#f59e0b'},{id:'G2',n:'Matthieu',c:'#10b981'},{id:'F1',n:'Emy',c:'#a855f7'},{id:'F2',n:'Zoé',c:'#ef4444'}];
const SK=[{id:'classic',n:'Classique',c:['#46f0a0','#2bc47d']},{id:'neon',n:'Néon',c:['#22e5ff','#ff3bd4']},{id:'feu',n:'Feu',c:['#ff4b2b','#ffb347']},{id:'ocean',n:'Océan',c:['#2b7bff','#38d6ff','#1a4fd0']},{id:'glace',n:'Glace',c:['#e8fbff','#8fd8ff']},{id:'toxic',n:'Toxique',c:['#b6ff2b','#3a3a3a']},{id:'arc',n:'Arc-en-ciel',c:null},{id:'or',n:'Or',c:['#ffd84a','#ffb000','#fff2a8']}];
const PASS=[['s','neon'],['c','M'],['s','feu'],['c','G1'],['s','ocean'],['c','G2'],['s','glace'],['c','F1'],['s','toxic'],['s','arc'],['c','F2'],['s','or']];
const lvOf=(t,id)=>PASS.findIndex(p=>p[0]===t&&p[1]===id)+1;
let S={xp:0,ch:'P',sk:'classic',sens:1,bots:15,joy:1,name:'',best:0,kills:0};
try{Object.assign(S,JSON.parse(localStorage.getItem('snakefam1')||'{}'))}catch(e){}
const save=()=>{try{localStorage.setItem('snakefam1',JSON.stringify(S))}catch(e){}};
const lvl=()=>Math.min(12,Math.floor(S.xp/100));
const okC=c=>lvOf('c',c.id)<=lvl(),okS=k=>lvOf('s',k.id)<=lvl();
const skin=id=>SK.find(k=>k.id===id)||SK[0];

/* Visages : avatars par défaut (initiale) ou photos importées, gardées sur cet appareil */
function defFace(c){const k=document.createElement('canvas');k.width=k.height=96;const g=k.getContext('2d');
 g.fillStyle=c.c;g.fillRect(0,0,96,96);g.fillStyle='#fff';g.font='bold 56px system-ui';g.textAlign='center';g.textBaseline='middle';g.fillText(c.n[0],48,52);return k.toDataURL()}
let PH={};try{PH=JSON.parse(localStorage.getItem('snakefamph')||'{}')}catch(e){}
const FACES={},IMG={};
CH.forEach(c=>{FACES[c.id]=PH[c.id]||defFace(c);const i=new Image();i.onload=()=>refresh();i.src=FACES[c.id];IMG[c.id]=i});
$('phb').onclick=()=>$('ph').click();
$('ph').onchange=e=>{const f=e.target.files[0];e.target.value='';if(!f)return;const id=S.ch,u=URL.createObjectURL(f),im=new Image();
 im.onload=()=>{const k=document.createElement('canvas');k.width=k.height=96;const g=k.getContext('2d'),m=Math.min(im.width,im.height);
  g.drawImage(im,(im.width-m)/2,(im.height-m)/2,m,m,0,0,96,96);URL.revokeObjectURL(u);
  const d=k.toDataURL('image/jpeg',.85);FACES[id]=d;PH[id]=d;IMG[id].src=d;
  try{localStorage.setItem('snakefamph',JSON.stringify(PH))}catch(_){}};im.src=u};
const swatch=k=>k.c?`linear-gradient(90deg,${k.c.join(',')})`:'linear-gradient(90deg,#f33,#fa3,#ee3,#3d6,#3cf,#46f,#d3f)';
const segCol=(k,i)=>k.c?k.c[(i>>1)%k.c.length]:`hsl(${(i*13)%360},90%,60%)`;

/* ---------- Menu ---------- */
function faceAt(g,k,x,y,r){const im=IMG[k];g.save();g.beginPath();g.arc(x,y,r,0,6.283);g.clip();
 if(im&&im.complete&&im.naturalWidth)g.drawImage(im,x-r,y-r,2*r,2*r);else{g.fillStyle='#ddd';g.fillRect(x-r,y-r,2*r,2*r)}
 g.restore();g.lineWidth=Math.max(2,r*.12);g.strokeStyle='#fff';g.beginPath();g.arc(x,y,r,0,6.283);g.stroke()}
function prev(c){const g=c.getContext('2d'),w=c.width,sk=skin(S.sk);g.clearRect(0,0,w,w);
 for(let i=9;i>=0;i--){const x=w*(.7-.065*i),y=w*(.45+.035*i+.07*Math.sin(i*.9)),r=w*.12*(1-i*.025);
  if(i){g.fillStyle=segCol(sk,i);g.beginPath();g.arc(x,y,r,0,6.283);g.fill()}else faceAt(g,S.ch,x,y,w*.16)}}
function refresh(){const p=document.querySelector('.pg.on').id;({'p-lobby':rLobby,'p-locker':rLocker,'p-pass':rPass,'p-set':rSet})[p]()}
function go(p){document.querySelectorAll('.pg').forEach(e=>e.classList.toggle('on',e.id==='p-'+p));
 document.querySelectorAll('#nav button').forEach(b=>b.classList.toggle('on',b.dataset.p===p));refresh()}
document.querySelectorAll('#nav button').forEach(b=>b.onclick=()=>go(b.dataset.p));
function rLobby(){prev($('pv'));$('nm').value=$('nm').value||S.name||'';$('who').textContent=CH.find(c=>c.id===S.ch).n+' · '+skin(S.sk).n;
 $('s1').textContent=S.best;$('s2').textContent=S.kills;$('s3').textContent=lvl();
 const L=lvl();$('xb').style.width=(L>=12?100:S.xp%100)+'%';$('xt').textContent=L>=12?'Passe terminé 🎉':`${S.xp%100}/100 XP vers le niveau ${L+1}`}
function rLocker(){prev($('pv2'));$('phb').textContent='📷 Photo pour '+CH.find(c=>c.id===S.ch).n;
 $('gc').innerHTML=CH.map(c=>{const o=okC(c);return `<button class="cell ${S.ch===c.id?'sel':''} ${o?'':'lk'}" data-c="${c.id}"><img src="${FACES[c.id]}"><b>${c.n}</b>${o?'':`<em>🔒 Niv ${lvOf('c',c.id)}</em>`}</button>`}).join('');
 $('gs').innerHTML=SK.map(k=>{const o=okS(k);return `<button class="cell ${S.sk===k.id?'sel':''} ${o?'':'lk'}" data-s="${k.id}"><i class="sw" style="background:${swatch(k)}"></i><b>${k.n}</b>${o?'':`<em>🔒 Niv ${lvOf('s',k.id)}</em>`}</button>`}).join('')}
$('p-locker').onclick=e=>{const b=e.target.closest('[data-c],[data-s]');if(!b)return;
 if(b.dataset.c){const c=CH.find(x=>x.id===b.dataset.c);if(okC(c))S.ch=c.id}else{const k=skin(b.dataset.s);if(okS(k))S.sk=k.id}save();rLocker()};
function rPass(){const L=lvl();$('pl').textContent=`Niveau ${L} / 12`;$('pb').style.width=(L>=12?100:S.xp%100)+'%';
 $('pt').textContent=L>=12?'Tout est débloqué !':`${S.xp%100} / 100 XP`;
 $('pr').innerHTML=PASS.map((p,i)=>{const lv=i+1,c=p[0]==='c',nm=c?CH.find(x=>x.id===p[1]).n:skin(p[1]).n;
  const ic=c?`<img src="${FACES[p[1]]}">`:`<i class="sw" style="background:${swatch(skin(p[1]))}"></i>`;
  return `<div class="row ${lv<=L?'got':''}"><span class="lv">${lv}</span>${ic}<b>${c?'Perso : ':'Skin : '}${nm}</b><em>${lv<=L?'✔ Obtenu':'🔒'}</em></div>`}).join('')}
function rSet(){[['r1','v1','sens'],['r2','v2','bots'],['r3','v3','joy']].forEach(([r,v,k])=>{$(r).value=S[k];$(v).textContent=k==='bots'?S[k]:'×'+S[k]})}
[['r1','v1','sens'],['r2','v2','bots'],['r3','v3','joy']].forEach(([r,v,k])=>$(r).oninput=()=>{S[k]=+$(r).value;$(v).textContent=k==='bots'?S[k]:'×'+S[k];save()});
let rc=0;$('rst').onclick=()=>{if(!rc){rc=1;$('rst').textContent='Appuie encore pour confirmer';setTimeout(()=>{rc=0;$('rst').textContent='Réinitialiser la progression'},3000);return}
 S={xp:0,ch:'P',sk:'classic',sens:1,bots:15,joy:1,name:'',best:0,kills:0};save();rc=0;$('rst').textContent='Réinitialiser la progression';rSet()};

/* ---------- Jeu ---------- */
const cv=$('cv'),ctx=cv.getContext('2d'),R=3200;let dpr=1,W=0,H=0;
function rs(){dpr=Math.min(2,devicePixelRatio||1);W=innerWidth;H=innerHeight;cv.width=W*dpr;cv.height=H*dpr}
addEventListener('resize',rs);rs();
let snakes=[],orbs=[],me=null,playing=false,live=false,time=0,nextSp=0,lbT=0,cam={x:0,y:0,z:.6},joy=null,bstOn=false;
const keys=new Set(),NAMES=['Zorg','Pixel','Vipère','Nono','Kiki','Boa','Mamba','Cobra','Ziggy','Sssam','Lulu','Kaa','Naja','Toto','Python','Rex','Bibi','Yoyo','Lola','Max','Nagini','Slinky','Rampe','Zigzag','Anaconda'];
const rad=m=>7+Math.min(13,Math.sqrt(m)*.9);
const angDiff=(a,b)=>{let d=a-b;while(d>Math.PI)d-=6.2832;while(d<-Math.PI)d+=6.2832;return d};
function orb(){const a=Math.random()*6.283,d=Math.sqrt(Math.random())*(R-80),big=Math.random()<.1;return{x:Math.cos(a)*d,y:Math.sin(a)*d,v:big?3:1,r:big?8:4.5,c:`hsl(${Math.random()*360},90%,62%)`}}
function mk(o){const a=Math.random()*6.283,s={x:o.x,y:o.y,a,ta:a,pw:1,m:o.m||10,seg:[],sk:o.sk,face:o.face,name:o.name,bot:!!o.bot,boost:false,kills:0,dead:false,t:0,wa:a,ag:Math.random()};
 s.r=rad(s.m);for(let i=0;i<12;i++)s.seg.push({x:s.x-Math.cos(a)*i*5,y:s.y-Math.sin(a)*i*5});return s}
function spawnBot(init){let x,y,k=0;do{const a=Math.random()*6.283,d=Math.sqrt(Math.random())*(R-200);x=Math.cos(a)*d;y=Math.sin(a)*d;k++}while(!init&&me&&Math.hypot(x-me.x,y-me.y)<700&&k<12);
 snakes.push(mk({x,y,sk:SK[Math.random()*SK.length|0],name:NAMES[Math.random()*NAMES.length|0],bot:true,m:10+Math.random()*(init?60:15)}))}
function start(){S.name=($('nm').value||'Joueur').trim().slice(0,12);save();
 snakes=[];orbs=[];time=0;nextSp=0;const a=Math.random()*6.283,d=Math.random()*600;
 me=mk({x:Math.cos(a)*d,y:Math.sin(a)*d,sk:skin(S.sk),face:S.ch,name:S.name});snakes.push(me);
 for(let i=0;i<S.bots;i++)spawnBot(true);for(let i=0;i<1400;i++)orbs.push(orb());
 cam.x=me.x;cam.y=me.y;playing=live=true;joy=null;
 $('menu').classList.remove('on');$('dead').classList.remove('on');$('hud').classList.remove('hide')}
function kill(s,by){if(s.dead)return;s.dead=true;if(by)by.kills++;
 const v=Math.max(1.2,s.m/s.seg.length*2);
 for(let i=0;i<s.seg.length;i+=2){if(orbs.length>3000)break;const q=s.seg[i];orbs.push({x:q.x+(Math.random()-.5)*10,y:q.y+(Math.random()-.5)*10,v,r:5+Math.min(5,v),c:segCol(s.sk,i)})}
 if(s===me)over(by)}
function over(by){playing=false;joy=null;$('jb').classList.add('hide');$('hud').classList.add('hide');try{navigator.vibrate&&navigator.vibrate(200)}catch(e){}
 const sc=Math.floor(me.m),xp=Math.round(sc*.6+me.kills*12),b=lvl();S.xp=Math.min(1200,S.xp+xp);S.best=Math.max(S.best,sc);S.kills+=me.kills;save();
 const un=[];for(let l=b+1;l<=lvl();l++){const p=PASS[l-1];un.push(p[0]==='c'?'👤 '+CH.find(c=>c.id===p[1]).n:'🎨 '+skin(p[1]).n)}
 setTimeout(()=>{$('d1').textContent=by?`Éliminé par ${by.name}`:'Tu as touché la bordure !';
  $('d2').innerHTML=`Score <b>${sc}</b> · Éliminations <b>${me.kills}</b><br>+${xp} XP du passe`;
  $('d3').innerHTML=un.length?`<b style="color:var(--ac)">Débloqué !</b><br>${un.join('<br>')}`:'';$('dead').classList.add('on')},500)}
function ai(s,dt){s.t-=dt;if(s.t>0)return;s.t=.12+Math.random()*.1;
 let ta,bo=false;s.wa+=(Math.random()-.5)*.9;ta=s.wa;
 let best=null,bd=360*360;for(const o of orbs){const dx=o.x-s.x,dy=o.y-s.y,d=dx*dx+dy*dy;if(d<bd){bd=d;best=o}}
 if(best)ta=Math.atan2(best.y-s.y,best.x-s.x);
 let tg=null;if(s.ag>.35)for(const o of snakes){if(o===s||o.dead||o.m>s.m*.85)continue;const d=Math.hypot(o.x-s.x,o.y-s.y);if(d<450&&(!tg||d<tg.d))tg={o,d}}
 if(tg){ta=Math.atan2(tg.o.y+Math.sin(tg.o.a)*tg.o.r*7-s.y,tg.o.x+Math.cos(tg.o.a)*tg.o.r*7-s.x);bo=tg.d<300}
 const lx=s.x+Math.cos(s.a)*(s.r*4+50),ly=s.y+Math.sin(s.a)*(s.r*4+50);let dg=false;
 for(const o of snakes){if(o===s||o.dead||dg)continue;if(Math.hypot(o.x-s.x,o.y-s.y)>o.seg.length*o.r*.65+260)continue;
  for(let i=0;i<o.seg.length;i+=2){const q=o.seg[i];if(Math.hypot(q.x-lx,q.y-ly)<o.r+s.r+34){const cr=Math.cos(s.a)*(q.y-s.y)-Math.sin(s.a)*(q.x-s.x);ta=s.a-(cr>0?1:-1)*1.5;dg=true;bo=false;break}}}
 if(Math.hypot(s.x,s.y)>R-260){ta=Math.atan2(-s.y,-s.x);bo=false}
 s.ta=ta;s.boost=bo;s.pw=1}
function step(s,dt){s.r=rad(s.m);let sp=150;const bo=s.boost&&s.m>12;
 if(bo){sp=265;s.m-=dt*5;if(Math.random()<dt*6){const q=s.seg[s.seg.length-1];orbs.push({x:q.x,y:q.y,v:.8,r:3.5,c:segCol(s.sk,0)})}}
 const tr=4.6*(s.bot?1:S.sens)/(1+(s.r-8)*.045)*(bo?.8:1)*s.pw,d=angDiff(s.ta,s.a),mx=tr*dt;
 s.a+=Math.max(-mx,Math.min(mx,d*10*dt));s.x+=Math.cos(s.a)*sp*dt;s.y+=Math.sin(s.a)*sp*dt;
 const n=Math.min(260,Math.floor(10+s.m*.55)),gap=s.r*.62;
 while(s.seg.length<n){const l=s.seg[s.seg.length-1];s.seg.push({x:l.x,y:l.y})}while(s.seg.length>n)s.seg.pop();
 s.seg[0].x=s.x;s.seg[0].y=s.y;let px=s.x,py=s.y;
 for(let i=1;i<n;i++){const q=s.seg[i],dx=px-q.x,dy=py-q.y,dd=Math.hypot(dx,dy)||1;if(dd>gap){q.x=px-dx/dd*gap;q.y=py-dy/dd*gap}px=q.x;py=q.y}
 for(let i=orbs.length-1;i>=0;i--){const o=orbs[i],dx=o.x-s.x,dy=o.y-s.y,rr=s.r+o.r+12;if(dx*dx+dy*dy<rr*rr){s.m+=o.v;orbs[i]=orbs[orbs.length-1];orbs.pop()}}}
function upd(dt){time+=dt;
 let ix=0,iy=0,im=0;if(joy){ix=joy.x;iy=joy.y;im=joy.m}
 if(keys.size){ix=(keys.has('d')||keys.has('arrowright')?1:0)-(keys.has('a')||keys.has('arrowleft')?1:0);iy=(keys.has('s')||keys.has('arrowdown')?1:0)-(keys.has('w')||keys.has('arrowup')?1:0);im=ix||iy?1:0}
 if(im>.12){me.ta=Math.atan2(iy,ix);me.pw=.45+.55*Math.min(1,(im-.12)/.6)}else me.pw=1;
 me.boost=bstOn||keys.has(' ');
 for(const s of snakes){if(s.dead)continue;if(s.bot)ai(s,dt);step(s,dt)}
 const dies=[];
 for(const s of snakes){if(s.dead)continue;if(Math.hypot(s.x,s.y)>R-s.r){dies.push([s,null]);continue}
  out:for(const o of snakes){if(o===s||o.dead)continue;if(Math.hypot(o.x-s.x,o.y-s.y)>o.seg.length*o.r*.65+o.r*2+s.r)continue;
   const lim=(s.r+o.r)*.75,l2=lim*lim;for(let i=1;i<o.seg.length;i++){const q=o.seg[i],dx=q.x-s.x,dy=q.y-s.y;if(dx*dx+dy*dy<l2){dies.push([s,o]);break out}}}}
 for(const[s,o]of dies)kill(s,o);
 snakes=snakes.filter(s=>!s.dead);
 const ab=snakes.filter(s=>s.bot).length;if(ab<S.bots&&time>nextSp){spawnBot(false);nextSp=time+.8}
 for(let k=0;k<3&&orbs.length<1400;k++)orbs.push(orb());
 if(me.dead)return;
 cam.x+=(me.x-cam.x)*Math.min(1,dt*8);cam.y+=(me.y-cam.y)*Math.min(1,dt*8);
 cam.z+=(Math.min(W,H)/(560+me.r*16)-cam.z)*Math.min(1,dt*3);
 lbT-=dt;if(lbT<=0){lbT=.4;const a=[...snakes].sort((x,y)=>y.m-x.m),ri=a.indexOf(me);
  $('lb').innerHTML=a.slice(0,5).map(s=>`<div class="${s===me?'me':''}"><span>${s.name}</span><span>${s.m|0}</span></div>`).join('')+(ri>4?`<div class="me"><span>#${ri+1} ${me.name}</span><span>${me.m|0}</span></div>`:'');
  $('sc').textContent='Score '+(me.m|0)}}
function draw(){ctx.setTransform(1,0,0,1,0,0);ctx.fillStyle='#070b18';ctx.fillRect(0,0,cv.width,cv.height);
 const sc=cam.z*dpr;ctx.setTransform(sc,0,0,sc,cv.width/2-cam.x*sc,cv.height/2-cam.y*sc);
 const hw=cv.width/2/sc+60,hh=cv.height/2/sc+60;
 ctx.save();ctx.beginPath();ctx.arc(0,0,R,0,6.283);ctx.fillStyle='#10172e';ctx.fill();ctx.clip();
 ctx.fillStyle='#1d2748';for(let x=Math.floor((cam.x-hw)/80)*80;x<cam.x+hw;x+=80)for(let y=Math.floor((cam.y-hh)/80)*80;y<cam.y+hh;y+=80){ctx.beginPath();ctx.arc(x,y,3,0,6.283);ctx.fill()}
 ctx.restore();ctx.lineWidth=16;ctx.strokeStyle='#ff3b5c';ctx.beginPath();ctx.arc(0,0,R+8,0,6.283);ctx.stroke();
 for(const o of orbs){if(Math.abs(o.x-cam.x)>hw||Math.abs(o.y-cam.y)>hh)continue;ctx.fillStyle=o.c;ctx.globalAlpha=.3;ctx.beginPath();ctx.arc(o.x,o.y,o.r*1.9,0,6.283);ctx.fill();ctx.globalAlpha=1;ctx.beginPath();ctx.arc(o.x,o.y,o.r,0,6.283);ctx.fill()}
 const order=[...snakes].sort((a,b)=>(a===me)-(b===me));
 for(const s of order){const n=s.seg.length;
  for(let i=n-1;i>0;i--){const q=s.seg[i];if(Math.abs(q.x-cam.x)>hw||Math.abs(q.y-cam.y)>hh)continue;const t=i>n-8?.6+.4*(n-i)/8:1;
   ctx.fillStyle=segCol(s.sk,i);ctx.beginPath();ctx.arc(q.x,q.y,s.r*t,0,6.283);ctx.fill()}
  if(Math.abs(s.x-cam.x)>hw||Math.abs(s.y-cam.y)>hh)continue;
  if(s.face)faceAt(ctx,s.face,s.x,s.y,s.r*1.3);
  else{ctx.fillStyle=segCol(s.sk,0);ctx.beginPath();ctx.arc(s.x,s.y,s.r,0,6.283);ctx.fill();
   for(const sd of[-1,1]){const ex=s.x+Math.cos(s.a)*s.r*.35-Math.sin(s.a)*sd*s.r*.45,ey=s.y+Math.sin(s.a)*s.r*.35+Math.cos(s.a)*sd*s.r*.45;
    ctx.fillStyle='#fff';ctx.beginPath();ctx.arc(ex,ey,s.r*.33,0,6.283);ctx.fill();ctx.fillStyle='#111';ctx.beginPath();ctx.arc(ex+Math.cos(s.a)*s.r*.1,ey+Math.sin(s.a)*s.r*.1,s.r*.17,0,6.283);ctx.fill()}}
  ctx.fillStyle='#fff';ctx.font='bold 14px system-ui';ctx.textAlign='center';ctx.fillText(s.name,s.x,s.y-s.r*1.9)}}
let last=0;(function loop(t){requestAnimationFrame(loop);const dt=Math.min(.05,(t-last)/1000||0);last=t;if(live){if(playing)upd(dt);draw()}})(0);

/* ---------- Entrées ---------- */
function jShow(){const b=$('jb'),z=130*S.joy;b.style.width=b.style.height=z+'px';b.style.left=joy.ox+'px';b.style.top=joy.oy+'px';b.classList.remove('hide')}
cv.addEventListener('pointerdown',e=>{if(!playing||joy)return;joy={id:e.pointerId,ox:e.clientX,oy:e.clientY,x:0,y:0,m:0};jShow();$('jk').style.left=$('jk').style.top='50%';try{cv.setPointerCapture(e.pointerId)}catch(_){}});
cv.addEventListener('pointermove',e=>{if(!joy||e.pointerId!==joy.id)return;const rr=65*S.joy;let dx=e.clientX-joy.ox,dy=e.clientY-joy.oy;const m=Math.hypot(dx,dy);
 if(m>rr*1.6){joy.ox+=dx/m*(m-rr*1.6);joy.oy+=dy/m*(m-rr*1.6);dx=e.clientX-joy.ox;dy=e.clientY-joy.oy;jShow()}
 const mm=Math.hypot(dx,dy)||1,c=Math.min(mm,rr);joy.x=dx/mm;joy.y=dy/mm;joy.m=Math.min(1,mm/rr);
 $('jk').style.left=50+dx/mm*c/(rr*2)*100+'%';$('jk').style.top=50+dy/mm*c/(rr*2)*100+'%'});
const jEnd=e=>{if(joy&&e.pointerId===joy.id){joy=null;$('jb').classList.add('hide')}};
cv.addEventListener('pointerup',jEnd);cv.addEventListener('pointercancel',jEnd);
const bs=$('bst');bs.addEventListener('pointerdown',e=>{bstOn=true;e.preventDefault()});['pointerup','pointercancel','pointerleave'].forEach(n=>bs.addEventListener(n,()=>bstOn=false));
addEventListener('keydown',e=>{const k=e.key.toLowerCase();if('wasd arrowupdownleftright'.includes(k)||k===' '){keys.add(k);if(k===' ')e.preventDefault()}});
addEventListener('keyup',e=>keys.delete(e.key.toLowerCase()));
$('play').onclick=start;$('again').onclick=start;
$('tolobby').onclick=()=>{live=false;$('dead').classList.remove('on');$('menu').classList.add('on');go('lobby')};
rLobby();
</script></body></html>
