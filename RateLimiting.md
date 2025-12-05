# 🚀 **What is Rate Limiting? (Very Simple)**

**Rate Limiting** means **restricting how many requests a user/IP can make** to your server **within a specific time**.

### In simple words:

> **Rate Limiting prevents users (or bots) from hitting your API too many times in a short period.**

---

# 🧠 **Why Rate Limiting Is Needed?**

✔ Stop brute-force login attacks
✔ Stop bots from overusing your API
✔ Prevent DDoS-like behavior
✔ Avoid server overload
✔ Prevent someone from spamming signup/login
✔ Protect paid APIs from overuse

---

# ⚙️ **How Rate Limiting Works (Visualization)**

![Image](https://media.geeksforgeeks.org/wp-content/uploads/20240725172750/What-is-Rate-Limiting.png?utm_source=chatgpt.com)

![Image](https://miro.medium.com/1%2A3DUoq3XoknSKms9fbZJXLQ.gif?utm_source=chatgpt.com)

![Image](https://miro.medium.com/0%2AJZSfWyVXXnLncii9?utm_source=chatgpt.com)

### Basic process:

1. User hits your API → `/login`
2. Rate limiter checks:

```
Has this IP/user exceeded the limit?
```

3. If **not exceeded** → allow request
4. If exceeded → block request with:

```
429 Too Many Requests
```

---

# 📊 **Example of Rate Limit Rules**

| Rule                              | Meaning                   |
| --------------------------------- | ------------------------- |
| **100 requests / minute**         | Limit user to 100 req/min |
| **5 login tries / 10 minutes**    | Protect login page        |
| **1000 API calls / day per user** | Protect paid API          |

---

# 🛠️ **Rate Limiting in Node.js (Express)**

Use `express-rate-limit` package.

### Install:

```
npm install express-rate-limit
```

### Basic Example:

```js
import rateLimit from "express-rate-limit";

const limiter = rateLimit({
  windowMs: 1 * 60 * 1000, // 1 minute
  max: 100,                // limit 100 requests
});

app.use(limiter);
```

---

# 🔐 **Rate Limiting for Login (Very Important)**

```js
const loginLimiter = rateLimit({
  windowMs: 10 * 60 * 1000, // 10 min
  max: 5,
  message: "Too many login attempts!"
});

app.post("/login", loginLimiter, loginController);
```

Prevents brute-force attacks.

---

# ⚡ **Advanced Rate Limiting (Redis)**

In large systems:

* Use Redis for distributed rate limiting
* Because multiple servers must share the same counter

Example:

```
IP 123.11.22.3 → 5 requests left
```

Stored in Redis.

---

# 🧩 **Algorithms Used for Rate Limiting**

1. **Token Bucket**
2. **Leaky Bucket**
3. **Fixed Window**
4. **Sliding Window**

Most services use **Token Bucket**.

---

# 🧪 **Visual Example (Token Bucket)**

![Image](https://miro.medium.com/0%2AJZSfWyVXXnLncii9?utm_source=chatgpt.com)

![Image](https://media.geeksforgeeks.org/wp-content/uploads/20230301163751/ratelimiter.png?utm_source=chatgpt.com)

* Bucket has tokens
* Each request removes 1 token
* Tokens refill slowly
* If bucket empty → requests rejected

---

# 🌍 **Real-World Examples**

### Instagram:

* Limit likes per minute
* Limit follows per hour

### YouTube API:

* 10,000 units/day for free users

### Gmail:

* Limits email sending frequency

### MERN Apps:

* Limit login attempts
* Limit OTP requests
* Limit comment posting

---

# 🎯 **Benefits of Rate Limiting**

✔ Protects server from overload
✔ Reduces brute-force attacks
✔ Stops bot spam
✔ Saves server cost
✔ Better UX (API stability)

---

# 🛑 **Response When Limit is Hit**

Server returns:

```
HTTP 429 - Too Many Requests
```

---

# 🧠 Summary (Super Easy)

| Term          | Meaning                         |
| ------------- | ------------------------------- |
| Rate Limiting | Restrict number of requests     |
| Why?          | Prevent spam, DDOS, brute-force |
| Common rule   | 100 req/min                     |
| Tools         | express-rate-limit, Redis       |
| Response      | 429 Too Many Requests           |
| Algorithms    | Token bucket, Leaky bucket      |

