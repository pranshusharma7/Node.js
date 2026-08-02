<div align="center">

# 🟩 Node.js: Zero to Advanced

### Ek complete guide — JavaScript se backend developer banne tak

![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Advanced-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)

*JavaScript pata hai? Ab usse browser ke bahar, server par chalana seekhein — sab kuch easy Hinglish mein.*

</div>

---

## 📖 Kaise use karein yeh guide?

1. **Pehle JavaScript ke basics** pakke hone chahiye (functions, arrays, objects, async/await) — agar nahi hain, pehle wahan se shuru karein.
2. Order mein padhein — har topic pichle par based hai.
3. Har code example khud terminal mein chala kar dekhein.
4. Practice tasks zaroor karein — Node.js sirf padhne se nahi, banane se aata hai.

> 💡 **Setup:** [nodejs.org](https://nodejs.org) se Node.js install karein. Terminal mein `node -v` chala kar version check karein.

---

## 📑 Table of Contents

- [Part 1: Foundations](#-part-1-foundations)
  - [1.1 Node.js Kya Hai?](#11-nodejs-kya-hai)
  - [1.2 Node.js vs Browser JS](#12-nodejs-vs-browser-js)
  - [1.3 Pehla Node Program](#13-pehla-node-program)
  - [1.4 npm & package.json](#14-npm--packagejson)
- [Part 2: Core Modules](#-part-2-core-modules)
  - [2.1 Module System](#21-module-system)
  - [2.2 File System (fs)](#22-file-system-fs)
  - [2.3 Path Module](#23-path-module)
  - [2.4 OS & Events Module](#24-os--events-module)
- [Part 3: Node.js ka Asynchronous Nature](#-part-3-nodejs-ka-asynchronous-nature)
  - [3.1 Single-Threaded, Non-Blocking](#31-single-threaded-non-blocking-kya-matlab)
  - [3.2 Event Loop in Node](#32-event-loop-in-node)
- [Part 4: HTTP Server from Scratch](#-part-4-http-server-from-scratch)
- [Part 5: Express.js](#-part-5-expressjs)
  - [5.1 Express Setup](#51-express-setup)
  - [5.2 Routing](#52-routing)
  - [5.3 Middleware](#53-middleware)
  - [5.4 Request & Response](#54-request--response-objects)
- [Part 6: REST API Banana](#-part-6-rest-api-banana)
- [Part 7: Databases ke saath](#-part-7-databases-ke-saath)
  - [7.1 MongoDB + Mongoose](#71-mongodb--mongoose)
  - [7.2 CRUD Operations](#72-crud-operations)
- [Part 8: Authentication](#-part-8-authentication)
  - [8.1 Password Hashing](#81-password-hashing-bcrypt)
  - [8.2 JWT Tokens](#82-jwt-json-web-tokens)
- [Part 9: Error Handling & Validation](#-part-9-error-handling--validation)
- [Part 10: Environment Variables & Config](#-part-10-environment-variables--config)
- [Part 11: Advanced Concepts](#-part-11-advanced-concepts)
  - [11.1 Streams](#111-streams)
  - [11.2 Buffer](#112-buffer)
  - [11.3 Child Processes & Cluster](#113-child-processes--cluster)
  - [11.4 Worker Threads](#114-worker-threads)
- [Part 12: Testing & Deployment](#-part-12-testing--deployment)
- [Part 13: Practice Projects](#-part-13-practice-projects-beginner--advanced)
- [Part 14: Resources](#-part-14-further-resources)

---

## 🟢 Part 1: Foundations

### 1.1 Node.js Kya Hai?

Node.js ek **JavaScript runtime environment** hai jo JS code ko browser ke bahar bhi chalane deta hai — jaise server par, terminal mein, ya kisi bhi machine par.

- Node.js **Chrome ke V8 engine** par based hai (jo JS ko fast machine code mein convert karta hai)
- Isse hum **backend** (server-side) development kar sakte hain — databases, APIs, file handling, authentication, sab kuch JS mein
- Ab aap **MERN Stack** (MongoDB, Express, React, Node) jaisi full-stack technology use kar sakte hain

### 1.2 Node.js vs Browser JS

| | Browser JavaScript | Node.js |
|---|---|---|
| Chalta kahan hai | Browser ke andar | Computer/server par directly |
| DOM access | ✅ Haan (`document`, `window`) | ❌ Nahi |
| File system access | ❌ Nahi (security ki wajah se) | ✅ Haan (`fs` module) |
| Use case | Website interactive banana | Server, API, database, CLI tools |
| Modules | `import`/`export` (ES Modules) | `require`/`module.exports` (CommonJS) |

### 1.3 Pehla Node Program

```javascript
// app.js
console.log("Namaste Node.js!");

function add(a, b) {
  return a + b;
}
console.log(add(5, 3));
```

Terminal mein chalayein:
```bash
node app.js
```

### 1.4 npm & package.json

**npm** (Node Package Manager) — dusron ka likha hua code (packages/libraries) apne project mein use karne ka tareeka.

```bash
# Naya project shuru karna
npm init -y

# Package install karna
npm install express

# Sirf development ke liye (production mein nahi chahiye)
npm install --save-dev nodemon

# Global install (poore system mein available)
npm install -g nodemon
```

`package.json` — yeh file aapke project ka "identity card" hai:

```json
{
  "name": "mera-project",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  }
}
```

```bash
npm run dev    # scripts mein defined "dev" command chalayega
```

> 📌 `node_modules` folder aur `package-lock.json` — inhe kabhi GitHub par upload na karein. Ek `.gitignore` file banayein aur usme `node_modules` likh dein.

**🎯 Practice Task:** `npm init -y` se naya project banayein, ek `app.js` file banayein jo `console.log` se aapka naam print kare, aur `npm run dev` se chalayein (nodemon install karke).

---

## 🟡 Part 2: Core Modules

### 2.1 Module System

Node.js mein code ko files mein todkar rakhte hain — **modules**.

```javascript
// math.js
function add(a, b) {
  return a + b;
}
function subtract(a, b) {
  return a - b;
}

module.exports = { add, subtract };
```

```javascript
// app.js
const math = require("./math");
console.log(math.add(5, 3)); // 8

// Ya destructure karke
const { add, subtract } = require("./math");
console.log(subtract(5, 3)); // 2
```

**Built-in modules** — Node.js ke saath already aate hain, install karne ki zaroorat nahi:

```javascript
const fs = require("fs");
const path = require("path");
const os = require("os");
const http = require("http");
```

### 2.2 File System (fs)

Files padhna, likhna, delete karna — server-side ka bahut common kaam:

```javascript
const fs = require("fs");

// Synchronous (blocking) — line-by-line ruk kar chalta hai
const data = fs.readFileSync("data.txt", "utf-8");
console.log(data);

// Asynchronous (non-blocking) — recommended tareeka
fs.readFile("data.txt", "utf-8", (err, data) => {
  if (err) {
    console.log("Error:", err);
    return;
  }
  console.log(data);
});

// File likhna
fs.writeFile("output.txt", "Namaste Node!", (err) => {
  if (err) throw err;
  console.log("File likh di gayi!");
});

// Modern tareeka — Promises ke saath (async/await)
const fsPromises = require("fs/promises");

async function readMyFile() {
  try {
    const content = await fsPromises.readFile("data.txt", "utf-8");
    console.log(content);
  } catch (err) {
    console.log("Error:", err);
  }
}
```

> ⚠️ **Rule:** Real projects mein hamesha **asynchronous** version use karein (`readFile`, `writeFile`) — synchronous version (`readFileSync`) poore server ko rok deta hai jab tak file na padh le, jisse baaki requests slow ho jati hain.

### 2.3 Path Module

File paths ko sahi tareeke se handle karne ke liye (Windows/Mac/Linux — sab par kaam kare):

```javascript
const path = require("path");

console.log(path.join(__dirname, "files", "data.txt"));
// Poora path banata hai, chahe OS koi bhi ho

console.log(path.basename("/users/pranshu/app.js")); // app.js
console.log(path.extname("app.js"));                  // .js
console.log(__dirname);  // current folder ka path
console.log(__filename); // current file ka poora path
```

### 2.4 OS & Events Module

```javascript
const os = require("os");
console.log(os.platform());   // "linux", "win32", "darwin"
console.log(os.freemem());    // free memory
console.log(os.cpus().length); // CPU cores ki ginti

// EventEmitter — Node ka event-based system, bahut important concept
const EventEmitter = require("events");
const myEmitter = new EventEmitter();

myEmitter.on("greet", (naam) => {
  console.log(`Namaste, ${naam}!`);
});

myEmitter.emit("greet", "Pranshu"); // Namaste, Pranshu!
```

**🎯 Practice Task:** Ek script banayein jo `fs` module se ek text file mein aapke 5 favourite subjects likhe, phir usi file ko wapas padh kar console mein print kare.

---

## 🟠 Part 3: Node.js ka Asynchronous Nature

### 3.1 Single-Threaded, Non-Blocking Kya Matlab?

Node.js **ek hi thread** (single-threaded) par chalta hai, lekin **non-blocking** hai — matlab lambi cheezein (file read, database query, API call) background mein chalti hain, aur Node dusre requests handle karta rehta hai.

```javascript
console.log("1. Server shuru hua");

setTimeout(() => {
  console.log("3. Yeh 2 second baad chalega (background mein)");
}, 2000);

console.log("2. Yeh turant chalega");

// Output: 1, 2, 3 (order note karein — 3 sabse aakhir mein)
```

Isi wajah se Node.js **hazaaron requests ek saath** handle kar sakta hai bina hang hue — jo isse web servers ke liye bahut fast banata hai.

### 3.2 Event Loop in Node

Node.js ka event loop browser jaisa hi hai, lekin extra phases ke saath (timers, I/O callbacks, etc.):

```javascript
console.log("Start");

setTimeout(() => console.log("Timeout"), 0);

Promise.resolve().then(() => console.log("Promise"));

console.log("End");

// Output order: Start, End, Promise, Timeout
// Kyunki Promises (microtasks) hamesha setTimeout (macrotasks) se pehle chalte hain
```

---

## 🔴 Part 4: HTTP Server from Scratch

Bina kisi library ke, sirf Node.js se ek web server banate hain — samajhne ke liye ki Express ke peeche kya hota hai:

```javascript
const http = require("http");

const server = http.createServer((req, res) => {
  console.log(req.method, req.url); // request ka method aur URL

  if (req.url === "/") {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Home Page");
  } else if (req.url === "/about") {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("About Page");
  } else {
    res.writeHead(404, { "Content-Type": "text/plain" });
    res.end("404 - Page Not Found");
  }
});

server.listen(3000, () => {
  console.log("Server chal raha hai: http://localhost:3000");
});
```

> 📌 Yeh dekh kar samajh aata hai ki har route manually likhna kitna mushkil hoga — isliye **Express.js** jaisa framework use karte hain.

**🎯 Practice Task:** Upar wale server mein ek `/contact` route add karein jo apna naam aur email plain text mein return kare.

---

## 🟣 Part 5: Express.js

Express.js — Node.js ka sabse popular **web framework**, jo server banana bahut aasan bana deta hai.

### 5.1 Express Setup

```bash
npm install express
```

```javascript
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("Namaste from Express!");
});

app.listen(3000, () => {
  console.log("Server chal raha hai: http://localhost:3000");
});
```

### 5.2 Routing

```javascript
app.get("/", (req, res) => {
  res.send("Home Page");
});

app.post("/submit", (req, res) => {
  res.send("Form submit hua");
});

// Route parameters (dynamic values)
app.get("/user/:id", (req, res) => {
  res.send(`User ID: ${req.params.id}`);
});

// Query parameters — jaise /search?naam=pranshu
app.get("/search", (req, res) => {
  res.send(`Search kiya: ${req.query.naam}`);
});
```

### 5.3 Middleware

Middleware — ek function jo **request aur response ke beech mein** chalta hai. Logging, authentication, JSON parsing — sab middleware se hota hai.

```javascript
// Built-in middleware — JSON body ko parse karne ke liye
app.use(express.json());

// Custom middleware — har request pe chalega
app.use((req, res, next) => {
  console.log(`${req.method} request aayi: ${req.url}`);
  next(); // agle middleware/route ko control pass karna zaroori hai
});

// Route-specific middleware
function checkAuth(req, res, next) {
  const isLoggedIn = true; // yahan real check hoga
  if (isLoggedIn) {
    next();
  } else {
    res.status(401).send("Login karna zaroori hai");
  }
}

app.get("/dashboard", checkAuth, (req, res) => {
  res.send("Welcome to Dashboard");
});
```

### 5.4 Request & Response Objects

```javascript
app.post("/user", (req, res) => {
  console.log(req.body);    // POST data (JSON body)
  console.log(req.params);  // URL parameters (/user/:id)
  console.log(req.query);   // Query string (?key=value)
  console.log(req.headers); // Request headers

  res.status(201).json({ message: "User bana diya", data: req.body });
});
```

**🎯 Practice Task:** Ek Express server banayein jisme 3 routes hon: `/`, `/about`, aur `/user/:naam` (jo URL se naam lekar "Namaste, [naam]!" return kare).

---

## 🔵 Part 6: REST API Banana

REST API — data ko **HTTP methods** ke through manage karne ka standard tareeka:

| Method | Kaam |
|--------|------|
| `GET` | Data padhna (Read) |
| `POST` | Naya data banana (Create) |
| `PUT`/`PATCH` | Data update karna (Update) |
| `DELETE` | Data delete karna (Delete) |

```javascript
const express = require("express");
const app = express();
app.use(express.json());

let students = [
  { id: 1, naam: "Pranshu", marks: 85 },
  { id: 2, naam: "Rahul", marks: 78 },
];

// GET all
app.get("/students", (req, res) => {
  res.json(students);
});

// GET one
app.get("/students/:id", (req, res) => {
  const student = students.find((s) => s.id === parseInt(req.params.id));
  if (!student) return res.status(404).json({ message: "Student nahi mila" });
  res.json(student);
});

// POST — naya student add karna
app.post("/students", (req, res) => {
  const newStudent = { id: students.length + 1, ...req.body };
  students.push(newStudent);
  res.status(201).json(newStudent);
});

// PUT — update karna
app.put("/students/:id", (req, res) => {
  const student = students.find((s) => s.id === parseInt(req.params.id));
  if (!student) return res.status(404).json({ message: "Nahi mila" });
  Object.assign(student, req.body);
  res.json(student);
});

// DELETE
app.delete("/students/:id", (req, res) => {
  students = students.filter((s) => s.id !== parseInt(req.params.id));
  res.json({ message: "Delete ho gaya" });
});

app.listen(3000, () => console.log("API chal raha hai"));
```

**🎯 Practice Task:** Upar wale students API ko Postman ya Thunder Client se test karein — sabhi 5 routes try karein (GET all, GET one, POST, PUT, DELETE).

---

## 🟤 Part 7: Databases ke saath

### 7.1 MongoDB + Mongoose

```bash
npm install mongoose
```

```javascript
const mongoose = require("mongoose");

mongoose.connect("mongodb://localhost:27017/mydatabase")
  .then(() => console.log("MongoDB se connect ho gaya"))
  .catch((err) => console.log("Connection error:", err));

// Schema — data ka structure define karna
const studentSchema = new mongoose.Schema({
  naam: { type: String, required: true },
  marks: { type: Number, required: true },
  createdAt: { type: Date, default: Date.now },
});

// Model — schema se actual "Student" object banaya
const Student = mongoose.model("Student", studentSchema);
```

### 7.2 CRUD Operations

```javascript
// CREATE
async function createStudent() {
  const student = new Student({ naam: "Pranshu", marks: 90 });
  await student.save();
  console.log("Save ho gaya:", student);
}

// READ
async function getStudents() {
  const allStudents = await Student.find();
  const oneStudent = await Student.findById("someId");
  console.log(allStudents);
}

// UPDATE
async function updateStudent(id) {
  const updated = await Student.findByIdAndUpdate(id, { marks: 95 }, { new: true });
  console.log(updated);
}

// DELETE
async function deleteStudent(id) {
  await Student.findByIdAndDelete(id);
  console.log("Delete ho gaya");
}
```

**Express + Mongoose milakar:**
```javascript
app.post("/students", async (req, res) => {
  try {
    const student = await Student.create(req.body);
    res.status(201).json(student);
  } catch (err) {
    res.status(400).json({ error: err.message });
  }
});
```

---

## ⚫ Part 8: Authentication

### 8.1 Password Hashing (bcrypt)

Password ko **kabhi bhi plain text mein store nahi karte** — hamesha hash karke:

```bash
npm install bcrypt
```

```javascript
const bcrypt = require("bcrypt");

async function registerUser(password) {
  const hashedPassword = await bcrypt.hash(password, 10); // 10 = salt rounds
  console.log(hashedPassword); // random-looking string
  // isko database mein store karein, original password kabhi nahi
}

async function loginUser(inputPassword, storedHash) {
  const isMatch = await bcrypt.compare(inputPassword, storedHash);
  console.log(isMatch); // true/false
}
```

### 8.2 JWT (JSON Web Tokens)

Login ke baad user ko "pehchaanne" ka tareeka — bina baar-baar password maange:

```bash
npm install jsonwebtoken
```

```javascript
const jwt = require("jsonwebtoken");
const SECRET_KEY = "yeh-secret-kisi-ko-mat-batana";

// Login ke baad token banana
function generateToken(user) {
  return jwt.sign({ id: user.id, naam: user.naam }, SECRET_KEY, { expiresIn: "1h" });
}

// Middleware — token verify karna
function verifyToken(req, res, next) {
  const token = req.headers["authorization"]?.split(" ")[1];
  if (!token) return res.status(401).json({ message: "Token nahi mila" });

  try {
    const decoded = jwt.verify(token, SECRET_KEY);
    req.user = decoded;
    next();
  } catch (err) {
    res.status(403).json({ message: "Invalid token" });
  }
}

app.get("/profile", verifyToken, (req, res) => {
  res.json({ message: `Welcome ${req.user.naam}` });
});
```

> ⚠️ `SECRET_KEY` jaisi cheezein **kabhi code mein hardcode na karein** — inhe `.env` file mein rakhein ([Part 10](#-part-10-environment-variables--config) dekhein).

---

## 🟢 Part 9: Error Handling & Validation

```javascript
// Global error handling middleware — app.js ke sabse aakhir mein
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ message: "Kuch galat ho gaya server mein" });
});

// Async routes mein errors ko catch karna
app.get("/students/:id", async (req, res, next) => {
  try {
    const student = await Student.findById(req.params.id);
    if (!student) {
      return res.status(404).json({ message: "Student nahi mila" });
    }
    res.json(student);
  } catch (err) {
    next(err); // error handling middleware ko bhej diya
  }
});
```

**Validation** (input data check karna) — `express-validator` jaisi library se:

```bash
npm install express-validator
```

```javascript
const { body, validationResult } = require("express-validator");

app.post(
  "/students",
  [
    body("naam").notEmpty().withMessage("Naam zaroori hai"),
    body("marks").isNumeric().withMessage("Marks number hone chahiye"),
  ],
  (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
      return res.status(400).json({ errors: errors.array() });
    }
    res.send("Data valid hai!");
  }
);
```

---

## 🟡 Part 10: Environment Variables & Config

Secret keys, database URLs — inhe code mein na likh kar `.env` file mein rakhte hain:

```bash
npm install dotenv
```

```
# .env file
PORT=3000
DB_URL=mongodb://localhost:27017/mydb
JWT_SECRET=mera-secret-key
```

```javascript
// app.js ke sabse upar
require("dotenv").config();

const PORT = process.env.PORT || 3000;
const DB_URL = process.env.DB_URL;

app.listen(PORT, () => console.log(`Server ${PORT} par chal raha hai`));
```

> ⚠️ **Zaroori:** `.env` file ko `.gitignore` mein add karein — isse kabhi GitHub par upload na karein, warna aapki secret keys public ho jayengi.

---

## 🟠 Part 11: Advanced Concepts

### 11.1 Streams

Bade files ya data ko **ek saath poora load kiye bina, tukdo mein (chunks)** process karna:

```javascript
const fs = require("fs");

// Bina stream ke — poori file memory mein load hogi (bade file ke liye bura)
// Stream ke saath — chunk by chunk padhta hai (efficient)
const readStream = fs.createReadStream("bigfile.txt", "utf-8");

readStream.on("data", (chunk) => {
  console.log("Naya chunk mila:", chunk.length, "characters");
});

readStream.on("end", () => {
  console.log("File poori padh li gayi");
});
```

### 11.2 Buffer

Binary data (images, videos, raw bytes) ko handle karne ka tareeka:

```javascript
const buf = Buffer.from("Namaste");
console.log(buf);           // <Buffer 4e 61 6d 61 73 74 65>
console.log(buf.toString()); // Namaste
```

### 11.3 Child Processes & Cluster

Node.js single-threaded hai, lekin **cluster module** se multiple CPU cores use kar sakte hain:

```javascript
const cluster = require("cluster");
const os = require("os");

if (cluster.isPrimary) {
  const numCPUs = os.cpus().length;
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork(); // har CPU core ke liye ek worker
  }
} else {
  // Worker process yahan Express server chalayega
  const app = require("express")();
  app.listen(3000);
}
```

### 11.4 Worker Threads

CPU-heavy kaam (jaise complex calculations) ko main thread block kiye bina alag thread mein chalana:

```javascript
const { Worker, isMainThread, parentPort } = require("worker_threads");

if (isMainThread) {
  const worker = new Worker(__filename);
  worker.on("message", (msg) => console.log("Worker se mila:", msg));
} else {
  parentPort.postMessage("Heavy calculation complete!");
}
```

---

## 🔴 Part 12: Testing & Deployment

**Testing** (Jest ke saath):
```bash
npm install --save-dev jest
```
```javascript
// sum.js
function sum(a, b) { return a + b; }
module.exports = sum;

// sum.test.js
const sum = require("./sum");
test("2 + 3 barabar 5 hona chahiye", () => {
  expect(sum(2, 3)).toBe(5);
});
```
```bash
npx jest
```

**Deployment checklist:**
- Environment variables production server par set karein (Render, Railway, Vercel dashboard mein)
- `package.json` mein `"start": "node app.js"` script hona chahiye
- Free hosting options: **Render**, **Railway**, **Cyclic**, **Vercel** (serverless functions ke liye)

---

## 🎯 Part 13: Practice Projects (Beginner → Advanced)

| # | Project | Concepts Cover Honge |
|---|---------|----------------------|
| 1 | 📁 File Organizer CLI | `fs`, `path`, command-line args |
| 2 | 🌐 Basic HTTP Server | `http` module, routing |
| 3 | 📝 Notes API | Express, REST routes, in-memory array |
| 4 | 🔐 Login/Signup System | bcrypt, JWT, MongoDB |
| 5 | 📷 Image Upload API | `multer`, file handling |
| 6 | 💬 Real-time Chat App | Socket.io, WebSockets |
| 7 | 🛒 E-commerce Backend | MongoDB, CRUD, authentication, cart logic |
| 8 | 📊 URL Shortener | Express, MongoDB, redirects |
| 9 | 📧 Email Sender Service | `nodemailer` |
| 10 | 🚀 Full REST API + Deployment | Sab kuch milakar, Render/Railway par deploy |

> 💡 **Suggestion:** Yeh projects [JavaScript guide](#) ke frontend knowledge ke saath combine karke **MERN stack full projects** banayein — yeh internship applications mein sabse zyada impress karta hai.

---

## 📚 Part 14: Further Resources

- [Node.js Official Docs](https://nodejs.org/en/docs/) — sabse authentic documentation
- [Express.js Official Docs](https://expressjs.com/) — Express ke liye complete guide
- [MongoDB University](https://learn.mongodb.com/) — free MongoDB courses
- [Postman](https://www.postman.com/) — API testing ke liye must-have tool

---

<div align="center">

### 🌟 Agar yeh guide helpful lagi, toh repo ko star ⭐ karna na bhoolein!

**Happy Backend Coding! 🚀**

</div>
