# FishProductions
index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>FishProductions22 — Featured Videos</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background: #f4f4f4;
      color: #333;
    }
    header {
      background: #111;
      color: #fff;
      padding: 40px 20px;
      text-align: center;
    }
    header h1 {
      margin: 0;
      font-size: 2.8em;
    }
    header p {
      margin: 10px 0 0;
      font-size: 1.1em;
    }
    .videos-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 20px;
      padding: 20px;
      max-width: 1000px;
      margin: 0 auto;
    }
    .video-card {
      background: #000;
      overflow: hidden;
      position: relative;
      padding-top: 56.25%; /* 16:9 aspect ratio */
    }
    .video-card iframe {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      border: none;
    }
    footer {
      background: #111;
      color: #fff;
      text-align: center;
      padding: 20px;
      margin-top: 40px;
    }
    footer a {
      color: #4FC3F7;
      text-decoration: none;
    }
    @media (max-width: 600px) {
      header h1 { font-size: 2em; }
      header p { font-size: 1em; }
    }
  </style>
</head>
<body>

  <header>
    <h1>FishProductions22</h1>
    <p>Our top videos — check them out below 👇</p>
  </header>

  <section class="videos-grid">
    <div class="video-card">
      <iframe src="https://www.youtube.com/embed/k25tLVoaFcg" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
    <div class="video-card">
      <iframe src="https://www.youtube.com/embed/oGwFSVVrHqI" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
    <div class="video-card">
      <iframe src="https://www.youtube.com/embed/aOJFMLIOR9A" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
  </section>

  <footer>
    <p>Subscribe on YouTube for more →</p>
    <p><a href="https://www.youtube.com/@fishproductions22" target="_blank">FishProductions22 Channel</a></p>
  </footer>

</body>
</html>
