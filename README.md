index.html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Gen-4 Season 4 — Final Points Standings</title>
  <style>
    :root{--bg:#0f1720;--card:#0b1220;--muted:#9aa4b2;--accent:#ffcc00;--accent2:#4fc3f7}
    html,body{height:100%;margin:0;font-family:Inter,system-ui,Segoe UI,Roboto,Arial;color:#e6eef6;background:linear-gradient(180deg,#071021 0%, #071623 100%);}
    .wrap{max-width:1100px;margin:36px auto;padding:24px}
    header{display:flex;align-items:center;gap:16px}
    .logo{width:64px;height:64px;border-radius:8px;background:linear-gradient(135deg,var(--accent),var(--accent2));display:flex;align-items:center;justify-content:center;font-weight:700}
    h1{margin:0;font-size:1.6rem}
    p.lead{margin:8px 0 18px;color:var(--muted)}

    .controls{display:flex;gap:12px;flex-wrap:wrap;margin-bottom:16px}
    .search{flex:1;min-width:220px}
    input[type="search"], select{width:100%;padding:10px 12px;border-radius:8px;border:1px solid rgba(255,255,255,0.06);background:rgba(255,255,255,0.02);color:inherit}
    button{background:var(--accent);border:none;color:#071021;padding:10px 14px;border-radius:8px;cursor:pointer}

    .card{background:rgba(255,255,255,0.03);border-radius:10px;padding:12px;overflow:auto;box-shadow:0 6px 18px rgba(2,6,23,0.6)}
    table{width:100%;border-collapse:collapse;font-size:0.95rem}
    thead th{position:sticky;top:0;background:linear-gradient(180deg,rgba(0,0,0,0.3),rgba(0,0,0,0.2));backdrop-filter:blur(4px);z-index:2;padding:10px;text-align:left;font-weight:600;color:var(--muted)}
    tbody td{padding:10px;border-top:1px solid rgba(255,255,255,0.03)}
    tbody tr:hover{background:linear-gradient(90deg,rgba(79,195,247,0.03),transparent)}
    .num{font-variant-numeric:tabular-nums;color:#dbe9ff}

    /* highlight top 3 */
    tbody tr[data-pos="1"]{background:linear-gradient(90deg,rgba(255,204,0,0.06),transparent)}
    tbody tr[data-pos="2"]{background:linear-gradient(90deg,rgba(192,192,192,0.04),transparent)}
    tbody tr[data-pos="3"]{background:linear-gradient(90deg,rgba(205,127,50,0.03),transparent)}

    .meta{display:flex;gap:12px;flex-wrap:wrap;margin-top:10px;color:var(--muted);font-size:0.9rem}

    .small{font-size:0.85rem;color:var(--muted)}

    @media (max-width:720px){
      thead th:nth-child(6), tbody td:nth-child(6), thead th:nth-child(7), tbody td:nth-child(7){display:none}
    }
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="logo">G4</div>
      <div>
        <h1>Gen-4 — Season 4 — Final Points Standings</h1>
        <p class="lead">Interactive standings table. Sort, filter, and export the data below.</p>
      </div>
    </header>

    <div class="controls">
      <div class="search">
        <input id="filterInput" type="search" placeholder="Filter by driver name or team — e.g. 'Labonte'" />
      </div>
      <div style="width:170px">
        <select id="sortSelect">
          <option value="pos">Sort: Position</option>
          <option value="pts">Sort: Points (desc)</option>
          <option value="wins">Sort: Wins (desc)</option>
          <option value="top5">Sort: Top 5s (desc)</option>
          <option value="dnfs">Sort: DNF's (asc)</option>
        </select>
      </div>
      <div>
        <button id="exportBtn">Export CSV</button>
      </div>
    </div>

    <div class="card">
      <table id="standingsTable">
        <thead>
          <tr>
            <th>Pos.</th>
            <th>Driver</th>
            <th>Pts</th>
            <th>Pts-</th>
            <th>Wins</th>
            <th class="small">Top 5s</th>
            <th class="small">Top 10s</th>
            <th class="small">Starts</th>
            <th class="small">DNF's</th>
          </tr>
        </thead>
        <tbody>
          <!-- Data rows inserted by script -->
        </tbody>
      </table>
    </div>

    <div class="meta small">Data source: user-provided. Designed for quick reference — click headers in the UI to sort or use the controls above.</div>
  </div>

  <script>
    // Data array derived from the user's table
    const data = [
      {pos:1, driver:'Terry Labonte', pts:501, ptsDiff:null, wins:1, top5:10, top10:14, starts:20, dnfs:0},
      {pos:2, driver:'Jeff Gordon', pts:500, ptsDiff:-1, wins:4, top5:10, top10:13, starts:20, dnfs:2},
      {pos:3, driver:'Dale Jarrett', pts:456, ptsDiff:-45, wins:2, top5:5, top10:12, starts:20, dnfs:3},
      {pos:4, driver:'Dale Earnhardt', pts:454, ptsDiff:-47, wins:2, top5:7, top10:9, starts:20, dnfs:1},
      {pos:5, driver:'Jeff Burton', pts:448, ptsDiff:-53, wins:2, top5:7, top10:9, starts:20, dnfs:2},
      {pos:6, driver:'Bobby Labonte', pts:445, ptsDiff:-56, wins:1, top5:6, top10:11, starts:20, dnfs:1},
      {pos:7, driver:"Dale Earnhardt Jr.", pts:431, ptsDiff:-70, wins:1, top5:7, top10:11, starts:20, dnfs:1},
      {pos:8, driver:'Bill Elliott', pts:417, ptsDiff:-84, wins:0, top5:7, top10:9, starts:20, dnfs:2},
      {pos:9, driver:'Steve Park', pts:391, ptsDiff:-110, wins:2, top5:4, top10:8, starts:20, dnfs:2},
      {pos:10, driver:'Jimmie Johnson', pts:391, ptsDiff:-110, wins:0, top5:5, top10:9, starts:20, dnfs:3},
      {pos:11, driver:'Rusty Wallace', pts:380, ptsDiff:-121, wins:0, top5:3, top10:10, starts:20, dnfs:3},
      {pos:12, driver:'Tony Stewart', pts:366, ptsDiff:-135, wins:2, top5:5, top10:7, starts:17, dnfs:2},
      {pos:13, driver:'Darrell Waltrip', pts:350, ptsDiff:-151, wins:0, top5:4, top10:5, starts:20, dnfs:2},
      {pos:14, driver:'Michael Waltrip', pts:344, ptsDiff:-157, wins:0, top5:3, top10:6, starts:20, dnfs:3},
      {pos:15, driver:'John Andretti', pts:333, ptsDiff:-168, wins:1, top5:3, top10:6, starts:20, dnfs:4},
      {pos:16, driver:'Ricky Craven', pts:332, ptsDiff:-169, wins:0, top5:3, top10:7, starts:19, dnfs:2},
      {pos:17, driver:'Ricky Rudd', pts:326, ptsDiff:-175, wins:1, top5:2, top10:6, starts:20, dnfs:3},
      {pos:18, driver:'Christian Fitipaldi', pts:302, ptsDiff:-199, wins:0, top5:2, top10:2, starts:20, dnfs:3},
      {pos:19, driver:'Mark Martin', pts:293, ptsDiff:-208, wins:1, top5:2, top10:4, starts:20, dnfs:3},
      {pos:20, driver:'Kenny Wallace', pts:292, ptsDiff:-209, wins:0, top5:2, top10:7, starts:18, dnfs:5},
      {pos:21, driver:'Ernie Irvan', pts:288, ptsDiff:-213, wins:0, top5:1, top10:6, starts:20, dnfs:3},
      {pos:22, driver:'Kenny Schrader', pts:288, ptsDiff:-213, wins:0, top5:0, top10:2, starts:20, dnfs:4},
      {pos:23, driver:'Matt Kenseth', pts:283, ptsDiff:-218, wins:0, top5:0, top10:3, starts:20, dnfs:5},
      {pos:24, driver:'Elliott Sadler', pts:281, ptsDiff:-220, wins:0, top5:1, top10:4, starts:20, dnfs:6},
      {pos:25, driver:'Ward Burton', pts:276, ptsDiff:-225, wins:0, top5:0, top10:3, starts:20, dnfs:4},
      {pos:26, driver:'Mike Skinner', pts:258, ptsDiff:-243, wins:0, top5:0, top10:4, starts:20, dnfs:4},
      {pos:27, driver:'Derrick Cope', pts:222, ptsDiff:-279, wins:0, top5:0, top10:3, starts:20, dnfs:5},
      {pos:28, driver:'Kyle Petty', pts:218, ptsDiff:-283, wins:0, top5:1, top10:1, starts:20, dnfs:1},
      {pos:29, driver:'Mike McLaughlin', pts:190, ptsDiff:-311, wins:0, top5:0, top10:1, starts:20, dnfs:6},
      {pos:30, driver:'Kevin Harvick', pts:186, ptsDiff:-315, wins:0, top5:0, top10:0, starts:20, dnfs:5},
      {pos:31, driver:'Johnny Benson', pts:153, ptsDiff:-348, wins:0, top5:0, top10:0, starts:20, dnfs:7},
      {pos:32, driver:'Ryan Newman', pts:147, ptsDiff:-354, wins:0, top5:0, top10:0, starts:20, dnfs:8},
      {pos:33, driver:'Wally Dallenbach', pts:63, ptsDiff:-438, wins:0, top5:0, top10:1, starts:3, dnfs:0},
      {pos:34, driver:'Greg Biffle', pts:34, ptsDiff:-467, wins:0, top5:1, top10:1, starts:2, dnfs:1},
      {pos:35, driver:'Boris Said', pts:2, ptsDiff:-499, wins:0, top5:0, top10:0, starts:1, dnfs:1}
    ];

    const tbody = document.querySelector('#standingsTable tbody');

    function renderRows(rows){
      tbody.innerHTML = '';
      rows.forEach(r=>{
        const tr = document.createElement('tr');
        tr.setAttribute('data-pos', r.pos);
        tr.innerHTML = `
          <td class="num">${r.pos}</td>
          <td>${r.driver}</td>
          <td class="num">${r.pts}</td>
          <td class="num">${r.ptsDiff===null?'-':r.ptsDiff}</td>
          <td class="num">${r.wins}</td>
          <td class="num">${r.top5}</td>
          <td class="num">${r.top10}</td>
          <td class="num">${r.starts}</td>
          <td class="num">${r.dnfs}</td>
        `;
        tbody.appendChild(tr);
      })
    }

    // initial render
    renderRows(data);

    // filter
    document.getElementById('filterInput').addEventListener('input', e=>{
      const q = e.target.value.trim().toLowerCase();
      if(!q){ renderRows(data); return }
      const filtered = data.filter(d=>d.driver.toLowerCase().includes(q));
      renderRows(filtered);
    });

    // sort
    document.getElementById('sortSelect').addEventListener('change', e=>{
      const val = e.target.value;
      let copy = [...data];
      if(val==='pos') copy.sort((a,b)=>a.pos-b.pos);
      if(val==='pts') copy.sort((a,b)=>b.pts-a.pts);
      if(val==='wins') copy.sort((a,b)=>b.wins-a.wins);
      if(val==='top5') copy.sort((a,b)=>b.top5-a.top5?b.top5-a.top5: b.pts-a.pts );
      if(val==='dnfs') copy.sort((a,b)=>a.dnfs-b.dnfs);
      renderRows(copy);
    });

    // export CSV
    function toCSV(rows){
      const hdr = ['Pos','Driver','Pts','Pts-','Wins','Top5','Top10','Starts','DNFs'];
      const lines = [hdr.join(',')];
      rows.forEach(r=>{
        const row = [r.pos, '"'+r.driver.replace(/"/g,'""')+'"', r.pts, r.ptsDiff===null?'-':r.ptsDiff, r.wins, r.top5, r.top10, r.starts, r.dnfs];
        lines.push(row.join(','));
      });
      return lines.join('\n');
    }

    document.getElementById('exportBtn').addEventListener('click', ()=>{
      const csv = toCSV(data);
      const blob = new Blob([csv], {type:'text/csv'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url; a.download = 'gen4_season4_standings.csv';
      document.body.appendChild(a); a.click(); a.remove(); URL.revokeObjectURL(url);
    });

  </script>
</body>
</html>
