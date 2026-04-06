
// app.js
const express = require("express");
const app = express();

app.use(express.json());

// Temporary storage (instead of database)
let users = [];

// Frontend HTML + JS (served from backend)
app.get("/", (req, res) => {
  res.send(`
    <h2>Register</h2>
    <input id="ruser" placeholder="Username"><br><br>
    <input id="rpass" placeholder="Password"><br><br>
    <button onclick="register()">Register</button>

    <h2>Login</h2>
    <input id="luser" placeholder="Username"><br><br>
    <input id="lpass" placeholder="Password"><br><br>
    <button onclick="login()">Login</button>

    <script>
      async function register() {
        const username = document.getElementById("ruser").value;
        const password = document.getElementById("rpass").value;

        const res = await fetch("/register", {
          method: "POST",
          headers: {"Content-Type": "application/json"},
          body: JSON.stringify({ username, password })
        });

        alert(await res.text());
      }

      async function login() {
        const username = document.getElementById("luser").value;
        const password = document.getElementById("lpass").value;

        const res = await fetch("/login", {
          method: "POST",
          headers: {"Content-Type": "application/json"},
          body: JSON.stringify({ username, password })
        });

        alert(await res.text());
      }
    </script>
  `);
});

// Register API
app.post("/register", (req, res) => {
  const { username, password } = req.body;
  users.push({ username, password });
  res.send("User Registered");
});

// Login API
app.post("/login", (req, res) => {
  const { username, password } = req.body;

  const user = users.find(
    u => u.username === username && u.password === password
  );

  if (user) {
    res.send("Login Success");
  } else {
    res.send("Invalid Credentials");
  }
});

// Start server
app.listen(3000, () => {
  console.log("Server running at http://localhost:3000");
});
git init
git add .
git commit -m "simple fullstack app"
git branch -M main
git remote add origin <your-repo-link>
git push -u origin main
