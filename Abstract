<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Agriculture District / Year / Season Dashboard</title>
<style>
body {
    font-family: "Segoe UI", Arial, sans-serif;
    background: #eef2f6;
    margin: 20px;
    color: #2c3e50;
}
h1 {
    text-align: center;
    margin-bottom: 6px;
    font-weight: 800;
    font-size: 26px;
    color: #1a3e72;
}
h2 {
    text-align: center;
    color: #1a3e72;
    margin: 34px 0 14px;
    font-size: 20px;
}
.subtitle {
    text-align: center;
    color: #5b6b7d;
    margin-bottom: 20px;
    font-size: 14px;
}
.controls {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 24px;
    margin: 18px auto 26px;
}
.control-box {
    width: 280px;
    text-align: center;
}
.select-label {
    font-weight: 700;
    font-size: 14px;
    color: #1a3e72;
    margin-bottom: 8px;
    display: block;
}
.custom-select {
    width: 100%;
    padding: 10px 14px;
    border-radius: 12px;
    border: 2px solid #1a3e72;
    background: #ffffff;
    font-size: 14px;
    font-weight: 600;
    color: #1a3e72;
    cursor: pointer;
    appearance: none;
    background-image: url("data:image/svg+xml;utf8,<svg fill='%231a3e72' height='24' viewBox='0 0 24 24' width='24' xmlns='http://www.w3.org/2000/svg'><path d='M7 10l5 5 5-5z'/></svg>");
    background-repeat: no-repeat;
    background-position: right 12px center;
    transition: 0.2s;
}
.custom-select:hover { border-color: #2563eb; box-shadow: 0 0 8px rgba(37,99,235,0.35); }
.custom-select:disabled { opacity: 0.5; cursor: not-allowed; }

.table-container { width: 98%; margin: auto; overflow-x: auto; padding-bottom: 10px; }
table {
    width: 100%;
    border-collapse: collapse;
    background: #ffffff;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 3px 12px rgba(0,0,0,0.15);
    margin-bottom: 10px;
}
thead th { position: sticky; top: 0; z-index: 5; }
th { padding: 9px; font-size: 12.5px; text-align: center; border: 1px solid #c7c7c7; font-weight: 700; }
td { border: 1px solid #d8d8d8; padding: 7px 9px; font-size: 12.5px; text-align: right; }
td.left { text-align: left; padding-left: 14px; font-weight: bold; color: #1e2a38; }
tbody tr:nth-child(even) { background-color: #f7f9fc; }
tbody tr:hover { background-color: #dceeff; }
tfoot tr { background-color: #1a3b67; color: #fff; font-size: 13.5px; font-weight: 700; }
tfoot td.left { color: #fff; }

.kharif-header { background: #1f8f4e; color: #fff; }
.kharif-sub { background: #34c86c !important; color: #fff; }
.rabi-header { background: #d35400; color: #fff; }
.rabi-sub { background: #f39c12 !important; color: #fff; }
.highlight-col { background-color: #fff2cc !important; font-weight: bold; }
.negative { color: #d32f2f; font-weight: bold; }
.positive { color: #1b7f3b; font-weight: bold; }

.section { display: none; }
.section.active { display: block; }
.hint {
    text-align: center;
    color: #7a8a9a;
    font-size: 13px;
    margin: 6px 0 20px;
    font-style: italic;
}
.back-btn {
    display: block;
    margin: 10px auto 0;
    padding: 8px 18px;
    border-radius: 8px;
    border: none;
    background: linear-gradient(90deg,#ff6a00,#2563eb);
    color: #fff;
    font-weight: 700;
    cursor: pointer;
}
</style>
</head>
<body>

<h1>Agriculture District / Year / Season Wise Dashboard</h1>
<div class="subtitle">Combined Booking Summary + Extent (Acres) &amp; Farmer Count Year-wise / Season-wise Difference Analysis</div>

<div class="controls">
    <div class="control-box">
        <label class="select-label" for="districtSelect">Select District</label>
        <select id="districtSelect" class="custom-select" onchange="render()">
            <option value="ALL">-- All Districts --</option>
        </select>
    </div>
    <div class="control-box">
        <label class="select-label" for="compareSelect">Compare With Year Wise (%)</label>
        <select id="compareSelect" class="custom-select" onchange="render()">
            <option value="">-- Select --</option>
            <option value="extent">Extent % Difference</option>
            <option value="farmer">Farmer % Difference</option>
        </select>
    </div>
</div>

<!-- ================= SECTION 1: MAIN ABSTRACT SUMMARY ================= -->
<h2>District / Year / Season Wise Abstract (Extent &amp; Farmers)</h2>
<div class="table-container">
<table id="summaryTable">
    <thead>
        <tr>
            <th rowspan="2">S.No</th>
            <th rowspan="2">District</th>
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
            <th class="kharif-sub">Extent (Acres)</th><th class="kharif-sub">Farmers</th>
            <th class="rabi-sub">Extent (Acres)</th><th class="rabi-sub">Farmers</th>
            <th class="kharif-sub">Extent (Acres)</th><th class="kharif-sub">Farmers</th>
            <th class="rabi-sub">Extent (Acres)</th><th class="rabi-sub">Farmers</th>
            <th class="kharif-sub">Extent (Acres)</th><th class="kharif-sub">Farmers</th>
            <th class="rabi-sub">Extent (Acres)</th><th class="rabi-sub">Farmers</th>
            <th class="kharif-sub">Extent (Acres)</th><th class="kharif-sub">Farmers</th>
            <th class="rabi-sub">Extent (Acres)</th><th class="rabi-sub">Farmers</th>
        </tr>
    </thead>
    <tbody id="summaryBody"></tbody>
    <tfoot id="summaryFoot"></tfoot>
</table>
</div>
<div class="hint">Tip: choose a district above to view only that district's abstract, or keep "All Districts" to see everything.</div>

<!-- ================= SECTION 2: EXTENT DIFFERENCE ================= -->
<div id="extentSection" class="section">
<h2>Kharif Extent (Acres) &ndash; Year Wise % Change</h2>
<div class="table-container">
<table id="extentKharifTable">
    <thead>
        <tr>
            <th>S.No</th><th>District</th>
            <th>Kharif 2022 Extent</th>
            <th>Kharif 2023 Extent</th><th>Change % (2023 vs 2022)</th>
            <th>Kharif 2024 Extent</th><th>Change % (2024 vs 2023)</th>
            <th>Kharif 2025 Extent</th><th>Change % (2025 vs 2024)</th>
        </tr>
    </thead>
    <tbody id="extentKharifBody"></tbody>
    <tfoot id="extentKharifFoot"></tfoot>
</table>
</div>

<h2>Rabi Extent (Acres) &ndash; 2025-26 vs 2024-25 % Change</h2>
<div class="table-container">
<table id="extentRabiTable">
    <thead>
        <tr>
            <th>S.No</th><th>District</th>
            <th>Rabi 2024-2025 Extent</th>
            <th>Rabi 2025-2026 Extent</th>
            <th>Change % (2025-26 vs 2024-25)</th>
        </tr>
    </thead>
    <tbody id="extentRabiBody"></tbody>
    <tfoot id="extentRabiFoot"></tfoot>
</table>
</div>
</div>

<!-- ================= SECTION 3: FARMER DIFFERENCE ================= -->
<div id="farmerSection" class="section">
<h2>Kharif Farmer Count &ndash; Year Wise % Change</h2>
<div class="table-container">
<table id="farmerKharifTable">
    <thead>
        <tr>
            <th>S.No</th><th>District</th>
            <th>Kharif 2022 Farmers</th>
            <th>Kharif 2023 Farmers</th><th>Change % (2023 vs 2022)</th>
            <th>Kharif 2024 Farmers</th><th>Change % (2024 vs 2023)</th>
            <th>Kharif 2025 Farmers</th><th>Change % (2025 vs 2024)</th>
        </tr>
    </thead>
    <tbody id="farmerKharifBody"></tbody>
    <tfoot id="farmerKharifFoot"></tfoot>
</table>
</div>

<h2>Rabi Farmer Count &ndash; 2025-26 vs 2024-25 % Change</h2>
<div class="table-container">
<table id="farmerRabiTable">
    <thead>
        <tr>
            <th>S.No</th><th>District</th>
            <th>Rabi 2024-2025 Farmers</th>
            <th>Rabi 2025-2026 Farmers</th>
            <th>Change % (2025-26 vs 2024-25)</th>
        </tr>
    </thead>
    <tbody id="farmerRabiBody"></tbody>
    <tfoot id="farmerRabiFoot"></tfoot>
</table>
</div>
</div>

<button class="back-btn" onclick="history.back()">Back</button>

<script>
/* =====================================================================
   MASTER DATA
   Order: [K2022E,K2022F, R2223E,R2223F, K2023E,K2023F, R2324E,R2324F,
           K2024E,K2024F, R2425E,R2425F, K2025E,K2025F, R2526E,R2526F]
   ===================================================================== */
const districts = [
"ALLURI SITHARAMA RAJU","ANAKAPALLI","ANANTAPUR","ANNAMAYYA","BAPATLA","CHITTOOR",
"DR. B.R. AMBEDKAR K","EAST GODAVARI","ELURU","GUNTUR","KAKINADA","KRISHNA","KURNOOL",
"NANDYAL","NTR","PALNADU","PARVATHIPURAM","PRAKASAM","S.P.S.R NELLORE","SRIKAKULAM",
"SRI SATYASAI","TIRUPATI","VISAKHAPATNAM","VIZIANAGARAM","WEST GODAVARI","Y.S.R"
];

const summary = [
[108820,192795,41103.45,20580,293604.45,113723,37657.02,19241,306876.32,130741,41053.19,19886,442938.31,179640,70600.85,37815],
[202354,180777,40546.89,40825,249810.26,186503,39888.96,29204,281092.37,228511,40730.29,31017,353068.55,297354,95146.14,110032],
[319522,943472,265497,73109,991902.7,292230,211922.1,55974,1053838,312254,205923.9,53675,1181654,335656,393966.69,113390],
[116095,100187,54245.53,39948,204650.6,109356,53756.64,32061,200556.7,108965,125000.6,56465,242696.1,119683,123743.73,73100],
[266064,132713,298389.49,127893,261805.1,122567,292329.3,111694,267656,128725,321095.9,124770,356725.4,187923,475121.93,234887],
[183939,175112,47516.96,48695,246390.1,144824,56821.62,43391,256375.1,150545,70309.12,43701,330221.1,194081,100062.34,87168],
[138782,90012,173236.2,100145,261098,160265,173259.1,98128,262425.4,158490,166819.2,93230,287568.9,210025,190017.35,125411],
[192120,95376,177090.33,72675,323256,112404,181627.5,69160,332105.5,112817,184162.9,67039,382338,144402,261088.18,115809],
[250458,120426,227607.80,85509,483109.2,135202,206568.3,67313,490262.7,134532,200342.1,64778,547634.8,165124,333458.36,137039],
[228153,119208,146587.98,60794,235904.3,99709,157227.4,58929,224813.3,91300,178578,68519,262293.6,124589,249181.42,122659],
[231457,160716,182396.08,105511,307747.7,158182,181354.8,100087,324013.5,170338,184882.5,101827,386234,244349,239017.12,160526],
[401317,178244,312433.29,115341,412910,162688,301637,106367,417877.7,174791,316910.8,129370,449281.6,202297,408203.81,209607],
[903597,350769,214037.73,75077,1017399,384198,233270.9,74088,1054950,389639,214520.3,71593,1150305,402774,433686.46,156443],
[525351,219310,398835.42,133464,551791.9,192526,339638.8,97134,576710.7,196916,319253.4,112840,759878,260391,755381.15,241133],
[232797,107724,79742.40,27756,313144.3,119355,49853.91,15972,322328.6,124919,85895.86,28654,424763.5,169940,185275.41,73670],
[395516,209126,111356.43,43920,375299,178426,97360.24,32310,435511.2,191312,159205.7,50656,691422.4,299448,331457.42,139510],
[212252,118632,45910.19,24387,302323.9,127888,31637.59,11680,309458.5,131152,37821.69,14203,356892,154565,77498.4,51777],
[347243,160028,332266.43,130199,353677.9,146924,301217,95446,393489.9,152790,294507,95238,512084.7,205979,495408.96,194248],
[92247,30023,345533.12,97803,177140.5,50247,297084.4,74412,126828.9,37573,338035.2,89461,293163.3,94089,478381.87,156354],
[670927,341848,84156.56,42278,467875.5,318338,131297.1,80739,475490.2,336335,128988.8,79837,567550.4,427138,246914.58,226172],
[402858,298835,173389.57,163703,424524.5,186099,70482.6,34641,513129,219529,83144.88,36380,538596.3,216000,152158.88,71933],
[82019,45059,201343.63,77569,144828.7,58782,202869.1,72033,135476.4,52674,203394.3,70548,180746.4,85226,312224.06,141199],
[13069,12063,4558.88,3776,22220.29,15450,4495.82,2763,21761.52,18354,4337.31,3091,24881.91,21587,7189.31,8756],
[272650,231021,131495.33,105230,361200.4,222641,96869.07,52664,364570.4,212040,102868.6,60067,477427.1,341750,233295.1,218227],
[197825,105109,213885.16,104039,230445.1,109198,222686.9,104028,226613.2,103927,221340.6,99726,248462.5,127213,238354,124413],
[231362,100899,293844.59,100285,303146.14,118505,316180.08,102691,303539.35,117952,306247.41,89524,289862.59,119962,472220.96,167016]
];

const summaryTotal = [7905169,4133147,4597017,2020511,9317186.71,4026230,4288992.62,1642150,9678650.64,4187121,4607369.66,1756095,11738735.44,5331725,7359054.48,3498294];

/* Extent Kharif: [K2022, K2023, pct23v22, K2024, pct24v23, K2025, pct25v24] */
const extentKharif = [
[108820.00,293604.45,169.81,306876.32,4.52,442938.31,44.34],
[202354.00,249810.26,23.45,281092.37,12.52,353068.55,25.61],
[319522.00,991902.70,210.43,1053838.00,6.24,1181654.00,12.13],
[116095.00,204650.60,76.28,200556.70,-2.00,242696.10,21.01],
[266064.00,261805.10,-1.60,267656.00,2.23,356725.40,33.28],
[183939.00,246390.10,33.95,256375.10,4.05,330221.10,28.80],
[138782.00,261098.00,88.14,262425.40,0.51,287568.90,9.58],
[192120.00,323256.00,68.26,332105.50,2.74,382338.00,15.13],
[250458.00,483109.20,92.89,490262.70,1.48,547634.80,11.70],
[228153.00,235904.30,3.40,224813.30,-4.70,262293.60,16.67],
[231457.00,307747.70,32.96,324013.50,5.29,386234.00,19.20],
[401317.00,412910.00,2.89,417877.70,1.20,449281.60,7.52],
[903597.00,1017399.00,12.59,1054950.00,3.69,1150305.00,9.04],
[525351.00,551791.90,5.03,576710.70,4.52,759878.00,31.76],
[232797.00,313144.30,34.51,322328.60,2.93,424763.50,31.78],
[395516.00,375299.00,-5.11,435511.20,16.04,691422.40,58.76],
[212252.00,302323.90,42.44,309458.50,2.36,356892.00,15.33],
[347243.00,353677.90,1.85,393489.90,11.26,512084.70,30.14],
[92247.00,177140.50,92.03,126828.90,-28.40,293163.30,131.15],
[670927.00,467875.50,-30.26,475490.20,1.63,567550.40,19.36],
[402858.00,424524.50,5.38,513129.00,20.87,538596.30,4.96],
[82019.00,144828.70,76.58,135476.40,-6.46,180746.40,33.42],
[13069.00,22220.29,70.02,21761.52,-2.06,24881.91,14.34],
[272650.00,361200.40,32.48,364570.40,0.93,477427.10,30.96],
[197825.00,230445.10,16.49,226613.20,-1.66,248462.50,9.64],
[231362.00,303146.14,31.03,305339.35,0.72,289862.59,-5.07]
];
const extentKharifTotal = [7218794.00,9317205.54,29.07,9679550.46,3.89,11738690.46,21.27];

/* Extent Rabi: [R2425, R2526, pct] */
const extentRabi = [
[41053.19,70600.85,71.97],[40730.29,95146.14,133.60],[205923.90,393966.69,91.32],
[125000.60,123743.73,-1.01],[321095.90,475121.93,47.97],[70309.12,100062.34,42.32],
[166819.20,190017.35,13.91],[184162.90,261088.18,41.77],[200342.10,333458.36,66.44],
[178578.00,249181.42,39.54],[184882.50,239017.12,29.28],[316910.80,408203.81,28.81],
[214520.30,433686.46,102.17],[319253.40,755381.15,136.61],[85895.86,185275.41,115.70],
[159205.70,331457.42,108.19],[37821.69,77498.40,104.90],[294507.00,495408.96,68.22],
[338035.20,478381.87,41.52],[128988.80,246914.58,91.42],[83144.88,152158.88,83.00],
[203394.30,312224.06,53.51],[4337.31,7189.31,65.76],[102868.60,233295.10,126.79],
[221340.60,238354.00,7.69],[306247.41,472220.96,54.20]
];
const extentRabiTotal = [4535369.55,7359054.48,62.26];

/* Farmer Kharif: [K2022, K2023, pct23v22, K2024, pct24v23, K2025, pct25v24] */
const farmerKharif = [
[192795,113723,-41,130741,15,179640,37],
[180777,186503,3,228511,23,297354,30],
[943472,292230,-69,312254,7,335656,7],
[100187,109356,9,108965,-0,119683,10],
[132713,122567,-8,128725,5,187923,46],
[175112,144824,-17,150545,4,194081,29],
[90012,160265,78,158490,-1,210025,33],
[95376,112404,18,112817,0,144402,28],
[120426,135202,12,134532,-0,165124,23],
[119208,99709,-16,91300,-8,124589,36],
[160716,158182,-2,170338,8,244349,43],
[178244,162688,-9,174791,7,202297,16],
[350769,384198,10,389639,1,402774,3],
[219310,192526,-12,196916,2,260391,32],
[107724,119355,11,124919,5,169940,36],
[209126,178426,-15,191312,7,299448,57],
[118632,127888,8,131152,3,154565,18],
[160028,146924,-8,152790,4,205979,35],
[30023,50247,67,37573,-25,94089,150],
[341848,318338,-7,336335,6,427138,27],
[298835,186099,-38,219529,18,216000,-2],
[45059,58782,30,52674,-10,85226,62],
[12063,15450,28,18354,19,21587,18],
[231021,222641,-4,212040,-5,341750,61],
[105109,109198,4,103927,-5,127213,22],
[100899,118505,17,117952,-0,119962,2]
];
const farmerKharifTotal = [4819484,4026230,-16,4187121,4,5331185,27];

/* Farmer Rabi: [R2425, R2526, pct] */
const farmerRabi = [
[19886,37815,90],[31017,110032,255],[53675,113390,111],[56465,73100,29],
[124770,234887,88],[43701,87168,99],[93230,125411,35],[67039,115809,73],
[64778,137039,112],[68519,122659,79],[101827,160526,58],[129370,209607,62],
[71593,156443,119],[112840,241133,114],[28654,73670,157],[50656,139510,175],
[14203,51777,265],[95238,194248,104],[89461,156354,75],[79837,226172,183],
[36380,71933,98],[70548,141199,100],[3091,8756,183],[60067,218227,263],
[99726,124413,25],[89524,167016,87]
];
const farmerRabiTotal = [1756095,3498294,99];

/* =====================================================================
   HELPERS
   ===================================================================== */
function fmt(n) {
    if (n === undefined || n === null || isNaN(n)) return "-";
    return Number(n).toLocaleString('en-IN', {maximumFractionDigits:2, minimumFractionDigits: (n % 1 !== 0 ? 2 : 0)});
}
function pctSpan(p) {
    const cls = p < 0 ? "negative" : "positive";
    const sign = p > 0 ? "+" : "";
    return `<span class="${cls}">${sign}${p.toFixed(2)} %</span>`;
}
function pctSpanInt(p) {
    const cls = p < 0 ? "negative" : "positive";
    const sign = p > 0 ? "+" : "";
    return `<span class="${cls}">${sign}${p} %</span>`;
}

function populateDistrictSelect() {
    const sel = document.getElementById("districtSelect");
    districts.forEach(d => {
        const opt = document.createElement("option");
        opt.value = d; opt.textContent = d;
        sel.appendChild(opt);
    });
}

function getSelectedIndexes() {
    const value = document.getElementById("districtSelect").value;
    if (value === "ALL") return districts.map((d,i)=>i);
    const idx = districts.indexOf(value);
    return idx === -1 ? [] : [idx];
}

/* =====================================================================
   RENDER: SUMMARY TABLE
   ===================================================================== */
function renderSummary(indexes) {
    const body = document.getElementById("summaryBody");
    const foot = document.getElementById("summaryFoot");
    body.innerHTML = "";
    indexes.forEach((i, order) => {
        const r = summary[i];
        const tr = document.createElement("tr");
        let cells = `<td>${order+1}</td><td class="left">${districts[i]}</td>`;
        for (let c = 0; c < r.length; c++) {
            const isExtentCol = (c % 2 === 0); // extent columns
            cells += `<td class="${isExtentCol ? 'highlight-col':''}">${fmt(r[c])}</td>`;
        }
        tr.innerHTML = cells;
        body.appendChild(tr);
    });

    if (indexes.length === districts.length) {
        foot.innerHTML = `<tr><td colspan="2" class="left">TOTAL</td>${summaryTotal.map(v=>`<td>${fmt(v)}</td>`).join("")}</tr>`;
    } else {
        foot.innerHTML = "";
    }
}

/* =====================================================================
   RENDER: EXTENT DIFFERENCE
   ===================================================================== */
function renderExtent(indexes) {
    const kBody = document.getElementById("extentKharifBody");
    const kFoot = document.getElementById("extentKharifFoot");
    kBody.innerHTML = "";
    indexes.forEach((i, order) => {
        const r = extentKharif[i];
        kBody.innerHTML += `<tr>
            <td>${order+1}</td><td class="left">${districts[i]}</td>
            <td>${fmt(r[0])}</td>
            <td class="highlight-col">${fmt(r[1])}</td><td>${pctSpan(r[2])}</td>
            <td>${fmt(r[3])}</td><td>${pctSpan(r[4])}</td>
            <td class="highlight-col">${fmt(r[5])}</td><td>${pctSpan(r[6])}</td>
        </tr>`;
    });
    kFoot.innerHTML = indexes.length === districts.length
        ? `<tr><td colspan="2" class="left">Grand Total</td>
             <td>${fmt(extentKharifTotal[0])}</td>
             <td>${fmt(extentKharifTotal[1])}</td><td>${pctSpan(extentKharifTotal[2])}</td>
             <td>${fmt(extentKharifTotal[3])}</td><td>${pctSpan(extentKharifTotal[4])}</td>
             <td>${fmt(extentKharifTotal[5])}</td><td>${pctSpan(extentKharifTotal[6])}</td></tr>`
        : "";

    const rBody = document.getElementById("extentRabiBody");
    const rFoot = document.getElementById("extentRabiFoot");
    rBody.innerHTML = "";
    indexes.forEach((i, order) => {
        const r = extentRabi[i];
        rBody.innerHTML += `<tr>
            <td>${order+1}</td><td class="left">${districts[i]}</td>
            <td>${fmt(r[0])}</td><td class="highlight-col">${fmt(r[1])}</td><td>${pctSpan(r[2])}</td>
        </tr>`;
    });
    rFoot.innerHTML = indexes.length === districts.length
        ? `<tr><td colspan="2" class="left">Grand Total</td>
             <td>${fmt(extentRabiTotal[0])}</td><td>${fmt(extentRabiTotal[1])}</td><td>${pctSpan(extentRabiTotal[2])}</td></tr>`
        : "";
}

/* =====================================================================
   RENDER: FARMER DIFFERENCE
   ===================================================================== */
function renderFarmer(indexes) {
    const kBody = document.getElementById("farmerKharifBody");
    const kFoot = document.getElementById("farmerKharifFoot");
    kBody.innerHTML = "";
    indexes.forEach((i, order) => {
        const r = farmerKharif[i];
        kBody.innerHTML += `<tr>
            <td>${order+1}</td><td class="left">${districts[i]}</td>
            <td>${fmt(r[0])}</td>
            <td class="highlight-col">${fmt(r[1])}</td><td>${pctSpanInt(r[2])}</td>
            <td>${fmt(r[3])}</td><td>${pctSpanInt(r[4])}</td>
            <td class="highlight-col">${fmt(r[5])}</td><td>${pctSpanInt(r[6])}</td>
        </tr>`;
    });
    kFoot.innerHTML = indexes.length === districts.length
        ? `<tr><td colspan="2" class="left">Grand Total</td>
             <td>${fmt(farmerKharifTotal[0])}</td>
             <td>${fmt(farmerKharifTotal[1])}</td><td>${pctSpanInt(farmerKharifTotal[2])}</td>
             <td>${fmt(farmerKharifTotal[3])}</td><td>${pctSpanInt(farmerKharifTotal[4])}</td>
             <td>${fmt(farmerKharifTotal[5])}</td><td>${pctSpanInt(farmerKharifTotal[6])}</td></tr>`
        : "";

    const rBody = document.getElementById("farmerRabiBody");
    const rFoot = document.getElementById("farmerRabiFoot");
    rBody.innerHTML = "";
    indexes.forEach((i, order) => {
        const r = farmerRabi[i];
        rBody.innerHTML += `<tr>
            <td>${order+1}</td><td class="left">${districts[i]}</td>
            <td>${fmt(r[0])}</td><td class="highlight-col">${fmt(r[1])}</td><td>${pctSpanInt(r[2])}</td>
        </tr>`;
    });
    rFoot.innerHTML = indexes.length === districts.length
        ? `<tr><td colspan="2" class="left">Grand Total</td>
             <td>${fmt(farmerRabiTotal[0])}</td><td>${fmt(farmerRabiTotal[1])}</td><td>${pctSpanInt(farmerRabiTotal[2])}</td></tr>`
        : "";
}

/* =====================================================================
   MASTER RENDER
   ===================================================================== */
function render() {
    const indexes = getSelectedIndexes();
    renderSummary(indexes);

    const compare = document.getElementById("compareSelect").value;
    const extentSec = document.getElementById("extentSection");
    const farmerSec = document.getElementById("farmerSection");

    extentSec.classList.remove("active");
    farmerSec.classList.remove("active");

    if (compare === "extent") {
        renderExtent(indexes);
        extentSec.classList.add("active");
    } else if (compare === "farmer") {
        renderFarmer(indexes);
        farmerSec.classList.add("active");
    }
}

populateDistrictSelect();
render();
</script>
</body>
</html>
