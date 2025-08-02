<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Counter Esports League</title>
  <style>
    body {
      background-color: #1f1f1f;
      color: white;
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
    }
    header {
      background-color: #2a2a2a;
      padding: 1rem;
      text-align: center;
      font-size: 1.5rem;
      font-weight: bold;
    }
    .container {
      padding: 2rem;
    }
    .tournament {
      background-color: #2a2a2a;
      border-radius: 8px;
      margin-bottom: 1rem;
      padding: 1rem;
      transition: 0.3s;
    }
    .tournament:hover {
      background-color: #3a3a3a;
    }
    .status {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      margin-bottom: 0.5rem;
    }
    .dot {
      width: 12px;
      height: 12px;
      border-radius: 50%;
    }
    .red { background-color: red; }
    .green { background-color: green; }
    .gray { background-color: gray; }
    .participants {
      margin-left: 1rem;
      font-size: 0.9rem;
    }
  </style>
</head>
<body>
  <header>Counter Esports League</header>
  <div class="container">
    <div class="tournament">
      <div class="status"><div class="dot green"></div> Активный турнир</div>
      <div>Название: ESL Pro League</div>
      <div class="participants">
        <div>Участники:</div>
        <ul>
          <li>Team Vitality</li>
          <li>Natus Vincere</li>
        </ul>
      </div>
    </div>

    <div class="tournament">
      <div class="status"><div class="dot red"></div> Прошедший турнир</div>
      <div>Название: PGL Major</div>
      <div class="participants">
        <div>Участники:</div>
        <ul>
          <li>G2 Esports</li>
          <li>FaZe Clan</li>
        </ul>
      </div>
    </div>

    <div class="tournament">
      <div class="status"><div class="dot gray"></div> Предстоящий турнир</div>
      <div>Название: BLAST Premier</div>
      <div class="participants">
        <div>Участники:</div>
        <ul>
          <li>Cloud9</li>
          <li>Astralis</li>
        </ul>
      </div>
    </div>
  </div>
</body>
</html>
