# 🔥 **Top Hack Prevention Techniques (Full Guide)**

These will protect your app from:

* SQL Injection
* XSS
* CSRF
* Token theft
* Session hijacking
* API abuse
* Brute force
* DDOS
* Malware uploads

Let’s cover everything one by one.

---

# 1️⃣ **Input Validation & Sanitization (Most Important)**

Never trust user input.

✔ Remove harmful characters
✔ Validate type (email, number, length)
✔ Escape HTML to prevent XSS
✔ Validate file uploads (type, size)

**Example (Node.js):**

```js
import validator from "validator";

if (!validator.isEmail(email)) {
  throw new Error("Invalid email!");
}
```

---

# 2️⃣ **Use Prepared Statements (Prevent SQL Injection)**

For SQL databases:

❌ Wrong:

```sql
SELECT * FROM users WHERE email = '${email}'
```

✔ Safe:

```sql
SELECT * FROM users WHERE email = ?
```

For MongoDB, avoid:

```js
User.find({ $where: "this.age == input" })
```

---

# 3️⃣ **Hash Passwords (Never store plain passwords)**

Use bcrypt:

```js
const hashed = await bcrypt.hash(password, 10);
```

Hashing techniques:

* bcrypt
* argon2 (best)
* scrypt

---

# 4️⃣ **Use JWT or Session Tokens Securely**

✔ Keep tokens short-lived
✔ Rotate refresh tokens
✔ Store JWT in `httpOnly` cookies
✔ Do NOT store tokens in localStorage

Why?
LocalStorage is accessible to JavaScript → vulnerable to XSS.

---

# 5️⃣ **Enable CORS Properly**

Never use `"*"` in production.

❌ Wrong:

```js
app.use(cors({ origin: "*" }));
```

✔ Safe:

```js
app.use(cors({
  origin: "https://yourdomain.com",
  credentials: true
}));
```

---

# 6️⃣ **Rate Limiting (Prevent Brute Force & Abuse)**

Example:

* Limit login attempts
* Limit API calls per minute

Node.js:

```js
import rateLimit from "express-rate-limit";

app.use("/login", rateLimit({
  windowMs: 1 * 60 * 1000,  // 1 min
  max: 5                     // 5 requests
}));
```

---

# 7️⃣ **Helmet (Prevent common attacks)**

For Express:

```js
import helmet from "helmet";
app.use(helmet());
```

Protection:

* Clickjacking
* XSS
* MIME sniffing
* Content security

---

# 8️⃣ **HTTPS Everywhere**

✔ Encrypt data in transit
✔ Protect tokens
✔ Protect credentials

HTTP = data sent in plain text
HTTPS = encrypted

Use SSL certificate (Free from Let's Encrypt).

---

# 9️⃣ **Content Security Policy (CSP)**

Prevents XSS by blocking fake scripts.

Example header:

```
Content-Security-Policy: default-src 'self';
```

---

# 🔟 **CSRF Protection (Very Important)**

For forms and cookies:

✔ Use CSRF tokens
✔ SameSite cookies enabled

Express:

```js
import csrf from "csurf";
app.use(csrf());
```

---

# 1️⃣1️⃣ **File Upload Validation**

Prevent malware upload.

✔ Allow only safe file types
✔ Limit file size
✔ Scan uploads
✔ Rename files

Example:

* Only images (jpeg/png)
* Max 2MB
* No executable files

---

# 1️⃣2️⃣ **Logging & Monitoring**

Monitor:

* Failed login attempts
* Suspicious IPs
* Sudden traffic spikes

Use:

* Winston (Node)
* Datadog
* Sentry
* ELK stack

---

# 1️⃣3️⃣ **Database Security**

✔ Disable public access
✔ Allow only whitelisted IPs
✔ Use environment variables
✔ Enable encryption at rest
✔ Backup regularly

MongoDB:

* Use SRV connection
* Turn on user authentication
* Avoid admin user for apps

---

# 1️⃣4️⃣ **Environment Variable Security**

Never push `.env` to GitHub.

✔ Add to `.gitignore`
✔ Use dotenv
✔ Use secret managers (AWS, GCP, Vercel)

---

# 1️⃣5️⃣ **Avoid eval(), new Function(), innerHTML**

These create security holes.

❌ Avoid:

```js
eval(userInput);
element.innerHTML = userInput;
```

✔ Use:

```js
element.textContent = userInput;
```

---

# 1️⃣6️⃣ **Middleware Authentication**

Protect APIs:

```js
function auth(req, res, next) {
   const token = req.headers.authorization?.split(" ")[1];
   if (!token) return res.status(401).json({ error: "Unauthorized" });
   next();
}
```

---

# 1️⃣7️⃣ **Strong Password Policy**

✔ Minimum length
✔ Numbers + special chars
✔ Prevent common passwords
✔ Warn reused passwords

---

# 1️⃣8️⃣ **Avoid Sensitive Data Exposure**

Never return:

* Password
* Token
* OTP
* Confidential info

Use:

```js
delete user.password;
```

---

# 1️⃣9️⃣ **Server Hardening**

✔ Disable unnecessary ports
✔ Limit SSH access
✔ Use firewalls
✔ Use fail2ban
✔ Disable root login

---

# 2️⃣0️⃣ **DDOS Protection**

Use:

* Cloudflare
* Nginx rate limiting
* Load balancing
* Token bucket algorithms

---

# 🎯 Full Security Checklist

| Area     | Protection                           |
| -------- | ------------------------------------ |
| Auth     | JWT/Sessions, rate limiting, hashing |
| Backend  | Helmet, validation, sanitized input  |
| Database | No public access, IP whitelisting    |
| Frontend | CSP headers, avoid innerHTML         |
| Network  | HTTPS, firewall                      |
| Tokens   | httpOnly cookies, short expiry       |
| Requests | CORS, CSRF                           |
| Code     | avoid eval, sanitize                 |

---
