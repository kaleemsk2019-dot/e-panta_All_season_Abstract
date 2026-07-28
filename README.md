<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Andhra Pradesh Agriculture Season Dashboard</title>
<style>
:root{
  --soil-dark:#2b2118;
  --soil:#5b4636;
  --kharif:#1f8f4e;
  --kharif-light:#34c86c;
  --rabi:#c2650b;
  --rabi-light:#f0a13a;
  --wheat:#f4ead3;
  --cream:#faf6ec;
  --ink:#22281f;
  --line:#e2d9c3;
  --pos:#1f8f4e;
  --neg:#c0392b;
  --card:#ffffff;
  --shadow:0 4px 18px rgba(43,33,24,0.09);
}
*{box-sizing:border-box;}
body{
  margin:0;
  font-family:'Segoe UI',Arial,sans-serif;
  background:
    radial-gradient(circle at 8% 0%, #eef3e4 0%, transparent 45%),
    radial-gradient(circle at 95% 10%, #fdeedb 0%, transparent 40%),
    var(--cream);
  color:var(--ink);
  min-height:100vh;
}

/* ===== HEADER ===== */
header.top{
  background:linear-gradient(120deg,var(--soil-dark) 0%,var(--soil) 55%, #6b4f2e 100%);
  color:#fdf8ee;
  padding:34px 28px 26px;
  position:relative;
  overflow:hidden;
}
header.top::after{
  content:"";
  position:absolute; right:-60px; top:-60px;
  width:260px; height:260px; border-radius:50%;
  background:radial-gradient(circle, rgba(52,200,108,0.35), transparent 70%);
}
header.top .eyebrow{
  letter-spacing:3px;
  text-transform:uppercase;
  font-size:11.5px;
  color:#c9e8b0;
  font-weight:700;
  margin-bottom:6px;
}
header.top h1{
  margin:0 0 6px;
  font-size:clamp(22px,3.2vw,32px);
  font-weight:800;
  letter-spacing:0.3px;
}
header.top p{
  margin:0;
  color:#e7ddc8;
  font-size:14px;
  max-width:760px;
  line-height:1.5;
}
.season-strip{
  display:flex; gap:8px; margin-top:18px; flex-wrap:wrap;
}
.season-chip{
  font-size:11.5px; font-weight:700; padding:5px 11px; border-radius:20px;
  border:1px solid rgba(255,255,255,0.25); color:#fdf8ee;
}
.season-chip.k{background:rgba(52,200,108,0.28);}
.season-chip.r{background:rgba(240,161,58,0.28);}

/* ===== TABS ===== */
nav.tabs{
  display:flex;
  max-width:1180px;
  margin:-22px auto 0;
  position:relative;
  z-index:5;
  background:var(--card);
  border-radius:14px;
  box-shadow:var(--shadow);
  padding:6px;
  gap:6px;
}
nav.tabs button{
  flex:1;
  border:none;
  background:transparent;
  padding:14px 10px;
  font-size:14.5px;
  font-weight:700;
  color:#7a7060;
  border-radius:10px;
  cursor:pointer;
  transition:.25s;
  display:flex; align-items:center; justify-content:center; gap:8px;
}
nav.tabs button:hover{ color:var(--soil); background:#f4ead3aa; }
nav.tabs button.active{
  color:#fff;
  background:linear-gradient(120deg,var(--kharif),#166a3c);
  box-shadow:0 4px 12px rgba(31,143,78,0.35);
}
nav.tabs button.active.rabi-active{
  background:linear-gradient(120deg,var(--rabi),#9c4d05);
  box-shadow:0 4px 12px rgba(194,101,11,0.35);
}

main{
  max-width:1180px;
  margin:26px auto 60px;
  padding:0 18px;
}
.panel{ display:none; animation:fadein .35s ease; }
.panel.active{ display:block; }
@keyframes fadein{ from{opacity:0; transform:translateY(6px);} to{opacity:1; transform:none;} }

/* ===== CONTROLS CARD ===== */
.controls-card{
  background:var(--card);
  border-radius:16px;
  box-shadow:var(--shadow);
  padding:20px 22px;
  margin-bottom:20px;
  display:flex;
  gap:22px;
  flex-wrap:wrap;
  align-items:flex-end;
  border:1px solid var(--line);
}
.control-group{ min-width:230px; }
.control-group label{
  display:block;
  font-weight:700;
  font-size:12.5px;
  letter-spacing:.4px;
  text-transform:uppercase;
  color:var(--soil);
  margin-bottom:7px;
}
select{
  width:100%;
  padding:11px 38px 11px 14px;
  border-radius:10px;
  border:1.5px solid var(--line);
  background:#fff;
  font-size:14px;
  font-weight:600;
  color:var(--ink);
  cursor:pointer;
  appearance:none;
  background-image:url("data:image/svg+xml;utf8,<svg fill='%235b4636' height='22' viewBox='0 0 24 24' width='22' xmlns='http://www.w3.org/2000/svg'><path d='M7 10l5 5 5-5z'/></svg>");
  background-repeat:no-repeat;
  background-position:right 10px center;
  transition:.2s;
}
select:hover{ border-color:var(--kharif); }
select:focus{ outline:none; border-color:var(--rabi); box-shadow:0 0 0 3px rgba(194,101,11,0.15); }
.hint-pill{
  font-size:12px;
  color:#8a7e68;
  background:var(--wheat);
  padding:8px 12px;
  border-radius:10px;
  font-weight:600;
}

/* ===== TABLE CARD ===== */
.table-card{
  background:var(--card);
  border-radius:16px;
  box-shadow:var(--shadow);
  border:1px solid var(--line);
  overflow:auto;
  max-height:72vh;
}
table{
  width:100%;
  border-collapse:collapse;
  font-size:13px;
  min-width:900px;
}
thead th{
  position:sticky; top:0; z-index:3;
  padding:10px 8px;
  text-align:center;
  border:1px solid rgba(255,255,255,0.25);
  font-weight:700;
  font-size:12.5px;
}
.kharif-header{background:var(--kharif); color:#fff;}
.kharif-sub{background:var(--kharif-light) !important; color:#fff; top:37px !important;}
.rabi-header{background:var(--rabi); color:#fff;}
.rabi-sub{background:var(--rabi-light) !important; color:#fff; top:37px !important;}
.snhdr{background:var(--soil-dark); color:#fff; top:0;}

tbody td{
  border:1px solid var(--line);
  padding:8px 10px;
  text-align:right;
  white-space:nowrap;
}
tbody td:first-child{ text-align:center; color:#9b8f78; }
tbody td.district-cell{
  text-align:left;
  font-weight:700;
  color:var(--soil-dark);
  position:sticky; left:0;
  background:inherit;
}
tbody tr:nth-child(even){ background:#faf6ec; }
tbody tr:nth-child(even) td.district-cell{ background:#faf6ec; }
tbody tr:nth-child(odd) td.district-cell{ background:#ffffff; }
tbody tr:hover{ background:#eaf5ea; }
tbody tr:hover td.district-cell{ background:#eaf5ea; }
.hl{ background:#FFF2CC !important; font-weight:700; }
tfoot td{
  background:var(--soil-dark);
  color:#fdf8ee;
  font-weight:800;
  font-size:13.5px;
  padding:10px;
  text-align:right;
  position:sticky; bottom:0;
}
tfoot td:first-child, tfoot td.district-cell{ text-align:left; background:var(--soil-dark); }

/* ===== DIFF CARDS ===== */
.diff-grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:20px;
}
@media (max-width:880px){ .diff-grid{ grid-template-columns:1fr; } }
.diff-card{
  background:var(--card);
  border-radius:16px;
  box-shadow:var(--shadow);
  border:1px solid var(--line);
  overflow:hidden;
}
.diff-card h3{
  margin:0;
  padding:14px 18px;
  font-size:15px;
  color:#fff;
  display:flex; align-items:center; gap:8px;
}
.diff-card.extent h3{ background:linear-gradient(100deg,var(--kharif),#166a3c); }
.diff-card.farmer h3{ background:linear-gradient(100deg,#2563a8,#1a3e72); }
.diff-card table{ min-width:0; font-size:13px; }
.diff-card td, .diff-card th{ padding:9px 10px; }
.diff-card thead th{ background:#f4ead3; color:var(--soil-dark); top:0; }
.pos{ color:var(--pos); font-weight:700; }
.neg{ color:var(--neg); font-weight:700; }
.rabi-block thead th{ background:#fbe3c4; }

.summary-note{
  margin-top:16px;
  background:var(--wheat);
  border-left:4px solid var(--rabi);
  padding:12px 16px;
  border-radius:8px;
  font-size:13.5px;
  color:var(--soil-dark);
}
.legend{
  display:flex; gap:16px; margin:10px 2px 18px; flex-wrap:wrap; font-size:12.5px; color:#7a7060; font-weight:600;
}
.legend span{ display:inline-flex; align-items:center; gap:6px; }
.dot{ width:10px; height:10px; border-radius:3px; display:inline-block; }
.dot.k{background:var(--kharif);}
.dot.r{background:var(--rabi);}
.dot.y{background:#FFF2CC; border:1px solid #d8c98a;}

footer{
  text-align:center;
  color:#a89a80;
  font-size:12px;
  padding:20px;
}
</style>
</head>
<body>

<header class="top">
  <div class="eyebrow">Department of Agriculture · Andhra Pradesh</div>
  <h1>Season-Wise Cropping Extent &amp; Farmer Coverage Dashboard</h1>
  <p>Consolidated district-level data across eight consecutive seasons, from Kharif 2022 through Rabi 2025-2026, with year-on-year difference analysis for extent (acres) and farmer participation.</p>
  <div class="season-strip">
    <span class="season-chip k">Kharif 2022</span><span class="season-chip r">Rabi 2022-23</span>
    <span class="season-chip k">Kharif 2023</span><span class="season-chip r">Rabi 2023-24</span>
    <span class="season-chip k">Kharif 2024</span><span class="season-chip r">Rabi 2024-25</span>
    <span class="season-chip k">Kharif 2025</span><span class="season-chip r">Rabi 2025-26</span>
  </div>
</header>

<nav class="tabs">
  <button class="tab-btn active" data-tab="summary" id="btnSummary">📊 Season-Wise Summary</button>
  <button class="tab-btn" data-tab="diff" id="btnDiff">📈 Extent &amp; Farmer Difference Analysis</button>
</nav>

<main>

  <!-- ============ PANEL 1: SUMMARY ============ -->
  <section class="panel active" id="panel-summary">
    <div class="controls-card">
      <div class="control-group" style="flex:2;">
        <label for="districtSelect">Select District</label>
        <select id="districtSelect" onchange="filterDistrict()"></select>
      </div>
      <div class="hint-pill">Showing extent (acres) &amp; farmer counts for every season, Kharif 2022 → Rabi 2025-26</div>
    </div>

    <div class="legend">
      <span><i class="dot k"></i> Kharif season</span>
      <span><i class="dot r"></i> Rabi season</span>
      <span><i class="dot y"></i> Most recent season (Rabi 2025-26)</span>
    </div>

    <div class="table-card">
      <table id="summaryTable">
        <thead>
          <tr>
            <th rowspan="2" class="snhdr">S.No</th>
            <th rowspan="2" class="snhdr">District</th>
            <th colspan="2" class="kharif-header">Kharif 2022</th>
            <th colspan="2" class="rabi-header">Rabi 2022-2023</th>
            <th colspan="2" class="kharif-header">Kharif 2023</th>
            <th colspan="2" class="rabi-header">Rabi 2023-2024</th>
            <th colspan="2" class="kharif-header">Kharif 2024</th>
            <th colspan="2" class="rabi-header">Rabi 2024-2025</th>
            <th colspan="2" class="kharif-header">Kharif 2025</th>
            <th colspan="2" class="rabi-header">Rabi 2025-2026</th>
          </tr>
          <tr>
            <th class="kharif-sub">Extent (Ac)</th><th class="kharif-sub">Farmers</th>
            <th class="rabi-sub">Extent (Ac)</th><th class="rabi-sub">Farmers</th>
            <th class="kharif-sub">Extent (Ac)</th><th class="kharif-sub">Farmers</th>
            <th class="rabi-sub">Extent (Ac)</th><th class="rabi-sub">Farmers</th>
            <th class="kharif-sub">Extent (Ac)</th><th class="kharif-sub">Farmers</th>
            <th class="rabi-sub">Extent (Ac)</th><th class="rabi-sub">Farmers</th>
            <th class="kharif-sub">Extent (Ac)</th><th class="kharif-sub">Farmers</th>
            <th class="rabi-sub">Extent (Ac)</th><th class="rabi-sub">Farmers</th>
          </tr>
        </thead>
        <tbody id="summaryBody"></tbody>
        <tfoot id="summaryFoot"></tfoot>
      </table>
    </div>
  </section>

  <!-- ============ PANEL 2: DIFFERENCE ANALYSIS ============ -->
  <section class="panel" id="panel-diff">
    <div class="controls-card">
      <div class="control-group">
        <label for="diffDistrictSelect">Select District</label>
        <select id="diffDistrictSelect" onchange="renderDiff()"></select>
      </div>
      <div class="hint-pill" id="diffHint">Extent &amp; farmer change (%) across seasons for the selected district</div>
    </div>

    <div class="diff-grid">
      <div class="diff-card extent">
        <h3>🌾 Extent Difference (Acres)</h3>
        <div style="overflow-x:auto;">
        <table id="extentKharifTable">
          <thead><tr>
            <th>Kharif 2022</th><th>Kharif 2023</th><th>Change %</th>
            <th>Kharif 2024</th><th>Change %</th><th>Kharif 2025</th><th>Change %</th>
          </tr></thead>
          <tbody></tbody>
        </table>
        </div>
        <div style="overflow-x:auto;" class="rabi-block">
        <table id="extentRabiTable">
          <thead><tr>
            <th>Rabi 2024-25</th><th>Rabi 2025-26</th><th>Change %</th>
          </tr></thead>
          <tbody></tbody>
        </table>
        </div>
      </div>

      <div class="diff-card farmer">
        <h3>👨‍🌾 Farmer Difference (Count)</h3>
        <div style="overflow-x:auto;">
        <table id="farmerKharifTable">
          <thead><tr>
            <th>Kharif 2022</th><th>Kharif 2023</th><th>Change %</th>
            <th>Kharif 2024</th><th>Change %</th><th>Kharif 2025</th><th>Change %</th>
          </tr></thead>
          <tbody></tbody>
        </table>
        </div>
        <div style="overflow-x:auto;" class="rabi-block">
        <table id="farmerRabiTable">
          <thead><tr>
            <th>Rabi 2024-25</th><th>Rabi 2025-26</th><th>Change %</th>
          </tr></thead>
          <tbody></tbody>
        </table>
        </div>
      </div>
    </div>

    <div class="summary-note" id="diffNote"></div>
  </section>

</main>

<footer>Andhra Pradesh Agriculture Season Dashboard · Data: Kharif 2022 – Rabi 2025-2026</footer>

<script>
/* =========================================================
   DATA
   Each row: [no, name,
     k22Ext,k22Farm, r2223Ext,r2223Farm,
     k23Ext,k23Farm, r2324Ext,r2324Farm,
     k24Ext,k24Farm, r2425Ext,r2425Farm,
     k25Ext,k25Farm, r2526Ext,r2526Farm]
   ========================================================= */
const DATA = [
[1,"ALLURI SITHARAMA RAJU",108820,192795,41103.45,20580,293604.45,113723,37657.02,19241,306876.32,130741,41053.19,19886,442938.31,179640,70600.85,37815],
[2,"ANAKAPALLI",202354,180777,40546.89,40825,249810.26,186503,39888.96,29204,281092.37,228511,40730.29,31017,353068.55,297354,95146.14,110032],
[3,"ANANTAPUR",319522,943472,265497,73109,991902.7,292230,211922.1,55974,1053838,312254,205923.9,53675,1181654,335656,393966.69,113390],
[4,"ANNAMAYYA",116095,100187,54245.53,39948,204650.6,109356,53756.64,32061,200556.7,108965,125000.6,56465,242696.1,119683,123743.73,73100],
[5,"BAPATLA",266064,132713,298389.49,127893,261805.1,122567,292329.3,111694,267656,128725,321095.9,124770,356725.4,187923,475121.93,234887],
[6,"CHITTOOR",183939,175112,47516.96,48695,246390.1,144824,56821.62,43391,256375.1,150545,70309.12,43701,330221.1,194081,100062.34,87168],
[7,"DR. B.R. AMBEDKAR K",138782,90012,173236.2,100145,261098,160265,173259.1,98128,262425.4,158490,166819.2,93230,287568.9,210025,190017.35,125411],
[8,"EAST GODAVARI",192120,95376,177090.33,72675,323256,112404,181627.5,69160,332105.5,112817,184162.9,67039,382338,144402,261088.18,115809],
[9,"ELURU",250458,120426,227607.80,85509,483109.2,135202,206568.3,67313,490262.7,134532,200342.1,64778,547634.8,165124,333458.36,137039],
[10,"GUNTUR",228153,119208,146587.98,60794,235904.3,99709,157227.4,58929,224813.3,91300,178578,68519,262293.6,124589,249181.42,122659],
[11,"KAKINADA",231457,160716,182396.08,105511,307747.7,158182,181354.8,100087,324013.5,170338,184882.5,101827,386234,244349,239017.12,160526],
[12,"KRISHNA",401317,178244,312433.29,115341,412910,162688,301637,106367,417877.7,174791,316910.8,129370,449281.6,202297,408203.81,209607],
[13,"KURNOOL",903597,350769,214037.73,75077,1017399,384198,233270.9,74088,1054950,389639,214520.3,71593,1150305,402774,433686.46,156443],
[14,"NANDYAL",525351,219310,398835.42,133464,551791.9,192526,339638.8,97134,576710.7,196916,319253.4,112840,759878,260391,755381.15,241133],
[15,"NTR",232797,107724,79742.40,27756,313144.3,119355,49853.91,15972,322328.6,124919,85895.86,28654,424763.5,169940,185275.41,73670],
[16,"PALNADU",395516,209126,111356.43,43920,375299,178426,97360.24,32310,435511.2,191312,159205.7,50656,691422.4,299448,331457.42,139510],
[17,"PARVATHIPURAM",212252,118632,45910.19,24387,302323.9,127888,31637.59,11680,309458.5,131152,37821.69,14203,356892,154565,77498.4,51777],
[18,"PRAKASAM",347243,160028,332266.43,130199,353677.9,146924,301217,95446,393489.9,152790,294507,95238,512084.7,205979,495408.96,194248],
[19,"S.P.S.R NELLORE",92247,30023,345533.12,97803,177140.5,50247,297084.4,74412,126828.9,37573,338035.2,89461,293163.3,94089,478381.87,156354],
[20,"SRIKAKULAM",670927,341848,84156.56,42278,467875.5,318338,131297.1,80739,475490.2,336335,128988.8,79837,567550.4,427138,246914.58,226172],
[21,"SRI SATYASAI",402858,298835,173389.57,163703,424524.5,186099,70482.6,34641,513129,219529,83144.88,36380,538596.3,216000,152158.88,71933],
[22,"TIRUPATI",82019,45059,201343.63,77569,144828.7,58782,202869.1,72033,135476.4,52674,203394.3,70548,180746.4,85226,312224.06,141199],
[23,"VISAKHAPATNAM",13069,12063,4558.88,3776,22220.29,15450,4495.82,2763,21761.52,18354,4337.31,3091,24881.91,21587,7189.31,8756],
[24,"VIZIANAGARAM",272650,231021,131495.33,105230,361200.4,222641,96869.07,52664,364570.4,212040,102868.6,60067,477427.1,341750,233295.1,218227],
[25,"WEST GODAVARI",197825,105109,213885.16,104039,230445.1,109198,222686.9,104028,226613.2,103927,221340.6,99726,248462.5,127213,238354,124413],
[26,"Y.S.R",231362,100899,293844.59,100285,303146.14,118505,316180.08,102691,303539.35,117952,306247.41,89524,289862.59,119962,472220.96,167016]
];

const TOTALS = {
  k22Ext:7905169, k22Farm:4133147, r2223Ext:4597017, r2223Farm:2020511,
  k23Ext:9317186.71, k23Farm:4026230, r2324Ext:4288992.62, r2324Farm:1642150,
  k24Ext:9678650.64, k24Farm:4187121, r2425Ext:4607369.66, r2425Farm:1756095,
  k25Ext:11738735.44, k25Farm:5331725, r2526Ext:7359054.48, r2526Farm:3498294
};

const FIELDS = ["no","name","k22Ext","k22Farm","r2223Ext","r2223Farm","k23Ext","k23Farm",
  "r2324Ext","r2324Farm","k24Ext","k24Farm","r2425Ext","r2425Farm","k25Ext","k25Farm","r2526Ext","r2526Farm"];

const ROWS = DATA.map(r=>{
  const o={};
  FIELDS.forEach((f,i)=>o[f]=r[i]);
  return o;
});

/* ===== helpers ===== */
function fmt(n){
  if(n===undefined||n===null||isNaN(n)) return "-";
  return Number(n).toLocaleString('en-IN',{maximumFractionDigits:2});
}
function pctChange(oldV,newV){
  if(!oldV) return null;
  return ((newV-oldV)/oldV)*100;
}
function pctCell(p){
  if(p===null) return '<td>-</td>';
  const cls = p<0 ? 'neg':'pos';
  const sign = p>0 ? '+':'';
  return `<td class="${cls}">${sign}${p.toFixed(2)}%</td>`;
}

/* =========================================================
   PANEL 1: SUMMARY TABLE
   ========================================================= */
function buildDistrictOptions(){
  const opts = ['<option value="ALL">All Districts</option>']
    .concat(ROWS.map(r=>`<option value="${r.name}">${r.name}</option>`));
  document.getElementById('districtSelect').innerHTML = opts.join('');
  document.getElementById('diffDistrictSelect').innerHTML =
    '<option value="ALL">All Districts (State Total)</option>' +
    ROWS.map(r=>`<option value="${r.name}">${r.name}</option>`).join('');
}

function buildSummaryTable(){
  const body = ROWS.map(r=>`
    <tr data-district="${r.name}">
      <td>${r.no}</td>
      <td class="district-cell">${r.name}</td>
      <td>${fmt(r.k22Ext)}</td><td>${fmt(r.k22Farm)}</td>
      <td>${fmt(r.r2223Ext)}</td><td>${fmt(r.r2223Farm)}</td>
      <td>${fmt(r.k23Ext)}</td><td>${fmt(r.k23Farm)}</td>
      <td>${fmt(r.r2324Ext)}</td><td>${fmt(r.r2324Farm)}</td>
      <td>${fmt(r.k24Ext)}</td><td>${fmt(r.k24Farm)}</td>
      <td>${fmt(r.r2425Ext)}</td><td>${fmt(r.r2425Farm)}</td>
      <td>${fmt(r.k25Ext)}</td><td>${fmt(r.k25Farm)}</td>
      <td class="hl">${fmt(r.r2526Ext)}</td><td class="hl">${fmt(r.r2526Farm)}</td>
    </tr>`).join('');
  document.getElementById('summaryBody').innerHTML = body;

  document.getElementById('summaryFoot').innerHTML = `
    <tr>
      <td colspan="2" class="district-cell">TOTAL</td>
      <td>${fmt(TOTALS.k22Ext)}</td><td>${fmt(TOTALS.k22Farm)}</td>
      <td>${fmt(TOTALS.r2223Ext)}</td><td>${fmt(TOTALS.r2223Farm)}</td>
      <td>${fmt(TOTALS.k23Ext)}</td><td>${fmt(TOTALS.k23Farm)}</td>
      <td>${fmt(TOTALS.r2324Ext)}</td><td>${fmt(TOTALS.r2324Farm)}</td>
      <td>${fmt(TOTALS.k24Ext)}</td><td>${fmt(TOTALS.k24Farm)}</td>
      <td>${fmt(TOTALS.r2425Ext)}</td><td>${fmt(TOTALS.r2425Farm)}</td>
      <td>${fmt(TOTALS.k25Ext)}</td><td>${fmt(TOTALS.k25Farm)}</td>
      <td>${fmt(TOTALS.r2526Ext)}</td><td>${fmt(TOTALS.r2526Farm)}</td>
    </tr>`;
}

function filterDistrict(){
  const value = document.getElementById('districtSelect').value;
  document.querySelectorAll('#summaryBody tr').forEach(row=>{
    row.style.display = (value==="ALL" || row.dataset.district===value) ? "" : "none";
  });
  document.getElementById('summaryFoot').style.display = (value==="ALL") ? "" : "none";
}

/* =========================================================
   PANEL 2: DIFFERENCE ANALYSIS
   ========================================================= */
function renderDiff(){
  const value = document.getElementById('diffDistrictSelect').value;
  let d;
  if(value==="ALL"){
    d = TOTALS;
  } else {
    d = ROWS.find(r=>r.name===value);
  }

  // Extent - Kharif
  const chg23 = pctChange(d.k22Ext, d.k23Ext);
  const chg24 = pctChange(d.k23Ext, d.k24Ext);
  const chg25 = pctChange(d.k24Ext, d.k25Ext);
  document.querySelector('#extentKharifTable tbody').innerHTML = `<tr>
    <td>${fmt(d.k22Ext)}</td><td>${fmt(d.k23Ext)}</td>${pctCell(chg23)}
    <td>${fmt(d.k24Ext)}</td>${pctCell(chg24)}<td>${fmt(d.k25Ext)}</td>${pctCell(chg25)}
  </tr>`;
  // Extent - Rabi
  const chgRabiE = pctChange(d.r2425Ext, d.r2526Ext);
  document.querySelector('#extentRabiTable tbody').innerHTML = `<tr>
    <td>${fmt(d.r2425Ext)}</td><td class="hl">${fmt(d.r2526Ext)}</td>${pctCell(chgRabiE)}
  </tr>`;

  // Farmers - Kharif
  const fchg23 = pctChange(d.k22Farm, d.k23Farm);
  const fchg24 = pctChange(d.k23Farm, d.k24Farm);
  const fchg25 = pctChange(d.k24Farm, d.k25Farm);
  document.querySelector('#farmerKharifTable tbody').innerHTML = `<tr>
    <td>${fmt(d.k22Farm)}</td><td>${fmt(d.k23Farm)}</td>${pctCell(fchg23)}
    <td>${fmt(d.k24Farm)}</td>${pctCell(fchg24)}<td>${fmt(d.k25Farm)}</td>${pctCell(fchg25)}
  </tr>`;
  // Farmers - Rabi
  const fchgRabi = pctChange(d.r2425Farm, d.r2526Farm);
  document.querySelector('#farmerRabiTable tbody').innerHTML = `<tr>
    <td>${fmt(d.r2425Farm)}</td><td class="hl">${fmt(d.r2526Farm)}</td>${pctCell(fchgRabi)}
  </tr>`;

  document.getElementById('diffHint').textContent =
    `Showing change data for: ${value==="ALL" ? "All Districts (State Total)" : value}`;

  const overallExtTrend = chgRabiE!==null && chgRabiE>=0 ? "increased" : "decreased";
  const overallFarmTrend = fchgRabi!==null && fchgRabi>=0 ? "increased" : "decreased";
  document.getElementById('diffNote').innerHTML =
    `<strong>${value==="ALL" ? "State-wide" : value}:</strong> Rabi cropping extent has ${overallExtTrend}
     by <strong>${chgRabiE===null?"-":Math.abs(chgRabiE).toFixed(2)+"%"}</strong> and farmer participation has ${overallFarmTrend}
     by <strong>${fchgRabi===null?"-":Math.abs(fchgRabi).toFixed(2)+"%"}</strong> in Rabi 2025-26 compared to Rabi 2024-25.`;
}

/* =========================================================
   TAB SWITCHING
   ========================================================= */
document.getElementById('btnSummary').addEventListener('click', ()=>switchTab('summary'));
document.getElementById('btnDiff').addEventListener('click', ()=>switchTab('diff'));

function switchTab(tab){
  document.querySelectorAll('.tab-btn').forEach(b=>{b.classList.remove('active','rabi-active');});
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
  document.getElementById('panel-'+tab).classList.add('active');
  if(tab==='summary'){
    document.getElementById('btnSummary').classList.add('active');
  } else {
    document.getElementById('btnDiff').classList.add('active','rabi-active');
  }
}

/* ===== INIT ===== */
buildDistrictOptions();
buildSummaryTable();
filterDistrict();
renderDiff();
</script>
</body>
</html>
