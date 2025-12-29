# SIH
INSTRUCTIONS:-
Just for the ease I have covered a little amt. of front end below i'll be pasting two codes the first code for the front end is a basic one so that you can undertsnad the blue print and after that there is the complex one in which there are multiple layouts so for that it is highly recommended to use VS code etc if you use an online compiler then (mat kar lala mara jaaega). The firt one can be implemeted on any online compiler for your understanding i would suggest (CodePen) and paste it into the html section. For second one use VS code and copy it and ask gpt whats the pre-requisites for this code to run then install it and implement at your end. Ideas are welcome and also i have made it as web frame for better understanding and better blueprint now i want you guys to ask gpt to code it into a mobile frame which is very simple.now work on charts etc 
Now I want someone who can also study the ground water substances etc jo mandeepp sir ne kaha tha and kindly send us what have you read after shortlisting what is to be read ask gpt very obvious,
Backend wale get your asses on work! ASAP
lets beat the shit outta this hackathon!!!!!!!!!!!!
Front END1(Blue Print):
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>HMPI — Heavy Metal Pollution Index</title>

  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&display=swap" rel="stylesheet">

  <!-- Leaflet CDN -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />

  <style>
    :root{
      --bg-deep:#02182b;
      --teal:#0aa3a3;
      --aqua:#2dd4bf;
      --accent:#ffd166; /* warm gold accent */
      --card:#062833;
      --muted:#9fb6b6;
      --glass: rgba(255,255,255,0.06);
      --success:#16a34a;
      --warning:#f59e0b;
      --danger:#ef4444;
      --white: #ffffff;
      --soft-shadow: 0 6px 18px rgba(2,24,43,0.6);
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family:'Inter',system-ui,-apple-system,Segoe UI,Roboto,"Helvetica Neue",Arial;
      color:var(--white);
      background: linear-gradient(180deg, rgba(2,24,43,0.92), rgba(2,24,43,0.92)), url('https://images.unsplash.com/photo-1507525428034-b723cf961d3e?q=80&w=2000&auto=format&fit=crop&ixlib=rb-4.0.3&s=3a2ff3b577d30c9cba2c6d8fbb8a3b81') center/cover fixed;
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      min-height:100vh;
      padding:40px;
    }

    .container{max-width:1100px;margin:0 auto}

    /* header / hero */
    header{
      display:flex;
      gap:24px;
      align-items:center;
      justify-content:space-between;
      margin-bottom:28px;
    }
    .brand{
      display:flex;gap:12px;align-items:center;
    }
    .logo{
      width:64px;height:64px;border-radius:12px;background:linear-gradient(135deg,var(--teal),var(--aqua));display:flex;align-items:center;justify-content:center;box-shadow: 0 6px 20px rgba(10,163,163,0.18);
    }
    .logo svg{filter:drop-shadow(0 6px 18px rgba(0,0,0,0.35));}
    h1{font-size:20px;margin:0;font-weight:700;letter-spacing:0.2px}
    p.lead{margin:0;color:var(--muted);font-size:13px}

    /* top cards */
    .cards{display:grid;grid-template-columns:repeat(4,1fr);gap:16px;margin-top:18px;margin-bottom:22px}
    .card{
      background: linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.02));
      border-radius:12px;padding:18px;box-shadow:var(--soft-shadow);
      border:1px solid rgba(255,255,255,0.04);cursor:pointer;transition:transform .18s ease, box-shadow .18s ease;
      display:flex;flex-direction:column;gap:8px;min-height:110px;
    }
    .card:hover{transform:translateY(-6px);box-shadow:0 18px 40px rgba(2,24,43,0.7)}
    .card h3{margin:0;font-size:15px}
    .card p{margin:0;color:var(--muted);font-size:12px}

    /* hero content */
    .hero{
      display:grid;grid-template-columns:1fr 420px;gap:22px;margin-top:18px;margin-bottom:20px;
    }
    .hero .left{
      background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      padding:22px;border-radius:14px;border:1px solid rgba(255,255,255,0.04);
      box-shadow:var(--soft-shadow);
    }
    .fact{
      display:flex;gap:14px;align-items:flex-start;margin-bottom:14px;
    }
    .fact .badge{
      width:56px;height:56px;border-radius:10px;background:linear-gradient(135deg,var(--accent),#ffb84d);display:flex;align-items:center;justify-content:center;color:#052a00;font-weight:800;
      font-size:14px;
    }
    .fact h2{margin:0;font-size:20px}
    .fact p{margin:6px 0 0 0;color:var(--muted);font-size:14px}

    blockquote{margin:0;padding:14px;border-left:4px solid rgba(255,255,255,0.04);color:var(--muted);font-style:italic;background:linear-gradient(90deg, rgba(255,255,255,0.01), rgba(255,255,255,0.00));border-radius:8px;margin-top:12px}

    /* form area */
    .panel{
      margin-top:14px;background:var(--glass);padding:14px;border-radius:10px;border:1px solid rgba(255,255,255,0.04);
    }
    label{display:block;font-size:13px;margin-bottom:6px;color:var(--muted)}
    input[type="text"], input[type="number"], input[type="file"], select{
      width:100%;padding:10px;border-radius:8px;border:1px solid rgba(255,255,255,0.06);background:transparent;color:var(--white);outline:none;font-size:14px;
    }
    .row{display:flex;gap:12px}
    .col{flex:1}

    button.cta{
      background:linear-gradient(90deg,var(--teal),var(--aqua));border:none;padding:12px 18px;border-radius:10px;color:#002323;font-weight:700;cursor:pointer;margin-top:8px;
      box-shadow:0 10px 28px rgba(10,163,163,0.14);
    }
    button.ghost{background:transparent;border:1px solid rgba(255,255,255,0.06);padding:10px;border-radius:8px;color:var(--muted);cursor:pointer}

    /* results */
    .results{margin-top:18px;display:grid;grid-template-columns:1fr 360px;gap:18px}
    .result-card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));padding:14px;border-radius:12px;border:1px solid rgba(255,255,255,0.04);box-shadow:var(--soft-shadow)}
    .status{
      display:flex;align-items:center;gap:12px;padding:10px;border-radius:10px;font-weight:700;
    }
    .status .dot{width:14px;height:14px;border-radius:4px;display:inline-block}
    table{width:100%;border-collapse:collapse;color:var(--muted);font-size:13px}
    th,td{padding:10px;text-align:left;border-bottom:1px dashed rgba(255,255,255,0.03)}
    th{color:var(--muted);font-weight:600}

    /* small helpers */
    .muted{color:var(--muted);font-size:13px}
    .note{font-size:12px;color:var(--muted);margin-top:8px}
    .tiny{font-size:12px;color:var(--muted)}

    footer{margin-top:28px;color:var(--muted);font-size:13px;text-align:center}

    /* responsive */
    @media(max-width:980px){
      .hero{grid-template-columns:1fr}
      .cards{grid-template-columns:repeat(2,1fr)}
      .results{grid-template-columns:1fr}
    }
    @media(max-width:520px){
      .cards{grid-template-columns:1fr}
    }

    /* little icon */
    .icon{
      width:38px;height:38px;border-radius:8px;background:rgba(255,255,255,0.03);display:flex;align-items:center;justify-content:center;color:var(--aqua);
    }

    .download{
      background:linear-gradient(90deg,#7b61ff,#ffd166);border:none;padding:10px 12px;border-radius:10px;color:#02182b;font-weight:700;cursor:pointer;
    }

    /* table for multi inputs */
    #samplesTable td {padding: 4px;}
    #samplesTable input {margin: 0;}

  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="brand">
        <div class="logo" aria-hidden>
          <!-- water droplet + test tube icon -->
          <svg width="34" height="34" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M12 2s-5 5.5-5 8.5A5 5 0 1 0 17 10C17 7.5 12 2 12 2z" fill="#02182b" opacity="0.95"/>
            <path d="M12 2s-5 5.5-5 8.5A5 5 0 1 0 17 10C17 7.5 12 2 12 2z" stroke="#fff" stroke-opacity=".12"/>
            <circle cx="12" cy="14.5" r="2.5" fill="#ffd166"/>
          </svg>
        </div>
        <div>
          <h1>HMPI — Groundwater Heavy Metal Monitor</h1>
          <p class="lead">Automated Heavy Metal Pollution Index — fast, consistent, auditable</p>
        </div>
      </div>

      <div style="text-align:right">
        <div style="font-size:13px;color:var(--muted)">Team: <strong>SafeWater</strong></div>
        <div style="margin-top:6px"><button class="ghost" onclick="showAbout()">About</button></div>
      </div>
    </header>

    <!-- top action cards -->
    <div class="cards" role="navigation" aria-label="key actions">
      <div class="card" onclick="scrollToForm()">
        <div style="display:flex;align-items:center;justify-content:space-between">
          <h3>Check Samples</h3>
          <div class="icon">🔬</div>
        </div>
        <p>Enter multiple metal concentrations manually and compute HMPI instantly.</p>
      </div>

      <div class="card" onclick="document.getElementById('csvFile').click()">
        <div style="display:flex;align-items:center;justify-content:space-between">
          <h3>Upload CSV</h3>
          <div class="icon">📁</div>
        </div>
        <p>Upload a CSV with multiple samples (name,pb,as,cd,lat,lon) for batch analysis.</p>
      </div>

      <div class="card" onclick="showReport()">
        <div style="display:flex;align-items:center;justify-content:space-between">
          <h3>View Map / Reports</h3>
          <div class="icon">🗺️</div>
        </div>
        <p>Visualize hotspots and export summary reports.</p>
      </div>

      <div class="card" onclick="showHelp()">
        <div style="display:flex;align-items:center;justify-content:space-between">
          <h3>How HMPI Works</h3>
          <div class="icon">📘</div>
        </div>
        <p>See the formula and editable guideline values used in calculations.</p>
      </div>
    </div>

    <!-- HERO -->
    <div class="hero">
      <div class="left">
        <div class="fact">
          <div class="badge">‼️</div>
          <div>
            <h2>Water quality matters — silently and quickly</h2>
            <p class="muted">Contaminated drinking water containing heavy metals causes long-term health risks. Rapid, consistent assessment helps communities act earlier.</p>
          </div>
        </div>

        <blockquote>
          “Automating HMPI calculations reduces human error and speeds up decisions. This tool helps scientists and policymakers spot unsafe water faster.”
        </blockquote>

        <div class="panel" style="margin-top:16px">
          <label>Quick Inputs — Enter up to 5 samples</label>
          <div id="multiSamples" style="margin-bottom:10px">
            <table id="samplesTable">
              <thead>
                <tr>
                  <th>Sample Name</th>
                  <th>Lead (Pb) mg/L</th>
                  <th>Arsenic (As) mg/L</th>
                  <th>Cadmium (Cd) mg/L</th>
                  <th>Lat (optional)</th>
                  <th>Lon (optional)</th>
                  <th>Action</th>
                </tr>
              </thead>
              <tbody>
                <!-- rows added dynamically -->
              </tbody>
            </table>
            <button class="ghost" onclick="addSampleRow()" id="addRowBtn">Add Sample</button>
          </div>

          <div style="display:flex;gap:8px;margin-top:12px">
            <div style="flex:1">
              <label>Guideline Pb (Si) mg/L</label>
              <input id="std_pb" type="number" step="any" value="0.01">
            </div>
            <div style="flex:1">
              <label>Guideline As (Si) mg/L</label>
              <input id="std_as" type="number" step="any" value="0.01">
            </div>
            <div style="flex:1">
              <label>Guideline Cd (Si) mg/L</label>
              <input id="std_cd" type="number" step="any" value="0.003">
            </div>
          </div>

          <div style="display:flex;gap:10px;align-items:center;margin-top:8px">
            <button class="cta" onclick="computeMulti()">Compute HMPI for Samples</button>
            <button class="ghost" onclick="resetMultiForm()">Reset</button>
            <div style="margin-left:auto">
              <small class="tiny">Editable guideline limits above — used in calculation</small>
            </div>
          </div>

        </div>

        <div class="note">Tip: Standards often vary by country and agency. Edit the guideline values above to match your reference before computing. Add up to 5 samples for manual entry.</div>
      </div>

      <aside>
        <div class="result-card" id="resultCard">
          <h3 style="margin-top:0">Quick Info</h3>
          <p class="muted">HMPI uses measured concentration (Mi) and standard permissible limits (Si) to compute a weighted index. You can process multiple samples manually or upload a CSV for batch processing.</p>
          <div style="margin-top:10px">
            <button class="ghost" onclick="showFormula()">Show Formula</button>
          </div>
        </div>
      </aside>
    </div>

    <!-- results + CSV area -->
    <div class="results">
      <div class="result-card">
        <h3 style="margin-top:0">Batch Analysis</h3>
        <p class="muted">Upload a CSV with columns: <code>name,pb,as,cd,lat,lon</code> (lat/lon optional). Or use manual inputs above.</p>
        <input id="csvFile" type="file" accept=".csv" style="margin-top:8px" onchange="handleCSV(event)">
        <div id="batchActions" style="margin-top:12px;display:flex;gap:8px">
          <button class="cta" id="processCSVBtn" onclick="processCSV()" disabled>Process CSV</button>
          <button class="ghost" onclick="clearBatch()">Clear</button>
          <button class="download" onclick="downloadBatch()" id="downloadBatchBtn" disabled>Download Results</button>
        </div>

        <div id="batchTableWrap" style="margin-top:12px;overflow:auto;max-height:360px"></div>
      </div>

      <div class="result-card">
        <h3 style="margin-top:0">Map & Summary</h3>
        <div id="map" style="height: 300px; border-radius: 10px; margin-top: 12px; margin-bottom: 12px;"></div>
        <p class="muted" id="mapNote">Map shows sample locations if lat/lon provided. Color-coded by risk: Green (Safe), Yellow (Moderate), Red (Unsafe).</p>

        <div id="summary" style="margin-top:8px">
          <div class="muted">Total samples: <span id="totalSamples">0</span></div>
          <div style="margin-top:8px">
            <canvas id="pieChart" style="max-height: 200px;"></canvas>
          </div>
          <div style="margin-top:12px">
            <small class="tiny">Classification thresholds: <strong>HMPI &lt; 50</strong> = Safe, <strong>50–100</strong> = Moderate, <strong>&gt;100</strong> = Unsafe.</small>
          </div>
        </div>

      </div>
    </div>

    <footer>
      Built for hackathon — HMPI automation. Data and output are for demonstration and require domain-validation before policy/health decisions.
    </footer>
  </div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
  // Utility: compute HMPI for a sample object {name, pb, as, cd, lat, lon}
  // Formula:
  // Qi = (Mi / Si) * 100
  // Wi = 1 / Si
  // HPI = sum(Wi * Qi) / sum(Wi)
  // We'll let user edit Si via inputs.

  function parseNum(v){
    if(v===null || v==="" || isNaN(Number(v))) return NaN;
    return Number(v);
  }

  function computeHMPI(sample, standards){
    // sample: {pb, as, cd}
    // standards: {pb, as, cd}
    const metals = ['pb','as','cd'];
    let sumWQ = 0, sumW = 0;
    for(const m of metals){
      const Mi = parseNum(sample[m]);
      const Si = parseNum(standards[m]);
      if(isNaN(Mi) || isNaN(Si) || Si === 0){
        // skip metal if missing or invalid
        continue;
      }
      // sub-index
      const Qi = (Mi / Si) * 100;
      const Wi = 1 / Si;
      sumWQ += Wi * Qi;
      sumW += Wi;
    }
    if(sumW === 0) return {hmpi: NaN};
    const hmpi = sumWQ / sumW;
    return {hmpi};
  }

  function riskLevel(hmpi){
    if(isNaN(hmpi)) return {label:'Unknown', color: 'var(--muted)', mapColor: 'gray'};
    if(hmpi < 50) return {label:'Safe', color: 'var(--success)', mapColor: 'green'};
    if(hmpi <= 100) return {label:'Moderate', color: 'var(--warning)', mapColor: 'yellow'};
    return {label:'Unsafe', color: 'var(--danger)', mapColor: 'red'};
  }

  // MULTI SAMPLE UI
  function addSampleRow(){
    const tbody = document.querySelector('#samplesTable tbody');
    if(tbody.children.length >= 5){
      alert('Maximum 5 samples for manual entry. Use CSV for more.');
      return;
    }
    const row = document.createElement('tr');
    row.innerHTML = `
      <td><input type="text" placeholder="e.g., Well-12"></td>
      <td><input type="number" step="any" placeholder="e.g., 0.015"></td>
      <td><input type="number" step="any" placeholder="e.g., 0.02"></td>
      <td><input type="number" step="any" placeholder="e.g., 0.002"></td>
      <td><input type="number" step="any" placeholder="e.g., 37.7749"></td>
      <td><input type="number" step="any" placeholder="e.g., -122.4194"></td>
      <td><button class="ghost" onclick="removeRow(this)">Remove</button></td>
    `;
    tbody.appendChild(row);
  }

  function removeRow(btn){
    btn.closest('tr').remove();
  }

  function computeMulti(){
    const rows = document.querySelectorAll('#samplesTable tbody tr');
    if(rows.length === 0){
      alert('Add at least one sample to compute.');
      return;
    }
    _csvRows = [];
    for(const row of rows){
      const inputs = row.querySelectorAll('input');
      _csvRows.push({
        name: inputs[0].value || 'Sample',
        pb: inputs[1].value,
        as: inputs[2].value,
        cd: inputs[3].value,
        lat: inputs[4].value,
        lon: inputs[5].value
      });
    }
    document.getElementById('processCSVBtn').disabled = false;
    processCSV();
  }

  function resetMultiForm(){
    const tbody = document.querySelector('#samplesTable tbody');
    tbody.innerHTML = '';
    addSampleRow(); // add one back
    clearBatch();
  }

  // CSV Handling
  let _csvRows = []; // array of objects
  function handleCSV(evt){
    const file = evt.target.files[0];
    if(!file) return;
    const reader = new FileReader();
    reader.onload = function(e){
      const text = e.target.result;
      parseCSV(text);
    };
    reader.readAsText(file);
  }

  function parseCSV(text){
    const lines = text.trim().split(/\r?\n/).filter(l=>l.trim().length>0);
    if(lines.length === 0) return;
    const header = lines[0].split(',').map(h=>h.trim().toLowerCase());
    const rows = [];
    for(let i=1;i<lines.length;i++){
      const cols = lines[i].split(',').map(c=>c.trim());
      const obj = {};
      for(let j=0;j<header.length;j++){
        obj[header[j]] = cols[j] !== undefined ? cols[j].trim() : '';
      }
      rows.push(obj);
    }
    _csvRows = rows;
    document.getElementById('processCSVBtn').disabled = false;
    renderCSVPreview();
  }

  function renderCSVPreview(){
    const wrap = document.getElementById('batchTableWrap');
    if(_csvRows.length === 0){
      wrap.innerHTML = '<div class="muted">No data loaded.</div>';
      return;
    }
    let html = '<table><thead><tr>';
    const keys = Object.keys(_csvRows[0]);
    for(const k of keys) html += `<th>${escapeHtml(k)}</th>`;
    html += '</tr></thead><tbody>';
    for(let i=0;i<Math.min(25,_csvRows.length);i++){
      html += '<tr>';
      for(const k of keys) html += `<td>${escapeHtml(_csvRows[i][k] || '')}</td>`;
      html += '</tr>';
    }
    html += '</tbody></table>';
    wrap.innerHTML = html;
  }

  let map; // global map var
  let pieChart; // global pie chart var

  function initMap(){
    if(map) map.remove(); // reset if exists
    map = L.map('map').setView([0, 0], 2);
    L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);
  }

  function processCSV(){
    if(_csvRows.length === 0) return;
    const std_pb = parseNum(document.getElementById('std_pb').value);
    const std_as = parseNum(document.getElementById('std_as').value);
    const std_cd = parseNum(document.getElementById('std_cd').value);
    if(isNaN(std_pb) || isNaN(std_as) || isNaN(std_cd)){
      alert('Please enter valid guideline values.');
      return;
    }
    const standards = {pb: std_pb, as: std_as, cd: std_cd};
    const results = [];
    let cSafe=0,cMod=0,cUn=0,cUnknown=0;
    initMap(); // reset map
    const bounds = L.latLngBounds();
    let hasGeo = false;
    for(const r of _csvRows){
      const sample = {
        pb: parseNum(r.pb ?? r['pb(mg/l)'] ?? r['lead'] ?? r['lead_mg_l'] ?? r['pb(mg/l)']),
        as: parseNum(r.as ?? r.arsenic ?? r['as(mg/l)']),
        cd: parseNum(r.cd ?? r.cadmium ?? r['cd(mg/l)'])
      };
      const out = computeHMPI(sample, standards);
      const h = isNaN(out.hmpi) ? null : Number(out.hmpi);
      const lvl = riskLevel(h || NaN);
      if(lvl.label === 'Safe') cSafe++;
      else if(lvl.label==='Moderate') cMod++;
      else if(lvl.label==='Unsafe') cUn++;
      else cUnknown++;
      const result = Object.assign({}, r, {hmpi: h===null ? '' : h.toFixed(4), level: lvl.label});
      results.push(result);

      // add to map if lat/lon
      const lat = parseNum(r.lat);
      const lon = parseNum(r.lon);
      if(!isNaN(lat) && !isNaN(lon)){
        hasGeo = true;
        L.marker([lat, lon], {icon: L.divIcon({className: 'marker', html: `<div style="background:${lvl.mapColor};width:20px;height:20px;border-radius:50%;"></div>`})})
          .addTo(map)
          .bindPopup(`Sample: ${escapeHtml(r.name || 'Unnamed')}<br>HMPI: ${result.hmpi || 'N/A'}<br>Level: ${lvl.label}`);
        bounds.extend([lat, lon]);
      }
    }
    window._batchResults = results;
    // render results table
    const wrap = document.getElementById('batchTableWrap');
    let html = '<table><thead><tr>';
    const keys = Object.keys(results[0]);
    for(const k of keys) html += `<th>${escapeHtml(k)}</th>`;
    html += '</tr></thead><tbody>';
    for(let i=0;i<results.length;i++){
      html += '<tr>';
      for(const k of keys) html += `<td>${escapeHtml(results[i][k] || '')}</td>`;
      html += '</tr>';
    }
    html += '</tbody></table>';
    wrap.innerHTML = html;

    document.getElementById('totalSamples').innerText = results.length;
    // Update pie chart
    if(pieChart) pieChart.destroy();
    const ctx = document.getElementById('pieChart').getContext('2d');
    pieChart = new Chart(ctx, {
      type: 'pie',
      data: {
        labels: ['Safe', 'Moderate', 'Unsafe', 'Unknown'],
        datasets: [{
          data: [cSafe, cMod, cUn, cUnknown],
          backgroundColor: ['var(--success)', 'var(--warning)', 'var(--danger)', 'var(--muted)'],
          borderWidth: 1
        }]
      },
      options: {
        responsive: true,
        plugins: {
          legend: {position: 'top'},
          title: {display: true, text: 'Risk Distribution', color: 'var(--white)'},
          tooltip: {
            callbacks: {
              label: function(context) {
                let label = context.label || '';
                if (label) {
                  label += ': ';
                }
                if (context.parsed !== null) {
                  label += context.parsed + ' samples';
                }
                return label;
              }
            }
          }
        }
      }
    });

    // Map fit
    if(hasGeo && bounds.isValid()){
      map.fitBounds(bounds, {padding: [50, 50]});
      document.getElementById('mapNote').innerText = 'Map shows color-coded sample locations.';
    } else {
      document.getElementById('mapNote').innerText = 'No geo-coordinates provided for mapping.';
    }

    document.getElementById('downloadBatchBtn').disabled = false;
    alert('Processed — results shown. View table, map, and pie chart. You can download the annotated CSV.');
  }

  function downloadBatch(){
    if(!window._batchResults || window._batchResults.length===0) return;
    const keys = Object.keys(window._batchResults[0]);
    const rows = window._batchResults.map(r => keys.map(k => `"${(r[k]||'').toString().replace(/"/g,'""')}"`).join(','));
    const csv = keys.join(',') + '\n' + rows.join('\n');
    const blob = new Blob([csv], {type:'text/csv'});
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a'); a.href = url; a.download = 'hmpi_results.csv'; document.body.appendChild(a); a.click(); a.remove(); URL.revokeObjectURL(url);
  }

  function clearBatch(){
    _csvRows = [];
    window._batchResults = null;
    document.getElementById('batchTableWrap').innerHTML = '<div class="muted">No data loaded.</div>';
    document.getElementById('processCSVBtn').disabled = true;
    document.getElementById('downloadBatchBtn').disabled = true;
    document.getElementById('totalSamples').innerText = '0';
    if(pieChart) pieChart.destroy();
    document.getElementById('pieChart').getContext('2d').clearRect(0,0,document.getElementById('pieChart').width,document.getElementById('pieChart').height);
    initMap();
    document.getElementById('mapNote').innerText = 'Map visualization — add samples with lat/lon to see markers.';
    document.getElementById('csvFile').value = '';
  }

  // small helpers
  function escapeHtml(s){
    if(!s && s !== 0) return '';
    return (''+s).replace(/[&<>"']/g, function(m){ return ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[m])});
  }

  // UI helpers
  function showAbout(){
    alert('HMPI Demo — Automated Heavy Metal Pollution Index calculator. This is a hackathon prototype. Validate outputs with domain experts before use.');
  }
  function showHelp(){
    alert('HMPI formula used: Qi = (Mi/Si)*100; Wi = 1/Si; HMPI = sum(Wi*Qi) / sum(Wi). Default standards are editable in the UI.');
  }
  function showFormula(){
    alert('Formula:\nQi = (Mi / Si) * 100\nWi = 1 / Si\nHMPI = (Σ Wi*Qi) / (Σ Wi)\nClassification: HMPI < 50: Safe; 50–100: Moderate; >100: Unsafe');
  }
  function showReport(){ alert('View the map and summary below after processing samples.') }
  function scrollToForm(){ window.scrollTo({top:200, behavior:'smooth'}); }

  // initialize
  initMap();
  addSampleRow(); // start with one row
  clearBatch();

</script>
</body>
</html>
Front END2(Complex):
<!-- index.html (Main Input Page) -->
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>HMPI — Heavy Metal Pollution Index</title>

  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&display=swap" rel="stylesheet">

  <style>
    :root{
      --bg-deep:#02182b;
      --teal:#0aa3a3;
      --aqua:#2dd4bf;
      --accent:#ffd166; /* warm gold accent */
      --card:#062833;
      --muted:#9fb6b6;
      --glass: rgba(255,255,255,0.06);
      --success:#16a34a;
      --warning:#f59e0b;
      --danger:#ef4444;
      --white: #ffffff;
      --soft-shadow: 0 6px 18px rgba(2,24,43,0.6);
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family:'Inter',system-ui,-apple-system,Segoe UI,Roboto,"Helvetica Neue",Arial;
      color:var(--white);
      background: linear-gradient(180deg, rgba(2,24,43,0.92), rgba(2,24,43,0.92)), url('https://images.unsplash.com/photo-1507525428034-b723cf961d3e?q=80&w=2000&auto=format&fit=crop&ixlib=rb-4.0.3&s=3a2ff3b577d30c9cba2c6d8fbb8a3b81') center/cover fixed;
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      min-height:100vh;
      padding:40px;
    }

    .container{max-width:1100px;margin:0 auto}

    /* header / hero */
    header{
      display:flex;
      gap:24px;
      align-items:center;
      justify-content:space-between;
      margin-bottom:28px;
    }
    .brand{
      display:flex;gap:12px;align-items:center;
    }
    .logo{
      width:64px;height:64px;border-radius:12px;background:linear-gradient(135deg,var(--teal),var(--aqua));display:flex;align-items:center;justify-content:center;box-shadow: 0 6px 20px rgba(10,163,163,0.18);
    }
    .logo svg{filter:drop-shadow(0 6px 18px rgba(0,0,0,0.35));}
    h1{font-size:20px;margin:0;font-weight:700;letter-spacing:0.2px}
    p.lead{margin:0;color:var(--muted);font-size:13px}

    /* top cards */
    .cards{display:grid;grid-template-columns:repeat(4,1fr);gap:16px;margin-top:18px;margin-bottom:22px}
    .card{
      background: linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.02));
      border-radius:12px;padding:18px;box-shadow:var(--soft-shadow);
      border:1px solid rgba(255,255,255,0.04);cursor:pointer;transition:transform .18s ease, box-shadow .18s ease;
      display:flex;flex-direction:column;gap:8px;min-height:110px;
    }
    .card:hover{transform:translateY(-6px);box-shadow:0 18px 40px rgba(2,24,43,0.7)}
    .card h3{margin:0;font-size:15px}
    .card p{margin:0;color:var(--muted);font-size:12px}

    /* hero content */
    .hero{
      display:grid;grid-template-columns:1fr 420px;gap:22px;margin-top:18px;margin-bottom:20px;
    }
    .hero .left{
      background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      padding:22px;border-radius:14px;border:1px solid rgba(255,255,255,0.04);
      box-shadow:var(--soft-shadow);
    }
    .fact{
      display:flex;gap:14px;align-items:flex-start;margin-bottom:14px;
    }
    .fact .badge{
      width:56px;height:56px;border-radius:10px;background:linear-gradient(135deg,var(--accent),#ffb84d);display:flex;align-items:center;justify-content:center;color:#052a00;font-weight:800;
      font-size:14px;
    }
    .fact h2{margin:0;font-size:20px}
    .fact p{margin:6px 0 0 0;color:var(--muted);font-size:14px}

    blockquote{margin:0;padding:14px;border-left:4px solid rgba(255,255,255,0.04);color:var(--muted);font-style:italic;background:linear-gradient(90deg, rgba(255,255,255,0.01), rgba(255,255,255,0.00));border-radius:8px;margin-top:12px}

    /* form area */
    .panel{
      margin-top:14px;background:var(--glass);padding:14px;border-radius:10px;border:1px solid rgba(255,255,255,0.04);
    }
    label{display:block;font-size:13px;margin-bottom:6px;color:var(--muted)}
    input[type="text"], input[type="number"], input[type="file"], select{
      width:100%;padding:10px;border-radius:8px;border:1px solid rgba(255,255,255,0.06);background:transparent;color:var(--white);outline:none;font-size:14px;
    }
    .row{display:flex;gap:12px}
    .col{flex:1}

    button.cta{
      background:linear-gradient(90deg,var(--teal),var(--aqua));border:none;padding:12px 18px;border-radius:10px;color:#002323;font-weight:700;cursor:pointer;margin-top:8px;
      box-shadow:0 10px 28px rgba(10,163,163,0.14);
    }
    button.ghost{background:transparent;border:1px solid rgba(255,255,255,0.06);padding:10px;border-radius:8px;color:var(--muted);cursor:pointer}

    /* results */
    .results{margin-top:18px;display:grid;grid-template-columns:1fr 360px;gap:18px}
    .result-card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));padding:14px;border-radius:12px;border:1px solid rgba(255,255,255,0.04);box-shadow:var(--soft-shadow)}
    .status{
      display:flex;align-items:center;gap:12px;padding:10px;border-radius:10px;font-weight:700;
    }
    .status .dot{width:14px;height:14px;border-radius:4px;display:inline-block}
    table{width:100%;border-collapse:collapse;color:var(--muted);font-size:13px}
    th,td{padding:10px;text-align:left;border-bottom:1px dashed rgba(255,255,255,0.03)}
    th{color:var(--muted);font-weight:600}

    /* small helpers */
    .muted{color:var(--muted);font-size:13px}
    .note{font-size:12px;color:var(--muted);margin-top:8px}
    .tiny{font-size:12px;color:var(--muted)}

    footer{margin-top:28px;color:var(--muted);font-size:13px;text-align:center}

    /* responsive */
    @media(max-width:980px){
      .hero{grid-template-columns:1fr}
      .cards{grid-template-columns:repeat(2,1fr)}
      .results{grid-template-columns:1fr}
    }
    @media(max-width:520px){
      .cards{grid-template-columns:1fr}
    }

    /* little icon */
    .icon{
      width:38px;height:38px;border-radius:8px;background:rgba(255,255,255,0.03);display:flex;align-items:center;justify-content:center;color:var(--aqua);
    }

    .download{
      background:linear-gradient(90deg,#7b61ff,#ffd166);border:none;padding:10px 12px;border-radius:10px;color:#02182b;font-weight:700;cursor:pointer;
    }

    /* table for multi inputs */
    #samplesTable td {padding: 4px;}
    #samplesTable input {margin: 0;}

  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="brand">
        <div class="logo" aria-hidden>
          <!-- water droplet + test tube icon -->
          <svg width="34" height="34" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M12 2s-5 5.5-5 8.5A5 5 0 1 0 17 10C17 7.5 12 2 12 2z" fill="#02182b" opacity="0.95"/>
            <path d="M12 2s-5 5.5-5 8.5A5 5 0 1 0 17 10C17 7.5 12 2 12 2z" stroke="#fff" stroke-opacity=".12"/>
            <circle cx="12" cy="14.5" r="2.5" fill="#ffd166"/>
          </svg>
        </div>
        <div>
          <h1>HMPI — Groundwater Heavy Metal Monitor</h1>
          <p class="lead">Automated Heavy Metal Pollution Index — fast, consistent, auditable</p>
        </div>
      </div>

      <div style="text-align:right">
        <div style="font-size:13px;color:var(--muted)">Team: <strong>SafeWater</strong></div>
        <div style="margin-top:6px"><button class="ghost" onclick="showAbout()">About</button></div>
      </div>
    </header>

    <!-- top action cards -->
    <div class="cards" role="navigation" aria-label="key actions">
      <div class="card" onclick="scrollToForm()">
        <div style="display:flex;align-items:center;justify-content:space-between">
          <h3>Check Samples</h3>
          <div class="icon">🔬</div>
        </div>
        <p>Enter multiple metal concentrations manually and compute HMPI instantly.</p>
      </div>

      <div class="card" onclick="document.getElementById('csvFile').click()">
        <div style="display:flex;align-items:center;justify-content:space-between">
          <h3>Upload CSV</h3>
          <div class="icon">📁</div>
        </div>
        <p>Upload a CSV with multiple samples (name,pb,as,cd,lat,lon) for batch analysis.</p>
      </div>

      <div class="card" onclick="showReport()">
        <div style="display:flex;align-items:center;justify-content:space-between">
          <h3>View Map / Reports</h3>
          <div class="icon">🗺️</div>
        </div>
        <p>Visualize hotspots and export summary reports.</p>
      </div>

      <div class="card" onclick="showHelp()">
        <div style="display:flex;align-items:center;justify-content:space-between">
          <h3>How HMPI Works</h3>
          <div class="icon">📘</div>
        </div>
        <p>See the formula and editable guideline values used in calculations.</p>
      </div>
    </div>

    <!-- HERO -->
    <div class="hero">
      <div class="left">
        <div class="fact">
          <div class="badge">‼️</div>
          <div>
            <h2>Water quality matters — silently and quickly</h2>
            <p class="muted">Contaminated drinking water containing heavy metals causes long-term health risks. Rapid, consistent assessment helps communities act earlier.</p>
          </div>
        </div>

        <blockquote>
          “Automating HMPI calculations reduces human error and speeds up decisions. This tool helps scientists and policymakers spot unsafe water faster.”
        </blockquote>

        <div class="panel" style="margin-top:16px">
          <label>Quick Inputs — Enter up to 5 samples</label>
          <div id="multiSamples" style="margin-bottom:10px">
            <table id="samplesTable">
              <thead>
                <tr>
                  <th>Sample Name</th>
                  <th>Lead (Pb) mg/L</th>
                  <th>Arsenic (As) mg/L</th>
                  <th>Cadmium (Cd) mg/L</th>
                  <th>Lat (optional)</th>
                  <th>Lon (optional)</th>
                  <th>Action</th>
                </tr>
              </thead>
              <tbody>
                <!-- rows added dynamically -->
              </tbody>
            </table>
            <button class="ghost" onclick="addSampleRow()" id="addRowBtn">Add Sample</button>
          </div>

          <div style="display:flex;gap:8px;margin-top:12px">
            <div style="flex:1">
              <label>Guideline Pb (Si) mg/L</label>
              <input id="std_pb" type="number" step="any" value="0.01">
            </div>
            <div style="flex:1">
              <label>Guideline As (Si) mg/L</label>
              <input id="std_as" type="number" step="any" value="0.01">
            </div>
            <div style="flex:1">
              <label>Guideline Cd (Si) mg/L</label>
              <input id="std_cd" type="number" step="any" value="0.003">
            </div>
          </div>

          <div style="display:flex;gap:10px;align-items:center;margin-top:8px">
            <button class="cta" onclick="computeMulti()">Compute HMPI for Samples</button>
            <button class="ghost" onclick="resetMultiForm()">Reset</button>
            <div style="margin-left:auto">
              <small class="tiny">Editable guideline limits above — used in calculation</small>
            </div>
          </div>

        </div>

        <div class="note">Tip: Standards often vary by country and agency. Edit the guideline values above to match your reference before computing. Add up to 5 samples for manual entry.</div>
      </div>

      <aside>
        <div class="result-card" id="resultCard">
          <h3 style="margin-top:0">Quick Info</h3>
          <p class="muted">HMPI uses measured concentration (Mi) and standard permissible limits (Si) to compute a weighted index. You can process multiple samples manually or upload a CSV for batch processing.</p>
          <div style="margin-top:10px">
            <button class="ghost" onclick="showFormula()">Show Formula</button>
          </div>
        </div>
      </aside>
    </div>

    <!-- results + CSV area -->
    <div class="results">
      <div class="result-card">
        <h3 style="margin-top:0">Batch Analysis</h3>
        <p class="muted">Upload a CSV with columns: <code>name,pb,as,cd,lat,lon</code> (lat/lon optional). Or use manual inputs above.</p>
        <input id="csvFile" type="file" accept=".csv" style="margin-top:8px" onchange="handleCSV(event)">
        <div id="batchActions" style="margin-top:12px;display:flex;gap:8px">
          <button class="cta" id="processCSVBtn" onclick="processCSV()" disabled>Process CSV</button>
          <button class="ghost" onclick="clearBatch()">Clear</button>
          <button class="download" onclick="downloadBatch()" id="downloadBatchBtn" disabled>Download Results</button>
        </div>

        <div id="batchTableWrap" style="margin-top:12px;overflow:auto;max-height:360px"></div>
      </div>

      <div class="result-card">
        <h3 style="margin-top:0">Quick Summary</h3>
        <p class="muted">After processing, view detailed analysis on the new page.</p>
      </div>
    </div>

    <footer>
      Built for hackathon — HMPI automation. Data and output are for demonstration and require domain-validation before policy/health decisions.
    </footer>
  </div>

<script>
  // Utility functions...
  function parseNum(v){
    if(v===null || v==="" || isNaN(Number(v))) return NaN;
    return Number(v);
  }

  function computeHMPI(sample, standards){
    const metals = ['pb','as','cd'];
    let sumWQ = 0, sumW = 0;
    for(const m of metals){
      const Mi = parseNum(sample[m]);
      const Si = parseNum(standards[m]);
      if(isNaN(Mi) || isNaN(Si) || Si === 0){
        continue;
      }
      const Qi = (Mi / Si) * 100;
      const Wi = 1 / Si;
      sumWQ += Wi * Qi;
      sumW += Wi;
    }
    if(sumW === 0) return {hmpi: NaN};
    const hmpi = sumWQ / sumW;
    return {hmpi};
  }

  function riskLevel(hmpi){
    if(isNaN(hmpi)) return {label:'Unknown', color: 'var(--muted)', mapColor: 'gray'};
    if(hmpi < 50) return {label:'Safe', color: 'var(--success)', mapColor: 'green'};
    if(hmpi <= 100) return {label:'Moderate', color: 'var(--warning)', mapColor: 'yellow'};
    return {label:'Unsafe', color: 'var(--danger)', mapColor: 'red'};
  }

  // MULTI SAMPLE UI
  function addSampleRow(){
    const tbody = document.querySelector('#samplesTable tbody');
    if(tbody.children.length >= 5){
      alert('Maximum 5 samples for manual entry. Use CSV for more.');
      return;
    }
    const row = document.createElement('tr');
    row.innerHTML = `
      <td><input type="text" placeholder="e.g., Well-12"></td>
      <td><input type="number" step="any" placeholder="e.g., 0.015"></td>
      <td><input type="number" step="any" placeholder="e.g., 0.02"></td>
      <td><input type="number" step="any" placeholder="e.g., 0.002"></td>
      <td><input type="number" step="any" placeholder="e.g., 37.7749"></td>
      <td><input type="number" step="any" placeholder="e.g., -122.4194"></td>
      <td><button class="ghost" onclick="removeRow(this)">Remove</button></td>
    `;
    tbody.appendChild(row);
  }

  function removeRow(btn){
    btn.closest('tr').remove();
  }

  function computeMulti(){
    const rows = document.querySelectorAll('#samplesTable tbody tr');
    if(rows.length === 0){
      alert('Add at least one sample to compute.');
      return;
    }
    _csvRows = [];
    for(const row of rows){
      const inputs = row.querySelectorAll('input');
      _csvRows.push({
        name: inputs[0].value || 'Sample',
        pb: inputs[1].value,
        as: inputs[2].value,
        cd: inputs[3].value,
        lat: inputs[4].value,
        lon: inputs[5].value
      });
    }
    processCSV(); // Now redirects to analysis
  }

  function resetMultiForm(){
    const tbody = document.querySelector('#samplesTable tbody');
    tbody.innerHTML = '';
    addSampleRow();
    clearBatch();
  }

  // CSV Handling
  let _csvRows = [];
  function handleCSV(evt){
    const file = evt.target.files[0];
    if(!file) return;
    const reader = new FileReader();
    reader.onload = function(e){
      const text = e.target.result;
      parseCSV(text);
    };
    reader.readAsText(file);
  }

  function parseCSV(text){
    const lines = text.trim().split(/\r?\n/).filter(l=>l.trim().length>0);
    if(lines.length === 0) return;
    const header = lines[0].split(',').map(h=>h.trim().toLowerCase());
    const rows = [];
    for(let i=1;i<lines.length;i++){
      const cols = lines[i].split(',').map(c=>c.trim());
      const obj = {};
      for(let j=0;j<header.length;j++){
        obj[header[j]] = cols[j] !== undefined ? cols[j].trim() : '';
      }
      rows.push(obj);
    }
    _csvRows = rows;
    renderCSVPreview();
  }

  function renderCSVPreview(){
    const wrap = document.getElementById('batchTableWrap');
    if(_csvRows.length === 0){
      wrap.innerHTML = '<div class="muted">No data loaded.</div>';
      return;
    }
    let html = '<table><thead><tr>';
    const keys = Object.keys(_csvRows[0]);
    for(const k of keys) html += `<th>${escapeHtml(k)}</th>`;
    html += '</tr></thead><tbody>';
    for(let i=0;i<Math.min(25,_csvRows.length);i++){
      html += '<tr>';
      for(const k of keys) html += `<td>${escapeHtml(_csvRows[i][k] || '')}</td>`;
      html += '</tr>';
    }
    html += '</tbody></table>';
    wrap.innerHTML = html;
  }

  function processCSV(){
    if(_csvRows.length === 0) return;
    const std_pb = parseNum(document.getElementById('std_pb').value);
    const std_as = parseNum(document.getElementById('std_as').value);
    const std_cd = parseNum(document.getElementById('std_cd').value);
    if(isNaN(std_pb) || isNaN(std_as) || isNaN(std_cd)){
      alert('Please enter valid guideline values.');
      return;
    }
    const standards = {pb: std_pb, as: std_as, cd: std_cd};
    const results = [];
    let cSafe=0,cMod=0,cUn=0,cUnknown=0;
    for(const r of _csvRows){
      const sample = {
        pb: parseNum(r.pb ?? r['pb(mg/l)'] ?? r['lead'] ?? r['lead_mg_l'] ?? r['pb(mg/l)']),
        as: parseNum(r.as ?? r.arsenic ?? r['as(mg/l)']),
        cd: parseNum(r.cd ?? r.cadmium ?? r['cd(mg/l)'])
      };
      const out = computeHMPI(sample, standards);
      const h = isNaN(out.hmpi) ? null : Number(out.hmpi);
      const lvl = riskLevel(h || NaN);
      if(lvl.label === 'Safe') cSafe++;
      else if(lvl.label==='Moderate') cMod++;
      else if(lvl.label==='Unsafe') cUn++;
      else cUnknown++;
      const result = Object.assign({}, r, {hmpi: h===null ? '' : h.toFixed(4), level: lvl.label});
      results.push(result);
    }
    // Store in localStorage and redirect to analysis.html
    localStorage.setItem('hmpiResults', JSON.stringify({
      results: results,
      counts: {safe: cSafe, mod: cMod, un: cUn, unknown: cUnknown},
      standards: standards
    }));
    window.location.href = 'analysis.html';
  }

  function downloadBatch(){
    // Optional: If needed on input page, but moved to analysis
  }

  function clearBatch(){
    _csvRows = [];
    document.getElementById('batchTableWrap').innerHTML = '<div class="muted">No data loaded.</div>';
    document.getElementById('csvFile').value = '';
  }

  function escapeHtml(s){
    if(!s && s !== 0) return '';
    return (''+s).replace(/[&<>"']/g, function(m){ return ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[m])});
  }

  // UI helpers
  function showAbout(){
    alert('HMPI Demo — Automated Heavy Metal Pollution Index calculator. This is a hackathon prototype. Validate outputs with domain experts before use.');
  }
  function showHelp(){
    alert('HMPI formula used: Qi = (Mi/Si)*100; Wi = 1/Si; HMPI = sum(Wi*Qi) / sum(Wi). Default standards are editable in the UI.');
  }
  function showFormula(){
    alert('Formula:\nQi = (Mi / Si) * 100\nWi = 1 / Si\nHMPI = (Σ Wi*Qi) / (Σ Wi)\nClassification: HMPI < 50: Safe; 50–100: Moderate; >100: Unsafe');
  }
  function showReport(){ alert('Process samples first to view analysis.') }
  function scrollToForm(){ window.scrollTo({top:200, behavior:'smooth'}); }

  // initialize
  addSampleRow(); // start with one row
  clearBatch();

</script>
</body>
</html>
