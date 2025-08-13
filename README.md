
<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Calculadora de Cláusulas</title>
  <style>
    :root{
      --bg:#0b1220; --card:#111a2b; --accent:#5bbcff; --text:#e8eef8; --muted:#94a3b8;
      --ok:#22c55e; --warn:#f59e0b; --err:#ef4444; --ring:rgba(91,188,255,.45);
    }
    *{box-sizing:border-box}
    body{margin:0; font-family:ui-sans-serif,system-ui,-apple-system,Segoe UI,Roboto,Ubuntu,Cantarell,"Helvetica Neue",Arial; background: radial-gradient(1200px 800px at 20% -10%, #0e223f 0%, transparent 60%), var(--bg); color:var(--text)}
    .wrap{min-height:100dvh; display:grid; place-items:center; padding:24px}
    .card{width:100%; max-width:1000px; background:linear-gradient(180deg, rgba(255,255,255,0.02), transparent), var(--card); border:1px solid rgba(255,255,255,0.06); border-radius:20px; box-shadow:0 10px 30px rgba(0,0,0,.35); padding:24px;}
    .title{font-size:clamp(22px, 2.4vw, 28px); font-weight:800; letter-spacing:.2px; display:flex; align-items:center; gap:10px;}
    .title .dot{width:10px; height:10px; background:var(--accent); border-radius:50%; box-shadow:0 0 18px var(--accent)}
    p{color:var(--muted); margin:.5rem 0 1rem}

    .row{display:flex; flex-wrap:wrap; gap:12px; align-items:end}
    .field{flex:1 1 280px}
    label{display:block; font-size:14px; color:var(--muted); margin:0 0 6px}
    input[type=text], input[type=number]{width:100%; padding:12px 14px; border-radius:12px; border:1px solid rgba(255,255,255,0.08); background:#0c1526; color:var(--text); outline:none; transition:.15s ease; font-size:15px}
    input::placeholder{color:#6b7a90}
    input:focus{border-color:var(--accent); box-shadow:0 0 0 6px var(--ring)}

    .btn{appearance:none; border:0; border-radius:12px; padding:12px 14px; font-weight:700; cursor:pointer; background:linear-gradient(180deg, #63c6ff, #3aa8f7); color:#001528; box-shadow:0 8px 24px rgba(74, 170, 255, .35); transition:transform .05s ease, filter .15s ease}
    .btn:active{transform:translateY(1px)}
    .muted-btn{background:#0f1a2d; color:var(--text); border:1px solid rgba(255,255,255,.1)}
    .danger{background:linear-gradient(180deg, #ff6b6b, #ef4444); color:white}

    .result{margin-top:18px; padding:16px; border-radius:14px; border:1px dashed rgba(255,255,255,0.15); background:rgba(12,21,38,.55)}
    .money{font-size:clamp(22px, 3vw, 30px); font-weight:900; letter-spacing:.3px}
    .rule{font-size:14px; color:var(--muted)}
    .bad{color:var(--err)}

    .grid{display:grid; grid-template-columns:repeat(auto-fit, minmax(220px,1fr)); gap:10px; margin-top:18px}
    .badge{padding:10px 12px; background:#0f1a2d; border:1px solid rgba(255,255,255,.08); border-radius:12px; font-size:13px; color:var(--muted)}

    .panel{margin-top:20px; padding:14px; border-radius:14px; background:#0c1526; border:1px solid rgba(255,255,255,.08)}
    .panel h2{margin:0 0 8px; font-size:16px}
    .slider-row{display:grid; grid-template-columns:1fr auto; gap:12px; align-items:center; margin:10px 0}
    .slider-row input[type=range]{width:100%}
    .chips{display:flex; flex-wrap:wrap; gap:8px; margin-top:8px}
    .chip{font-size:12px; padding:6px 10px; border-radius:999px; background:#0f1a2d; border:1px solid rgba(255,255,255,.1); color:var(--muted)}

    table{width:100%; border-collapse:separate; border-spacing:0 8px; margin-top:12px}
    th, td{padding:10px 12px; text-align:left; font-size:14px}
    thead th{color:var(--muted); font-weight:600}
    tbody tr{background:#0f1a2d; border:1px solid rgba(255,255,255,.08)}
    tbody tr td:first-child{border-top-left-radius:10px; border-bottom-left-radius:10px}
    tbody tr td:last-child{border-top-right-radius:10px; border-bottom-right-radius:10px}

    footer{margin-top:20px; font-size:12px; color:#7f8da3}
  </style>
</head>
<body>
  <div class="wrap">
    <section class="card">
      <h1 class="title"><span class="dot"></span> Calculadora de Cláusulas</h1>
      <p>Escribe el <strong>valor del jugador</strong>; el campo se formatea con puntos al vuelo. Puedes <strong>ajustar porcentajes</strong> con el deslizador, y ahora también <strong>editar/crear tramos</strong> (dividir un tramo, cambiar límites y porcentajes). Todo se guarda en tu navegador.</p>

      <div class="row">
        <div class="field">
          <label for="valor">Valor del jugador (EUR)</label>
          <input id="valor" type="text" inputmode="numeric" autocomplete="off" placeholder="p. ej., 25.555.555" />
        </div>
        <button id="calc" class="btn">Calcular</button>
        <button id="reset" class="btn muted-btn">Limpiar</button>
      </div>

      <div id="out" class="result" hidden>
        <div class="money" id="clausula"></div>
        <div class="rule" id="regla"></div>
      </div>

      <div id="badges" class="grid" aria-hidden="true"></div>

      <section class="panel" id="ajustes">
        <h2>Ajuste rápido del porcentaje del tramo actual</h2>
        <p class="rule">Mueve el deslizador (100%–200%) para previsualizar la cláusula del <em>valor actual</em>. Pulsa <strong>Guardar</strong> para aplicar al tramo en uso.</p>
        <div class="chips">
          <span class="chip">Tramo actual: <strong id="tramoActual">—</strong></span>
          <span class="chip">Porcentaje actual: <strong id="pctActual">—</strong></span>
          <span class="chip">Previsualización: <strong id="preview">—</strong></span>
        </div>
        <div class="slider-row">
          <input id="slider" type="range" min="100" max="200" step="1" value="110" />
          <div style="min-width:80px;text-align:right"><span id="sliderVal">110</span> %</div>
        </div>
        <div class="row" style="margin-top:8px">
          <button id="guardar" class="btn">Guardar para este tramo</button>
        </div>
      </section>

      <section class="panel" id="editor">
        <h2>Editor de tramos (límites y porcentajes)</h2>
        <p class="rule">Puedes <strong>reducir un tramo</strong> cambiando su máximo y luego <strong>crear otro tramo</strong> dividiéndolo por el punto que elijas. Los límites siempre quedan contiguos y sin solaparse.</p>
        <table>
          <thead>
            <tr>
              <th>#</th>
              <th>Mínimo (€)</th>
              <th>Máximo (€)</th>
              <th>Tipo</th>
              <th>Valor</th>
              <th>Acciones</th>
            </tr>
          </thead>
          <tbody id="tiersTable"></tbody>
        </table>
        <div class="row" style="margin-top:8px">
          <div class="field">
            <label for="splitValue">Dividir tramo por este valor (€)</label>
            <input id="splitValue" type="text" placeholder="p. ej., 12.000.000" />
          </div>
          <button id="splitBtn" class="btn">Dividir tramo seleccionado</button>
          <button id="defaultsBtn" class="btn muted-btn">Restaurar valores por defecto</button>
        </div>
      </section>

      <footer>Persistencia en <em>LocalStorage</em>. Cálculo sin decimales (truncado). El primer tramo puede ser "absoluto"; el resto usan %.</footer>
    </section>
  </div>

  <script>
    const $ = s => document.querySelector(s);
    const nf = new Intl.NumberFormat('es-ES', { maximumFractionDigits: 0 });
    const fmt = n => nf.format(n) + ' \u20AC';

    // ----- Tiers (tramos) dinámicos -----
    // type: 'abs' (importe fijo) o 'pct' (porcentaje)
    const DEFAULT_TIERS = [
      { min: 0, max: 1_000_000, type: 'abs', value: 1_000_000 },
      { min: 1_000_001, max: 3_000_000, type: 'pct', value: 130 },
      { min: 3_000_001, max: 5_000_000, type: 'pct', value: 120 },
      { min: 5_000_001, max: 15_000_000, type: 'pct', value: 115 },
      { min: 15_000_001, max: Infinity, type: 'pct', value: 110 },
    ];

    function loadTiers(){
      try{
        const raw = localStorage.getItem('clausulasTiersV1');
        if(!raw) return DEFAULT_TIERS.map(t=>({...t}));
        const arr = JSON.parse(raw);
        // Revivir Infinity
        return arr.map(t => ({...t, max: t.max === 'Infinity' ? Infinity : t.max }));
      }catch{ return DEFAULT_TIERS.map(t=>({...t})); }
    }
    function saveTiers(tiers){
      const serial = tiers.map(t => ({...t, max: t.max === Infinity ? 'Infinity' : t.max}));
      localStorage.setItem('clausulasTiersV1', JSON.stringify(serial));
    }

    let TIERS = loadTiers();

    // ----- Utilidades -----
    function limpiarEntrada(txt){
      const digits = (txt+"").replace(/\D+/g, "");
      if(!digits) return NaN;
      return Number(digits);
    }
    function formatInputEl(el){
      const val = el.value.replace(/\D+/g, '');
      el.value = val ? nf.format(Number(val)) : '';
    }

    function findTierIndex(valor){
      return TIERS.findIndex(t => valor >= t.min && valor <= t.max);
    }

    function calcClause(valor){
      const idx = findTierIndex(valor);
      if(idx === -1) return { clause: NaN, rule: 'Fuera de rango', idx: -1 };
      const t = TIERS[idx];
      if(t.type === 'abs'){
        return { clause: t.value, rule: `T${idx+1}: absoluto`, idx };
      }
      const pct = Math.max(100, t.value); // seguridad mínima 100%
      return { clause: Math.trunc(valor * pct / 100), rule: `T${idx+1}: ${pct}%`, idx };
    }

    function renderBadges(){
      const c = $('#badges');
      c.innerHTML = '';
      TIERS.forEach((t,i)=>{
        const maxTxt = t.max === Infinity ? '∞' : nf.format(t.max) + ' €';
        const typeTxt = t.type === 'abs' ? nf.format(t.value) + ' € (abs)' : t.value + ' %';
        const div = document.createElement('div');
        div.className = 'badge';
        div.textContent = `${nf.format(t.min)} € – ${maxTxt} → ${typeTxt}`;
        c.appendChild(div);
      });
    }

    function renderTable(){
      const tbody = $('#tiersTable');
      tbody.innerHTML = '';
      TIERS.forEach((t,i)=>{
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td><label><input type="radio" name="tierSel" value="${i}" ${i===0?'disabled':''}></label> T${i+1}</td>
          <td><input data-k="min" data-i="${i}" type="text" ${i===0?'disabled':''} value="${nf.format(t.min)}"/></td>
          <td><input data-k="max" data-i="${i}" type="text" ${t.max===Infinity?'disabled':''} value="${t.max===Infinity?'∞':nf.format(t.max)}"/></td>
          <td>
            <select data-k="type" data-i="${i}" ${i!==0? '' : 'disabled'}>
              <option value="abs" ${t.type==='abs'?'selected':''}>Absoluto</option>
              <option value="pct" ${t.type==='pct'?'selected':''}>Porcentaje</option>
            </select>
          </td>
          <td>
            <input data-k="value" data-i="${i}" type="number" min="${t.type==='pct'?100:0}" value="${t.value}" />
          </td>
          <td>
            ${i>0 ? '<button class="btn danger" data-action="remove" data-i="'+i+'">Eliminar</button>' : ''}
          </td>`;
        tbody.appendChild(tr);
      });

      // Wire inputs for formatting and updates
      tbody.querySelectorAll('input[type=text]').forEach(el=>{
        el.addEventListener('input', ()=>formatInputEl(el));
        el.addEventListener('blur', onCellCommit);
      });
      tbody.querySelectorAll('input[type=number], select').forEach(el=>{
        el.addEventListener('change', onCellCommit);
      });
      tbody.querySelectorAll('button[data-action="remove"]').forEach(btn=>{
        btn.addEventListener('click', ()=>removeTier(parseInt(btn.dataset.i,10)));
      });
    }

    function normalizeTiers(){
      // Ordenar por min, asegurar contiguidad, corregir solapamientos
      TIERS.sort((a,b)=>a.min-b.min);
      for(let i=0;i<TIERS.length;i++){
        const t = TIERS[i];
        if(i===0){ t.min = 0; }
        if(i>0){
          const prev = TIERS[i-1];
          t.min = Math.max(t.min, prev.max===Infinity? prev.min : prev.max+1);
        }
        if(t.max !== Infinity && t.max < t.min){ t.max = t.min; }
      }
      // Asegurar último infinito
      TIERS[TIERS.length-1].max = Infinity;
    }

    function onCellCommit(e){
      const el = e.target;
      const i = parseInt(el.dataset.i,10);
      const k = el.dataset.k;
      const t = TIERS[i];
      if(k==='type'){
        t.type = el.value;
        if(t.type==='pct' && t.value < 100) t.value = 100;
      } else if(k==='value'){
        const num = Number(el.value);
        if(!Number.isFinite(num)) return;
        if(t.type==='pct') t.value = Math.max(100, Math.trunc(num));
        else t.value = Math.max(0, Math.trunc(num));
      } else if(k==='min' || k==='max'){
        if(el.value.trim()==='∞'){ t.max = Infinity; }
        else {
          const num = limpiarEntrada(el.value);
          if(!Number.isFinite(num)) return;
          t[k] = Math.trunc(num);
        }
      }
      normalizeTiers();
      saveTiers(TIERS);
      renderBadges();
      renderTable();
      // Recalcular si hay valor
      const valor = limpiarEntrada($('#valor').value);
      if(Number.isFinite(valor)){
        const { clause, rule } = calcClause(valor);
        mostrarResultado(clause, rule + ' (actualizado)');
        syncSliderToTier(valor);
        previewWithSlider(valor);
      }
    }

    function removeTier(i){
      if(i<=0 || i>=TIERS.length-1) return; // no borrar primero ni último
      if(!confirm('¿Eliminar este tramo? Los vecinos se ajustarán para cubrir el hueco.')) return;
      TIERS.splice(i,1);
      normalizeTiers();
      saveTiers(TIERS);
      renderBadges();
      renderTable();
    }

    function splitTierAtValue(splitVal){
      // Busca el tramo que contiene splitVal y lo divide en dos
      const idx = findTierIndex(splitVal);
      if(idx<=0){ alert('Selecciona un valor dentro de un tramo porcentual (no el absoluto).'); return; }
      const t = TIERS[idx];
      if(t.max === Infinity){
        // dividir creando un penúltimo y último
        const left = { ...t, max: splitVal };
        const right = { ...t, min: splitVal+1, max: Infinity };
        TIERS.splice(idx, 1, left, right);
      } else {
        const left = { ...t, max: splitVal };
        const right = { ...t, min: splitVal+1, max: t.max };
        TIERS.splice(idx, 1, left, right);
      }
      normalizeTiers();
      saveTiers(TIERS);
      renderBadges();
      renderTable();
    }

    function renderSelection(){
      // Marca en la tabla el tramo actual según el valor introducido
      const valor = limpiarEntrada($('#valor').value);
      const idx = Number.isFinite(valor) ? findTierIndex(valor) : -1;
      document.querySelectorAll('input[name="tierSel"]').forEach((r,i)=>{
        r.checked = (i===idx);
      });
      return idx;
    }

    // ----- UI principal -----
    function mostrarResultado(clause, rule){
      $('#clausula').textContent = fmt(clause);
      $('#regla').textContent = rule;
      $('#out').hidden = false;
    }

    function syncSliderToTier(valor){
      const idx = findTierIndex(valor);
      if(idx<0) return;
      const t = TIERS[idx];
      const pct = t.type==='pct' ? t.value : 100;
      $('#slider').value = Math.max(100, pct);
      $('#sliderVal').textContent = Math.max(100, pct);
      $('#pctActual').textContent = (t.type==='pct'? t.value+' %' : '—');
      $('#tramoActual').textContent = `T${idx+1}`;
    }

    function previewWithSlider(valor){
      const idx = findTierIndex(valor);
      if(idx<0) { $('#preview').textContent = '—'; return; }
      const t = TIERS[idx];
      let c = t.type==='abs' ? t.value : Math.trunc(valor * Math.max(100, Number($('#slider').value)) / 100);
      $('#preview').textContent = fmt(c);
    }

    function calcular(){
      const entrada = $('#valor').value;
      const valor = limpiarEntrada(entrada);
      if(!Number.isFinite(valor)){
        $('#out').hidden = false;
        $('#clausula').textContent = 'Entrada no válida';
        $('#regla').textContent = '';
        $('#clausula').classList.add('bad');
        return;
      }
      $('#clausula').classList.remove('bad');
      const { clause, rule } = calcClause(valor);
      mostrarResultado(clause, rule);
      syncSliderToTier(valor);
      previewWithSlider(valor);
      renderSelection();
    }

    // Eventos
    $('#calc').addEventListener('click', calcular);
    $('#reset').addEventListener('click', () => {
      $('#valor').value = '';
      $('#out').hidden = true;
      $('#clausula').textContent = '';
      $('#regla').textContent = '';
      $('#preview').textContent = '—';
      $('#pctActual').textContent = '—';
      $('#tramoActual').textContent = '—';
      $('#valor').focus();
      renderSelection();
    });
    $('#valor').addEventListener('keydown', e => { if(e.key === 'Enter') calcular(); });
    $('#valor').addEventListener('input', () => {
      formatInputEl($('#valor'));
      const valor = limpiarEntrada($('#valor').value);
      if(Number.isFinite(valor)){
        previewWithSlider(valor);
        syncSliderToTier(valor);
        renderSelection();
      } else {
        $('#preview').textContent = '—';
      }
    });

    $('#slider').addEventListener('input', () => {
      const valor = limpiarEntrada($('#valor').value);
      $('#sliderVal').textContent = $('#slider').value;
      if(Number.isFinite(valor)) previewWithSlider(valor);
    });

    $('#guardar').addEventListener('click', () => {
      const valor = limpiarEntrada($('#valor').value);
      const idx = Number.isFinite(valor) ? findTierIndex(valor) : -1;
      if(idx<=0){ alert('Selecciona un valor que esté en un tramo porcentual.'); return; }
      const pct = Math.max(100, Number($('#slider').value));
      TIERS[idx].type = 'pct';
      TIERS[idx].value = pct;
      saveTiers(TIERS);
      renderBadges();
      renderTable();
      if(Number.isFinite(valor)){
        const { clause, rule } = calcClause(valor);
        mostrarResultado(clause, rule + ' (guardado)');
      }
    });

    $('#defaultsBtn').addEventListener('click', () => {
      if(!confirm('¿Restaurar tramos por defecto?')) return;
      TIERS = DEFAULT_TIERS.map(t=>({...t}));
      saveTiers(TIERS);
      renderBadges();
      renderTable();
      const valor = limpiarEntrada($('#valor').value);
      if(Number.isFinite(valor)){
        const { clause, rule } = calcClause(valor);
        mostrarResultado(clause, rule + ' (restaurado)');
        syncSliderToTier(valor);
        previewWithSlider(valor);
      }
    });

    $('#splitBtn').addEventListener('click', () => {
      const val = limpiarEntrada($('#splitValue').value);
      if(!Number.isFinite(val)){ alert('Introduce un valor válido para dividir.'); return; }
      splitTierAtValue(val);
      $('#splitValue').value = '';
    });

    // Inicialización
    function init(){
      renderBadges();
      renderTable();
      $('#valor').focus();
    }
    window.addEventListener('DOMContentLoaded', init);
  </script>
</body>
</html>
