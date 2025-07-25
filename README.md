# Game Scores Backend Setup

## 1. MySQL Database Setup

1. Open your MySQL client (e.g., MySQL Workbench, phpMyAdmin, or command line).
2. Run the following SQL commands to create the database and table:

```sql
CREATE DATABASE game_scores;
USE game_scores;
CREATE TABLE scores (
  id INT AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(50),
  game VARCHAR(50),
  score INT,
  created_at DATETIME
);
```

## 2. Backend Setup

1. Make sure you have [Node.js](https://nodejs.org/) installed.
2. Open a terminal in the `VoiceControl-Games-ML-main` folder.
3. Install dependencies:
   ```bash
   npm install express mysql2 cors
   ```
4. Edit `server.js` and update the MySQL credentials:
   - `user: 'your_mysql_user'`
   - `password: 'your_mysql_password'`
5. Start the server:
   ```bash
   node server.js
   ```
   The server will run on port 3001.

## 3. Frontend Integration Example

To save a score from your game, use this JavaScript code:

```js
fetch('http://localhost:3001/api/scores', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ username: 'Alice', game: 'snake', score: 123 })
})
.then(res => res.json())
.then(data => console.log(data));
```

To get the top 10 scores:

```js
fetch('http://localhost:3001/api/scores')
  .then(res => res.json())
  .then(data => console.log(data));
```

---

**Now you can save and retrieve game scores using your own MySQL database!** 
