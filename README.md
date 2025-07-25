<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Voice Control Gaming System</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <style>
    body {
      min-height: 100vh;
      margin: 0;
      background: linear-gradient(135deg, #e0e7ff 0%, #f5f5f5 100%);
      font-family: gotham, Arial, sans-serif;
    }
    .login-container {
      min-height: 100vh;
      width: 100vw;
      display: flex;
      align-items: center;
      justify-content: center;
      position: absolute;
      top: 0; left: 0;
      background: rgba(255,255,255,0.95);
      z-index: 10;
    }
    .login-card {
      background: #fff;
      border-radius: 18px;
      box-shadow: 0 8px 32px rgba(0,0,0,0.18);
      padding: 48px 36px 36px 36px;
      max-width: 350px;
      width: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 28px;
      position: relative;
    }
    .login-card img {
      width: 70px;
      height: 70px;
      margin-bottom: 8px;
      border-radius: 50%;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
      background: #f0f4ff;
      object-fit: cover;
    }
    .login-card h2 {
      font-size: 2.1rem;
      font-weight: 700;
      margin: 0 0 8px 0;
      color: #222;
      letter-spacing: 1px;
    }
    .login-card p {
      color: #555;
      font-size: 1.05rem;
      margin: 0 0 10px 0;
      text-align: center;
    }
    .login-card input[type="text"] {
      width: 100%;
      padding: 14px 18px;
      border: 1.5px solid #dbeafe;
      border-radius: 9px;
      font-size: 1.08rem;
      outline: none;
      transition: border 0.2s;
      margin-bottom: 8px;
      background: #f8fafc;
      color: #222;
    }
    .login-card input[type="text"]:focus {
      border: 1.5px solid #6366f1;
      background: #fff;
    }
    .login-card button {
      width: 100%;
      padding: 14px 0;
      background: linear-gradient(90deg, #6366f1 0%, #60a5fa 100%);
      color: #fff;
      border: none;
      border-radius: 9px;
      font-size: 1.15rem;
      font-weight: 600;
      cursor: pointer;
      transition: background 0.2s, transform 0.1s;
      margin-top: 8px;
      box-shadow: 0 2px 8px rgba(99,102,241,0.08);
    }
    .login-card button:hover {
      background: linear-gradient(90deg, #4f46e5 0%, #2563eb 100%);
      transform: translateY(-2px) scale(1.03);
    }
    @media (max-width: 480px) {
      .login-card {
        padding: 28px 8px;
        max-width: 95vw;
      }
      .login-card h2 {
        font-size: 1.4rem;
      }
    }
  </style>
  <div class="login-container" id="login-section">
    <div class="login-card">
      <img src="flag.png" alt="Game Logo">
      <h2>Welcome!</h2>
      <p>Enter your name to start playing</p>
      <input type="text" id="username" placeholder="Your Name">
      <button id="login-btn">Start Game</button>
    </div>
  </div>
    <div id="description">
    <h2>🎤 ML-Powered Voice Control Gaming Tool 🕹️</h2>
    <p>Welcome to my final year project - A modular system that integrates voice commands into browser-based games using CNN-powered voice recognition. In the demo below, I’ve implemented it with three interactive mini-games showcasing unique voice controls! Feel free to Fork the repo, train a model and add your own games.
</p>

</div>
<div id="user-scores" style="display:none; margin-bottom: 20px;"></div>
<button id="logout-btn" style="display:none; margin-bottom: 20px;">Logout</button>
    <div class="game-container" style="display:none;">
      <a href="snake.html" class="game-card">
            <div class="game-image" style="background-image: url('snake.png');"></div>
            <h3>Guide a Snake</h3>
            <p>Play Now →</p>
        </a>
        <a href="flag.html" class="game-card">
            <div class="game-image" style="background-image: url('flag.png');"></div>
            <h3>Guess the flag</h3>
            <p>Play Now →</p>
        </a>

        <a href="sudoku.html" class="game-card">
            <div class="game-image" style="background-image: url('sudoku.png');"></div>
            <h3>Solve Sudoku</h3>
            <p>Play Now →</p>
        </a>
    </div>
    <script>
      function showMainContent() {
        document.getElementById('login-section').style.display = 'none';
        document.getElementById('user-scores').style.display = '';
        document.getElementById('logout-btn').style.display = '';
        document.querySelector('.game-container').style.display = '';
      }
      function hideMainContent() {
        document.getElementById('login-section').style.display = '';
        document.getElementById('user-scores').style.display = 'none';
        document.getElementById('logout-btn').style.display = 'none';
        document.querySelector('.game-container').style.display = 'none';
      }
      function login() {
        const name = document.getElementById("username").value.trim();
        if (name !== "") {
          localStorage.setItem("username", name);
          localStorage.setItem("currentUser", name);
          showMainContent();
        } else {
          alert("Please enter your name.");
        }
      }
      document.getElementById("login-btn").addEventListener("click", login);
      document.getElementById("username").addEventListener("keydown", function(e) {
        if (e.key === "Enter") login();
      });
      document.getElementById("logout-btn").addEventListener("click", function() {
        localStorage.removeItem("username");
        localStorage.removeItem("currentUser");
        hideMainContent();
      });
      // On page load, show main content if logged in
      window.onload = function() {
        if (localStorage.getItem("username")) {
          showMainContent();
        } else {
          hideMainContent();
        }
      };
    </script>
    <script src="main.js"></script>
  <!-- User Profile Icon -->
  <div id="user-profile-icon" title="View Profile"></div>

  <!-- User Profile Modal -->
  <div id="user-profile-modal">
    <div class="modal-content">
      <h2>Your Profile</h2>
      <div class="avatar-container">
        <img id="profile-avatar" class="avatar-img" src="https://cdn-icons-png.flaticon.com/512/149/149071.png" alt="Avatar">
        <input type="file" id="avatar-upload" class="avatar-upload" accept="image/*" style="display:none;">
        <button id="avatar-upload-btn">Change Avatar</button>
      </div>
      <div class="edit-username">
        <input id="edit-username-input" type="text" placeholder="Username">
        <button id="edit-username-btn">Change Username</button>
      </div>
      <div id="profile-username"></div>
      <table id="profile-stats-table">
        <thead>
          <tr><th>Game</th><th>Times Played</th><th>Highest Score</th></tr>
        </thead>
        <tbody></tbody>
      </table>
      <div id="recent-scores-section">
        <h3>Recent Scores</h3>
        <table id="recent-scores-table">
          <thead>
            <tr><th>Game</th><th>Score</th><th>Date</th></tr>
          </thead>
          <tbody></tbody>
        </table>
      </div>
      <div class="leaderboard-section">
        <h3>Leaderboard</h3>
        <select id="leaderboard-game-select"></select>
        <table class="leaderboard-table">
          <thead>
            <tr><th>Username</th><th>Highest Score</th></tr>
          </thead>
          <tbody id="leaderboard-table-body"></tbody>
        </table>
      </div>
      <button class="close-btn" onclick="document.getElementById('user-profile-modal').style.display='none'">Close</button>
    </div>
  </div>
</body>
</html>
