<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>La Ruta del Placer — Todo en uno</title>
<style>
  :root{--bg:#0f0f12;--panel:#18181d;--card:#1f1f26;--text:#f3f3f8;--muted:#b3b3c2;--accent:#ff6a7a;--accent2:#7ad7ff;--good:#5fd17b;--warn:#ffb86b;--danger:#ff5c5c}
  *{box-sizing:border-box} html,body{height:100%}
  body{margin:0;background:linear-gradient(180deg,#0b0b0e,#13131a 35%,#0b0b0e);color:var(--text);font-family:Inter,system-ui,Segoe UI,Roboto,Arial,sans-serif;display:flex;flex-direction:column;align-items:center}
  header{width:100%;max-width:980px;padding:16px 20px;display:flex;align-items:center;justify-content:space-between;gap:10px}
  .brand{display:flex;align-items:center;gap:10px;font-weight:700;letter-spacing:.3px}
  .pill{background:linear-gradient(135deg,var(--accent),#ff9aa7);color:#0b0b0e;font-weight:800;padding:4px 10px;border-radius:999px;font-size:12px}
  .wrap{width:100%;max-width:980px;padding:8px 20px 24px 20px}
  .panel{background:var(--panel);border:1px solid #2c2c36;border-radius:14px;padding:16px;margin-bottom:16px}
  .panel h2{margin:4px 0 12px 0;font-size:18px}
  .row{display:flex;flex-wrap:wrap;gap:12px;align-items:center}
  .row>*{flex:1} .row .tight{flex:0 0 auto}
  label{font-size:13px;color:var(--muted);display:inline-flex;align-items:center;gap:8px}
  input[type=checkbox]{width:18px;height:18px}
  select,input[type=number],input[type=text],button{background:var(--card);color:var(--text);border:1px solid #333444;border-radius:10px;padding:10px 12px;font-size:14px}
  button{cursor:pointer;transition:transform .05s ease,background .2s} button:hover{transform:translateY(-1px)}
  .btn-accent{background:linear-gradient(135deg,var(--accent),#ff9aa7);color:#100f12;border:none;font-weight:800}
  .btn-outline{background:transparent;border:1px solid #3a3a48}
  .grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
  .card-area{position:relative;height:420px;overflow:hidden}
  .card{position:absolute;inset:0;margin:auto;width:100%;max-width:720px;height:100%;background:radial-gradient(120% 140% at 70% 0%,#2a2a38 0%,#1f1f26 55%,#1a1a22 100%);color:var(--text);border:1px solid #2c2c36;border-radius:16px;padding:20px;box-shadow:0 10px 30px rgba(0,0,0,.35);display:flex;flex-direction:column;justify-content:space-between;transform-origin:bottom center;transition:transform .25s ease-out,opacity .25s ease-out;user-select:none}
  .card.hidden{opacity:0;transform:translateY(20px) scale(.98);pointer-events:none}
  .card h3{margin:0 0 6px 0;font-size:22px}
  .badge{display:inline-flex;align-items:center;gap:8px;font-size:12px;color:#0b0b0e;font-weight:800;padding:6px 10px;border-radius:999px}
  .type-pregunta{background:linear-gradient(135deg,#7ad7ff,#ade8ff)}
  .type-reto{background:linear-gradient(135deg,#ff6a7a,#ffa0aa)}
  .type-castigo{background:linear-gradient(135deg,#ffd166,#ffe5a3)}
  .badge.role{background:#2f2f3b;color:#eaeaf1;border:1px solid #46465e}
  .muted{color:var(--muted);font-size:13px}
  .tags{display:flex;flex-wrap:wrap;gap:8px;margin-top:8px}
  .tag{font-size:11px;padding:6px 8px;border-radius:999px;border:1px solid #3a3a48;color:#d8d8e6;background:#262632}
  .content{font-size:16px;line-height:1.55}
  .timer{display:flex;align-items:center;gap:10px;margin-top:8px}
  .timer .display{font-variant-numeric:tabular-nums;font-weight:800}
  .actions{display:flex;gap:10px;justify-content:space-between;margin-top:14px}
  .left-actions,.right-actions{display:flex;gap:10px}
  .progress{height:10px;background:#242431;border-radius:999px;border:1px solid #2c2c36;overflow:hidden}
  .progress>div{height:100%;background:linear-gradient(90deg,var(--accent2),#c179ff);width:0%}
  .foot{display:flex;align-items:center;justify-content:space-between;gap:10px}
  .note{font-size:12px;color:var(--muted)} .warn{color:var(--warn);font-weight:700} .good{color:var(--good);font-weight:700} .danger{color:var(--danger);font-weight:800}
  @media (max-width:820px){.grid{grid-template-columns:1fr} .card-area{height:520px}}
  /* Show the file input on iOS */
  #importFile{display:inline-block !important; max-width:180px} #importFile::-webkit-file-upload-button{visibility:visible}
</style>
</head>
<body>
<header>
  <div class="brand">
    <span class="pill">JUEGO</span> <span>La Ruta del Placer — Todo en uno</span>
  </div>
  <div style="display:flex; gap:8px; align-items:center; flex-wrap:wrap">
    <button id="btnReset" class="btn-outline">Reiniciar</button>
    <button id="btnExport" class="btn-outline">Exportar baraja</button>
    <label for="importFile" class="btn-accent" style="display:inline-flex;align-items:center;gap:8px;cursor:pointer">Importar baraja</label>
    <input id="importFile" type="file" accept="application/json" />
  </div>
</header>

<div class="wrap">

  <div class="panel">
    <h2>Reglas & Ajustes</h2>
    <div class="row" style="gap:16px">
      <label class="tight"><input type="checkbox" id="altRoles" checked/> Alternar roles (Él/Ella)</label>
      <label class="tight"><input type="checkbox" id="progressive" checked/> Progresión de intensidad</label>
      <label class="tight"><input type="checkbox" id="orgasmLock" checked/> Bloqueo de orgasmo (Él) hasta el final</label>
      <label class="tight"><input type="checkbox" id="mixQuestions" checked/> Intercalar Preguntas & Retos</label>
      <label class="tight"><input type="checkbox" id="enableCastigos" checked/> Incluir Castigos</label>
    </div>
    <div class="row" style="margin-top:10px; gap:16px">
      <label class="tight">Duración por defecto (seg):
        <input type="number" id="defaultSecs" value="90" min="10" max="600" style="width:90px" />
      </label>
      <label class="tight">Palabra de seguridad:
        <input type="text" id="safeWord" value="ROJO" style="width:120px" />
      </label>
      <div class="tight">
        <span class="note">Si dices la palabra de seguridad, todo se detiene y se habla. Cuidado y consentimiento primero.</span>
      </div>
    </div>
    <div class="row" style="margin-top:10px; gap:16px">
      <div>
        <div class="note" style="margin-bottom:6px">Disponibilidad de materiales (filtra cartas):</div>
        <div class="grid">
          <label><input type="checkbox" class="mat" value="aceite" checked/> Aceite de masaje</label>
          <label><input type="checkbox" class="mat" value="lubricante" checked/> Lubricante (incl. anal)</label>
          <label><input type="checkbox" class="mat" value="antifaz" checked/> Antifaz</label>
          <label><input type="checkbox" class="mat" value="esposas" checked/> Esposas/cuerda</label>
          <label><input type="checkbox" class="mat" value="mordaza" checked/> Mordaza</label>
          <label><input type="checkbox" class="mat" value="pinzas" checked/> Pinzas</label>
          <label><input type="checkbox" class="mat" value="plug" checked/> Plug/juego anal</label>
          <label><input type="checkbox" class="mat" value="latigo" checked/> Látigo/azotes</label>
          <label><input type="checkbox" class="mat" value="vibrador" checked/> Vibrador</label>
          <label><input type="checkbox" class="mat" value="otro" checked/> Libre</label>
        </div>
      </div>
    </div>
  </div>

  <div class="panel">
    <h2>Baraja</h2>
    <div class="progress" title="Intensidad"><div id="progressFill"></div></div>
    <div class="card-area" id="cardArea"></div>
    <div class="actions">
      <div class="left-actions">
        <button id="btnPrev" class="btn-outline">⟵ Atrás</button>
        <button id="btnSkip" class="btn-outline">Saltar</button>
      </div>
      <div class="right-actions">
        <button id="btnFail" class="btn-outline">No cumplido</button>
        <button id="btnDone" class="btn-accent">Cumplido</button>
      </div>
    </div>
  </div>

  <div class="panel">
    <h2>Añadir carta propia</h2>
    <div class="grid">
      <label>Tipo
        <select id="newType">
          <option value="pregunta">Pregunta</option>
          <option value="reto">Reto</option>
          <option value="castigo">Castigo</option>
        </select>
      </label>
      <label>Para
        <select id="newRole">
          <option value="ella">Ella</option>
          <option value="el">Él</option>
          <option value="ambos">Ambos</option>
        </select>
      </label>
      <label>Intensidad (1–5)
        <input type="number" id="newInt" value="2" min="1" max="5"/>
      </label>
      <label>Duración (seg, opcional)
        <input type="number" id="newSecs" placeholder="p.ej. 120" min="10" max="1200"/>
      </label>
    </div>
    <label style="display:block; margin-top:8px">Texto de la carta
      <input type="text" id="newText" placeholder="Escribe aquí el reto/pregunta (usa vuestro lenguaje)."/>
    </label>
    <label style="display:block; margin-top:8px">Material (opcional)
      <select id="newMat">
        <option value="">—</option>
        <option value="aceite">Aceite</option>
        <option value="lubricante">Lubricante</option>
        <option value="antifaz">Antifaz</option>
        <option value="esposas">Esposas</option>
        <option value="mordaza">Mordaza</option>
        <option value="pinzas">Pinzas</option>
        <option value="plug">Juego anal</option>
        <option value="latigo">Látigo</option>
        <option value="vibrador">Vibrador</option>
        <option value="otro">Otro</option>
      </select>
    </label>
    <div style="margin-top:10px; display:flex; gap:10px">
      <button id="btnAdd" class="btn-outline">Añadir</button>
      <span class="note">Consejo: mantén consensos claros; usa el semáforo: Verde / Amarillo / <span class="danger">Rojo</span>.</span>
    </div>
  </div>

  <footer class="panel" style="text-align:center; opacity:.85">
    Versión todo en uno. Listo para jugar sin importar barajas. ✨
  </footer>
</div>

<script>
// Embedded default deck (todo en uno)
const EMBEDDED = {"deck": [{"id": 1, "type": "pregunta", "role": "ella", "intensity": 1, "seconds": 60, "text": "¿Qué gesto o detalle te pone en modo juego hoy?", "mats": ["otro"]}, {"id": 2, "type": "reto", "role": "el", "intensity": 1, "seconds": 90, "text": "Masaje de cuello y hombros con aceite; ritmo lento y respiración sincronizada.", "mats": ["aceite"]}, {"id": 3, "type": "pregunta", "role": "el", "intensity": 1, "seconds": 60, "text": "Elige: besos largos o caricias suaves por todo el cuerpo.", "mats": ["otro"]}, {"id": 4, "type": "reto", "role": "ella", "intensity": 1, "seconds": 90, "text": "Antifaz + caricias desde nuca a cintura, sin tocar zonas íntimas.", "mats": ["antifaz"]}, {"id": 5, "type": "pregunta", "role": "ella", "intensity": 2, "seconds": 60, "text": "Nombra una fantasía que hoy te gustaría explorar de forma suave.", "mats": ["otro"]}, {"id": 6, "type": "reto", "role": "el", "intensity": 2, "seconds": 120, "text": "Beso profundo + manos por encima de la ropa, jugando con el ritmo.", "mats": ["otro"]}, {"id": 7, "type": "pregunta", "role": "el", "intensity": 2, "seconds": 60, "text": "¿Te excita añadir ojos vendados o atadura suave? Elige uno.", "mats": ["antifaz", "esposas"]}, {"id": 8, "type": "reto", "role": "ella", "intensity": 2, "seconds": 120, "text": "Antifaz puesto; quien juega decide 2 zonas sorpresa para besar/careciar.", "mats": ["antifaz"]}, {"id": 9, "type": "pregunta", "role": "ella", "intensity": 2, "seconds": 60, "text": "¿Qué frase susurrada te enciende más ahora mismo?", "mats": ["otro"]}, {"id": 10, "type": "reto", "role": "el", "intensity": 2, "seconds": 120, "text": "Reto de control: quien recibe debe pedir permiso antes de avanzar.", "mats": ["otro"]}, {"id": 11, "type": "pregunta", "role": "ella", "intensity": 3, "seconds": 60, "text": "Del 1 al 10, ¿qué nivel de azotes consensuados te apetece?", "mats": ["latigo"]}, {"id": 12, "type": "reto", "role": "el", "intensity": 3, "seconds": 120, "text": "Esposas de muñeca; caricias lentas + pausas. Pregunta “¿más?” entre pasos.", "mats": ["esposas"]}, {"id": 13, "type": "pregunta", "role": "el", "intensity": 3, "seconds": 60, "text": "¿Prefieres órdenes juguetonas o silencios largos con miradas?", "mats": ["otro"]}, {"id": 14, "type": "reto", "role": "ella", "intensity": 3, "seconds": 120, "text": "3–6 toques/azotes acordados; entre cada uno, aceite y manos cálidas.", "mats": ["latigo", "aceite"]}, {"id": 15, "type": "castigo", "role": "ambos", "intensity": 3, "seconds": 45, "text": "Quien falle mantiene manos detrás durante un turno (sin tocar).", "mats": ["otro"]}, {"id": 16, "type": "reto", "role": "ambos", "intensity": 3, "seconds": 90, "text": "Desafío de resistencia: mantener postura elegida mientras recibe caricias.", "mats": ["otro"]}, {"id": 17, "type": "pregunta", "role": "ella", "intensity": 4, "seconds": 60, "text": "Elige: vibrador externo, juego de temperatura o mordaza breve.", "mats": ["vibrador", "mordaza"]}, {"id": 18, "type": "reto", "role": "el", "intensity": 4, "seconds": 120, "text": "Antifaz + vibrador en zonas no obvias; pausar/seguir a señal acordada.", "mats": ["antifaz", "vibrador"]}, {"id": 19, "type": "pregunta", "role": "el", "intensity": 4, "seconds": 60, "text": "¿Quieres control de voz (susurros, silencio o palabras clave)?", "mats": ["mordaza", "otro"]}, {"id": 20, "type": "reto", "role": "ella", "intensity": 4, "seconds": 120, "text": "Mordaza breve (1–2 min) + caricias/masaje; comunicación por gestos.", "mats": ["mordaza", "aceite"]}, {"id": 21, "type": "pregunta", "role": "ella", "intensity": 4, "seconds": 60, "text": "¿Te apetece juego de pinzas suaves o pellizcos controlados?", "mats": ["pinzas"]}, {"id": 22, "type": "reto", "role": "el", "intensity": 4, "seconds": 90, "text": "Pinzas/pellizcos breves + masaje con aceite alrededor (sin excederse).", "mats": ["pinzas", "aceite"]}, {"id": 23, "type": "pregunta", "role": "ella", "intensity": 5, "seconds": 60, "text": "¿Incluimos juego anal cómodo (lubricante/plug) de forma progresiva?", "mats": ["lubricante", "plug"]}, {"id": 24, "type": "reto", "role": "el", "intensity": 5, "seconds": 150, "text": "Lubricante: masaje muy cercano + exploración externa; parar/seguir a señal.", "mats": ["lubricante"]}, {"id": 25, "type": "pregunta", "role": "el", "intensity": 5, "seconds": 60, "text": "¿Quieres control del clímax con pausas justo antes de llegar?", "mats": ["otro"]}, {"id": 26, "type": "reto", "role": "ella", "intensity": 5, "seconds": 180, "text": "Atadura suave + vibrador; aproximaciones repetidas sin terminar.", "mats": ["esposas", "vibrador"]}, {"id": 27, "type": "reto", "role": "ambos", "intensity": 5, "seconds": 150, "text": "Cuerpos con aceite: fricción piel con piel, ritmo creciente.", "mats": ["aceite"]}, {"id": 28, "type": "pregunta", "role": "ella", "intensity": 5, "seconds": 60, "text": "Elige final: quién guía, ritmo y si quieres juego anal ligero (opcional).", "mats": ["lubricante", "plug", "otro"]}, {"id": 29, "type": "reto", "role": "ella", "intensity": 5, "seconds": 180, "text": "Final para Ella: eliges escena y ritmo; Él mantiene bloqueo si así lo queréis.", "mats": ["otro"]}, {"id": 30, "type": "reto", "role": "el", "intensity": 5, "seconds": 180, "text": "Final para Él: bloqueo liberado; termináis como hayáis decidido juntos.", "mats": ["otro"]}], "settings": {"altRoles": true, "progressive": true, "orgasmLock": true, "mixQuestions": true, "enableCastigos": true, "defaultSecs": 90, "safeWord": "ROJO", "mats": ["aceite", "lubricante", "antifaz", "esposas", "mordaza", "pinzas", "plug", "latigo", "vibrador", "otro"]}};

// Core state
let deck = [];
let index = 0;

// Helpers
const qs = s => document.querySelector(s);
const qsa = s => Array.from(document.querySelectorAll(s));

function getSettings(){
  return {
    altRoles: qs('#altRoles').checked,
    progressive: qs('#progressive').checked,
    orgasmLock: qs('#orgasmLock').checked,
    mixQuestions: qs('#mixQuestions').checked,
    enableCastigos: qs('#enableCastigos').checked,
    defaultSecs: parseInt(qs('#defaultSecs').value||'90',10),
    safeWord: (qs('#safeWord').value || 'ROJO').trim().toUpperCase(),
    mats: qsa('.mat').filter(c=>c.checked).map(c=>c.value)
  };
}

function buildDeck(source) {
  const base = (source && Array.isArray(source.deck)) ? source : EMBEDDED;
  let items = (base.deck || []).slice();

  const s = getSettings();
  // Filter by materials
  items = items.filter(it => (it.mats||[]).every(m => s.mats.includes(m)));

  // Interleave questions & retos if requested
  if(s.mixQuestions){
    const preguntas = items.filter(i=>i.type==='pregunta').sort((a,b)=>a.intensity-b.intensity);
    const retos = items.filter(i=>i.type==='reto').sort((a,b)=>a.intensity-b.intensity);
    const castigos = items.filter(i=>i.type==='castigo').sort((a,b)=>a.intensity-b.intensity);
    const mixed=[];
    const maxlen = Math.max(preguntas.length, retos.length);
    for(let k=0;k<maxlen;k++){ if(preguntas[k]) mixed.push(preguntas[k]); if(retos[k]) mixed.push(retos[k]); if(castigos[k] && k%2===0) mixed.push(castigos[k]); }
    items = mixed;
  } else {
    items.sort((a,b)=>a.intensity-b.intensity);
  }

  // Optional: remove castigos
  if(!s.enableCastigos) items = items.filter(i=>i.type!=='castigo');

  // Progressive or shuffle
  if(!s.progressive){ for(let i=items.length-1;i>0;i--){ const j=Math.floor(Math.random()*(i+1)); [items[i],items[j]]=[items[j],items[i]]; } }

  // Alternate roles if requested (keeps 'ambos')
  if(s.altRoles){
    let toggle='ella';
    items = items.map(it=>{ if(it.role==='ambos') return it; const o={...it}; o.role=toggle; toggle=toggle==='ella'?'el':'ella'; return o; });
  }

  // Enforce male orgasm lock
  if(s.orgasmLock){
    items = items.map((it, idx)=>({...it, maleLock: idx < items.length-1}));
  } else {
    items = items.map(it=>({...it, maleLock:false}));
  }

  deck = items;
  index = 0;
  render();
}

function render(){
  const area = qs('#cardArea');
  area.innerHTML = '';
  if(deck.length===0){
    area.innerHTML = '<div class="card" style="align-items:center; justify-content:center"><div class="muted">No hay cartas con los filtros actuales.</div></div>';
    updateProgress(); return;
  }
  deck.forEach((it,i)=>{
    const card = document.createElement('div');
    card.className = 'card'+(i===index?'':' hidden');
    card.setAttribute('data-idx', i);
    const typeCls = it.type==='pregunta'?'type-pregunta':(it.type==='reto'?'type-reto':'type-castigo');
    const top = document.createElement('div');
    top.innerHTML = `
      <div style="display:flex; align-items:center; justify-content:space-between; gap:8px">
        <div style="display:flex; gap:8px; align-items:center">
          <span class="badge ${typeCls}">${it.type.toUpperCase()}</span>
          <span class="badge role">${it.role==='ambos'?'Ambos':(it.role==='el'?'Él':'Ella')}</span>
          <span class="badge role" title="Intensidad">Int ${it.intensity}</span>
          ${it.maleLock?'<span class="badge role" title="Bloqueo de orgasmo activo">🔒 Él</span>':''}
        </div>
        <div class="muted">#${String(it.id).padStart(2,'0')}</div>
      </div>`;
    const mid = document.createElement('div');
    mid.innerHTML = `<h3>${it.type==='pregunta'?'Pregunta':'Acción'}</h3>
      <div class="content">${it.text}</div>
      <div class="tags">${(it.mats||[]).map(m=>`<span class="tag">${m}</span>`).join('')}</div>`;
    const bottom = document.createElement('div');
    const secs = it.seconds || getSettings().defaultSecs;
    bottom.innerHTML = `
      <div class="timer">
        <button class="btn-outline btnTimer">⏱ Iniciar ${secs}s</button>
        <span class="display">00:${String(Math.max(0,Math.min(599,secs))).padStart(2,'0')}</span>
      </div>
      <div class="foot">
        <div class="note">Palabra de seguridad: <b>${getSettings().safeWord}</b></div>
        <div class="note">${it.maleLock?'<span class="warn">Bloqueo de orgasmo (Él) activo</span>':'<span class="good">Bloqueo liberado</span>'}</div>
      </div>`;
    card.append(top, mid, bottom);
    area.appendChild(card);
  });
  attachCardHandlers();
  updateProgress();
}

let currentTimer=null;
function attachCardHandlers(){
  qsa('.card').forEach(card=>{
    const idx = parseInt(card.getAttribute('data-idx'),10);
    const btnTimer = card.querySelector('.btnTimer');
    const display = card.querySelector('.display');
    if(btnTimer){
      btnTimer.addEventListener('click',()=>{
        if(currentTimer) clearInterval(currentTimer);
        let seconds = deck[idx].seconds || getSettings().defaultSecs;
        update(seconds);
        btnTimer.disabled = true;
        currentTimer = setInterval(()=>{
          seconds--; update(seconds);
          if(seconds<=0){ clearInterval(currentTimer); btnTimer.disabled=false; flashDone(card); }
        },1000);
        function update(s){ const m=Math.floor(s/60), r=s%60; display.textContent = String(m).padStart(2,'0')+':'+String(r).padStart(2,'0'); }
      });
    }
  });

  // swipe
  const area = qs('#cardArea');
  let startX=null;
  area.addEventListener('touchstart', e=>{ startX = e.touches[0].clientX; });
  area.addEventListener('touchend', e=>{
    if(startX==null) return;
    const dx = e.changedTouches[0].clientX - startX;
    if(Math.abs(dx)>40){ if(dx<0) nextCard(); else prevCard(); }
    startX=null;
  });
}

function flashDone(card){ card.style.transform='scale(1.02)'; setTimeout(()=>card.style.transform='',180); }
function nextCard(){
  if(index<deck.length-1){ qs(`.card[data-idx="${index}"]`).classList.add('hidden'); index++; qs(`.card[data-idx="${index}"]`).classList.remove('hidden'); updateProgress(); }
}
function prevCard(){
  if(index>0){ qs(`.card[data-idx="${index}"]`).classList.add('hidden'); index--; qs(`.card[data-idx="${index}"]`).classList.remove('hidden'); updateProgress(); }
}
function updateProgress(){
  const fill = qs('#progressFill');
  const pct = deck.length ? Math.round(((index+1)/deck.length)*100) : 0;
  fill.style.width = pct + '%';
}

qs('#btnDone').addEventListener('click', nextCard);
qs('#btnSkip').addEventListener('click', nextCard);
qs('#btnPrev').addEventListener('click', prevCard);
qs('#btnFail').addEventListener('click', ()=> alert('Castigo sugerido: 30s sin tocar o 3 azotes consensuados. Revisad límites y seguid jugando.'));

['#altRoles','#progressive','#orgasmLock','#mixQuestions','#enableCastigos','#defaultSecs','#safeWord'].forEach(id=> qs(id).addEventListener('change', ()=>buildDeck()));

qsa('.mat').forEach(cb=> cb.addEventListener('change', ()=>buildDeck()));

// Export/Import
qs('#btnExport').addEventListener('click', ()=>{
  const data = { deck: deck, settings: getSettings() };
  const blob = new Blob([JSON.stringify(data,null,2)], {type:'application/json'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a'); a.href=url; a.download='baraja_exportada.json'; a.click(); URL.revokeObjectURL(url);
});

qs('#importFile').addEventListener('change', (e)=>{
  const file = e.target.files[0];
  if(!file) return;
  const reader = new FileReader();
  reader.onload = ev => {
    try{ const data = JSON.parse(ev.target.result); buildDeck(data); }
    catch{ alert('Archivo inválido'); }
  };
  reader.readAsText(file);
});

// Init with embedded deck
buildDeck(EMBEDDED);
</script>
</body>
</html>
