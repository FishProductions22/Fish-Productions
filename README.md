index.html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Gen-4 Season 4 — Final Points Standings</title>
  <style>
    body {
        margin: 0;
        padding: 0;
        font-family: Arial, sans-serif;
        background: #0b1622;
        color: #ffffff;
    }
    .container {
        width: 95%;
        max-width: 1200px;
        margin: 40px auto;
        background: #0f1c2e;
        padding: 20px;
        border-radius: 12px;
        box-shadow: 0 0 15px rgba(0,0,0,0.5);
    }
    table {
        width: 100%;
        border-collapse: collapse;
        margin-top: 20px;
    }
    th {
        background: #1d2d44;
        padding: 12px;
        text-align: left;
        font-weight: bold;
        color: #d3d6da;
    }
    tr {
        background: #132238; /* <<< unified navy row background */
    }
    td {
        padding: 12px;
        border-bottom: 1px solid #1f2f47;
        color: #e8ecf2;
    }
    tr:nth-child(even) {
        background: #0f1c2e; /* slightly darker navy for alternating */
    }
    h1 {
        text-align: center;
        color: #ffffff;
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
          <tr>
            <td>1</td>
            <td class="driver">
              <img src="images/terry-labonte.jpg" alt="Terry Labonte">
              Terry Labonte
            </td>
            <td>501</td><td>-</td><td>1</td><td>10</td><td>14</td><td>20</td><td>0</td>
          </tr>
          <tr class="alt">
            <td>2</td>
            <td class="driver">
              <img src="images/jeff-gordon.jpg" alt="Jeff Gordon">
              Jeff Gordon
            </td>
            <td>500</td><td>-1</td><td>4</td><td>10</td><td>13</td><td>20</td><td>2</td>
          </tr>
          <tr>
            <td>3</td>
            <td class="driver">
              <img src="images/dale-jarrett.jpg" alt="Dale Jarrett">
              Dale Jarrett
            </td>
            <td>456</td><td>-45</td><td>2</td><td>5</td><td>12</td><td>20</td><td>3</td>
          </tr>
          <!-- Continue pattern for all remaining drivers -->
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
